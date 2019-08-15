# Strategie de caching a resurselor

Aceasta este o strategie de aducere a unor resurse, care este combinată cu mecanismul de caching al browserului pentru a realiza un balans între ceea ce poate fi repede luat mai întâi din cache și apoi de pe net cu o ulterioară actualizare a cache-ului.

```javascript
// client-app.js
var url = window.location.href; // https://undeva.ro/v1/meteo.csv
var netDataPrezent = false;

/* O rută GET */
// caută pe net resursa mai intâi
fetch(url).then(function (raspuns) {
  return raspuns.json();
}).then(function (date) {
  console.log(date);
  netDataPrezent = true; // vreau sa folosesc datele acestea pentru că reteaua este rapida
  curataContinutulExistentDeja(); // o funcție care sa curețe zona de DOM de preexistente. Altfel, vei avea înregistrări duplicat
  injecteazaDateIntrUnTemplate(date);
});

/* O rută POST */
fetch(url, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  },
  body: JSON.stringify({
    'message': 'Bau!'
  });
}).then(function (raspuns) {
  return raspuns.json();
}).then(function (date) {
  console.log(date);
  netDataPrezent = true; // vreau sa folosesc datele acestea pentru că reteaua este rapida
  curataContinutulExistentDeja(); // o funcție care sa curețe zona de DOM de preexistente. Altfel, vei avea înregistrări duplicat
  injecteazaDateIntrUnTemplate(date);
});

// dacă netul este lent, se vor cere resursele din cache în așteptarea celor live
if ('caches' in window) {
  // vezi dacă resursa cerută nu cumva se află deja în cache.
  caches.match(url).then(function (raspuns) {
    // dacă resursa există în cache
    if (raspuns) {
      return raspuns.json();
    }
  }).then(function (date) {
    if (!netDataPrezent) {
      curataContinutulExistentDeja(); // o funcție care sa curețe zona de DOM de preexistente. Altfel, vei avea înregistrări duplicat
      // dacă nu am date primite direct din rețea, abia tunci folosește cache-ul
      injecteazaDateIntrUnTemplate(date);
    }
  });
}
```

Această strategie va funcționa în tandem cu un service-worker.js care ar putea avea următoarea structura.

```javascript
var CACHE_STATIC_NAME = 'static-v1';
var CACHE_DYNAMIC_NAME = 'dinamic';

self.addEventListener('install', (event) => {
  console.log('SW spune că s-a instalat frumos! ', event);
  /* ===== INIȚIEREA MECANISMULUI DE CACHING ===== */
  event.waitUntil(
    // caches reprezintă întregul director de cache-uri
    caches.open(CACHE_STATIC_NAME).then(function adaugaResursele(cache) {
      // argumentul cache este o referință către cache-ul care tocmai a fost creat
      // console.log('[Service Worker] - se face pre-caching-ul');
      // toate stringurile pasate lui cache.addAll vor fi pasate în obiecte `Request`.
      cache.addAll([
        '/',
        '/index.html',
        '/js/imagecapture.js',
        '/js/imagecapture.mjs',
        '/js/pathseg.js',
        '/js/screenfull',
        '/js/app-client.js',
        '/css/main.css',
        '/images/logo152.png'
      ]).then((responseArray) => {
        console.log('EventListener responseArray ' + responseArray);
        self.skipWaiting();
      }).catch((err) => {
        // indică dacă unul sau mai multe apeluri au eșuat
        if (err) throw err;
      });
      // cache.add('/index.html'); // adăugarea linie cu linie
    })
  ); // pentru a te asigura că mecanismul de caching este instalat, execută cu `waitUntil()`
});


self.addEventListener('activate', (event) => {
  console.log('SW spune că s-a activat și iată dovada: ', event);
  /* ==== AICI SE VOR CURĂȚA VERSIUNILE VECHI DE CACHE ==== */
  // așteaptă până când se încheie curățarea cache-urilor înainte să procedezi la următoarea etapă
  event.waitUntil(
    // obține cheile ce reprezintă toate cache-urile făcute
    caches.keys().then(function (keyList) {
      return Promise.all(keyList.map(function (key) {
        // transformă array-ul cache-urilor într-un array de promisiuni pentru a fi consumat de Promise.all
        if (key !== CACHE_STATIC_NAME && key !== CACHE_DYNAMIC_NAME) {
          // dacă găsim vreun cache care nu este cel curent (static-v1) și nici cel dinamic (dynamic-bibliokulus), sterge-l!
          console.log('Șterg vechitura: ', key);
          caches.delete(key); // operațiunea returnează o promisiune, care se adaugă array-ului ce va fi consumat cu Promise.all
        }
      }));
    })
  );
  return self.clients.claim();
});


self.addEventListener('fetch', (event) => {
  // console.log('SW spune la fetch: ', event);
  event.respondWith(
    /* === NETWORK FIRST STRATEGY === */
    // fetch(event.request).catch((err) => {return caches.match(event.request)})

    /* ==== CACHE FIRST STRATEGY */
    // caută în directorul principal de cache-uri o cheie (obiect răspuns) echivalentă cu cererea serviceworker-ului. Cîutarea se face în toate versiunile de cache-uri.
    caches.match(event.request).then(function (response) {
      // dacă nu ai nicio înregistrare în cache care să răspundă corespondent cereriii cu obiectul request, response va avea valoarea null
      if (response ) {
        return response; // dacă ai găsit un matching response la request, acesta va fi returnat.
      } else {
        // dacă nu ai găsit în cache o înregistrare corespondentă, încearcă direct la server. Returnează neapărat rezultatul.
        return fetch(event.request).then(function aduSiCashIt (res) {
          // ceea ce aduci de la server, bagă finamic în cache
          return caches.open(CACHE_DYNAMIC_NAME).then(function (cache) {
            cache.put(event.request.url, res.clone()); // în cache pui o clna care conține toate datele obiectului răspuns
            return res; // în acest moment obiectul răspuns a fost consumat și trebuie returnat cererii.
          });
        }).catch((err) => {
          // if (err) console.log(err);
          return caches.open(CACHE_STATIC_NAME).then((cache) => {
            return cache.match('/offline.html');
          });
        });
      }
    })
  );
});
// const
//   version = '0.3.0',
//   CACHE = version + '::CEva',
//   offlineURL = '/offline/',
//   installFilesEssential = [
//     '/',
//     '/manifest.json',
//     '/css/main.css',
//     '/js/app-client.js',
//     '/js/imagecapture.js',
//     '/js/imagecapture.mjs',
//     '/js/pathseg.js',
//     '/js/offline.js',
//     '/images/logo/logo152.png'
//   ].concat(offlineURL),
//   installFilesDesirable = [
//     '/favicon.ico'
//   ];
  ```

  În service-worker.js putem adopta o strategie *cache-then-network* + *cache-only* + *cache-with-network-fallback*. Această strategie seamnă mai mult cu una de routare pentru că poți controla care resursă se încarcă în funcție de care strategie.

  ```javascript
/* === STRATEGIA cache-then-network === */
self.addEventListener('fetch', function (event) {
  var urlUlMeuDeInteres = window.location.href; // apel către api pentru a cere resurse.Deocamdată aplic pe root.
  // implementarea strategiei *cache-then-network*
  if (event.request.url.indexOf(url) > -1) { // însemnând că s-a făcut o cerere pe această cale
    event.respondWith(caches.open(CACHE_DYNAMIC_NAME).then(function (cache) {
      return fetch (event.request).then(function (rezultat) {
        cache.put(event.request, rezultat.clone());
        return rezultat;
      });
    }));
  /* === STRATEGIA cache-only */
  } else if (new RegExp('\\b' + STATIC_FILES.join('\\b|\\b') + '\\b').test(event.request.url)) {
    // strategia cache-only, care va servi fișierele neapărat necesare numai din cache, fără a mai cere de pe rețea.
    self.addEventListener('fetch', function (event) {
      event.respondWith(caches.match(event.request));
    });
  /* === STRATEGIA cache-with-network-fallback === */
  } else {
    event.respondWith(
      /* === NETWORK FIRST STRATEGY === */
      // fetch(event.request).catch((err) => {return caches.match(event.request)})

      /* ==== CACHE FIRST STRATEGY */
      // caută în directorul principal de cache-uri o cheie (obiect răspuns) echivalentă cu cererea serviceworker-ului. Cîutarea se face în toate versiunile de cache-uri.
      caches.match(event.request).then(function (response) {
        // dacă nu ai nicio înregistrare în cache care să răspundă corespondent cereriii cu obiectul request, response va avea valoarea null
        if (response ) {
          return response; // dacă ai găsit un matching response la request, acesta va fi returnat.
        } else {
          // dacă nu ai găsit în cache o înregistrare corespondentă, încearcă direct la server. Returnează neapărat rezultatul.
          return fetch(event.request).then(function aduSiCashIt (res) {
            // ceea ce aduci de la server, bagă finamic în cache
            return caches.open(CACHE_DYNAMIC_NAME).then(function (cache) {
              cache.put(event.request.url, res.clone()); // în cache pui o clna care conține toate datele obiectului răspuns
              return res; // în acest moment obiectul răspuns a fost consumat și trebuie returnat cererii.
            });
          }).catch((err) => {
            // if (err) console.log(err);
            return caches.open(CACHE_STATIC_NAME).then((cache) => {
              if (event.request.headers.get('accept').includes('text/html')) {
                return cache.match('/offline.html');
              }
            });
          });
        }
      })
    );
  }
});
  ```
