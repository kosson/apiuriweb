# Cache

Este un mecanism de stocare în baza unor obiecte `Request` / `Response` care sunt introduse într-o zonă tampon a browserului. Obiectele `request` pot fi percepute drept cheile din obiectul cache creat.

Acest mecanism joacă un rol central în lucrul cu `ServiceWorker`-ii, dar trebuie reținut faptul că odată inițiat este disponibil atât serviceworker-ului, cât și browser-ului. Obiectul global dedicat cacheing-ului se numește `caches`, fiind o instanță a interfeței `CacheStorage`. Acesta oferă metodele de lucru:

- `delete()`,
- `has()`,
- `keys()`,
- `match()`,
- `open()`

Elementele care sunt introduse în cache, nu sunt actualizate decât atunci când se face asta înadins și nu sunt șterse decât dacă acest lucru este necesar.

Pentru a folosi `Cache`-ul, acesta trebuie deschis folosind metoda `open()`. Ceea ce se petrece este instanțierea unui obiect `CacheStorage`, care este o promisiune.

Interfața `CacheStorage` oferă și un director principal în care se găsesc cache-uri cu nume ce pot fi accesate de un `ServiceWorker` sau de programele JavaScript care lucrează în `window`.

Cache-urile pot fi gândite ca zone care poartă un nume în care se pot pune resurse necesare.
Atunci când instanțiezi un obiect `CacheStorage` cu metoda `open()`, trebuie să dai un nume acestui nou cache. Numele poate fi pasat metodei `open()` ca argument string.

## Metode

### Metoda `caches.open(cacheName)`

Metoda returnează o promisiune care rezolvă un obiect `Cache`, care este referit de stringul pasat drept prim argument al metodei. Dacă nu există cache-ul referit prin argument, va fi creat un nou cache, fiind returnată o promisiune care rezolvă către obiectul cache nou creat.

```javascript
caches.open(numeleCache).then(function(cache) {
  // Începe lucrul cu acest cache
});
```

Pentru exactitate, `caches` este o proprietate a obiectului mixin `WindowOrWorkerGlobalScope`, acesta fiind motivul pentru care este disponibil din `Window`. Pentru a face o referință către un obiect cache, se poate apela direct din `window`, apelând `caches` sau poate fi referită cu `self.caches`.

```javascript
var cacheUl = self.caches;
```

Exemplu de adăugare a unor resurse într-un cache.

```javascript
this.addEventListener('install', function(event) {
  // tratarea evenimentului.
});
```

### Metoda `Cache.match(request, options)`

Această metodă verifică dacă există un anumit `Request` sau un url în format string pentru un obiect `Response` deja existent. Metoda va returna o promisiune în cazul în care există o resursă în cache sau `undefined` în cazul în care nu există. Această metodă poate fi aplicată pe `caches` pentru a căuta în toate cache-urile, dar poate fi aplicată și pe un cache unic, dacă scenariul de lucru o cere - `cache.match()`.

```javascript
caches.match(request, options).then(function(response) {
  // prelucrează răspunsul
});
```

Obiectele cache vor fi cercetate în ordinea în care acestea au fost create.

Metoda returnează o promisiune care rezolvă către un răspuns asociat cererii corespondente făcute obiectului `Cache`.

Primul arument pasat metodei (`request`) poate fi înțeles ca o veritabilă cheie pentru elementele existente în obiectul cache. Acesta este un obiect `Request` sau un string URL al unui obiect `Request`.

Opțional, poate fi pasat un al doilea argument care este un obiect cu posibile configurări. Aceste configurări modelează cum vor fi făcute căutările în cache. Sunt posibile următoarele proprietăți:

- `ignoreSearch`, fiind un `Boolean` care specifică dacă procesul de căutare ar trebui să ignore query string-ul din url. De exemplu, dacă este setat la valoarea `true`, un posibil querystring `?valoare:ceva` ca parte a `http://www.undeva.ro/?valoare:ceva`, va fi ignorată atunci când se va face o căutare. Valoarea din oficiu este `false`;
- `ignoreMethod`, fiind un `Boolean`, care în cazul în care este setat la `true`, previne ca operațiunile de regăsire să valideze metoda `http` a obiectului `Request`. De regulă, doar metodele `GET` și `HEAD` sunt permise. Valoarea din oficiu este `false`;
- `ignoreVary` este un `Boolean` care atunci când este setat la valoarea `true` instruiește operațiunea de căutare să nu performeze o căutare VARY. Cu alte cuvinte, dacă se potrivește URL-ul, vei obține o potrivire indiferent dacă obiectul `Response` are un header `VARY` sau nu. Valoarea din oficiu este `false`;
- `cacheName` este un `DOMString` care indică un anumit cache în care să se facă căutarea.

### Metoda `Cache.matchAll(request, options)`

Returnează o promisiune care rezolvă către un array de cereri către obiectul cache.

### Metoda `Cache.add(request)`

Metoda preia un URL, aduce resursele la care acesta trimite și adaugă respectivul obiect de răspuns cache-ul construit. Funcțional vorbind, este echivalent operațiunilor făcute cu `fetch()` combinat cu metoda `put()` pentru a adăuga rezultatele în cache.

### Metoda `Cache.addAll(requests)`

Metoda preia un array de URL-uri, aduce resursele și adaugă respectivul obiect de răspuns în cache.

### Metoda `Cache.put(request, response)`

Adaugă în cache deopotrivă obiectul request și response.

### Metoda `Cache.delete(request, options)`

Caută în obiectul cache o cheie reprezentată de request și returnează o promisiune care rezolvă la `true` dacă datele există și au fost șterse. Dacă nu au fost găsite date, atunci promisiunea va rezolva la `false`.

### Metoda `Cache.keys(request, options)`

Returnează o promisiune care rezolvă la un array de chei existente în obiectul cache.

## Exemplu de lucru

Verificarea unei cereri dacă există deja în cache. Acest lucru în faci folosind metoda `match()`, care returnează o promisiune în cazul în care găsește resursa cerută în cache. Dacă nu este găsită resursa (situația `catch`) în cache, adu-o din rețea folosind un apel `fetch(event.request)`. Dacă nu găsești resursa în cache, deschide cache-ul și introdu resursa (`response`). Acum, va trebui să trimiți apelantului resursa adusă, care a fost pusă deja în cache. Pentru acest lucru este nevoie să faci o clonă a datelor din `response` deoarece, în pasul `put()`, datele au fost deja consumate de metoda  `put()` și nu poți face un chaining.

```javascript
var rapsunsCahed = caches.match(event.request).catch(function () {
  return fetch(event.request);
}).then(function (response) {
  caches.open('versiunea1').then(function (cache) {
    cache.put(event.request, response);
  });
  return response.clone();
}).catch(function () {
  return caches.match('/public/images/NuGăsescBoss.jpg'); // dacă rețeaua e picată și nu ai un răspuns în cache, trimite un răspuns pregătit anterior.
});
```

O versiune ceva mai elaborată, separă acțiunile în funcții dedicate. Vom porni cu un cache identificat prin variabila `cacheName` și o referință către un răspuns construit care va fi servit din oficiu. Mai avem două funcții specializate, una care gestionează răspunsul din oficiu și una care gestionează cererile din cache. Pentru a realiza nivelul de interacțiune, se vor folosi două evenimente dedicate: `fetch` și `activate`.

```javascript
const cacheName = 'v1';
const defaultRequest = new Request('/public/img/NuGăsescBoss.jpg');

function defaultResponse() {
  return caches.match(defaultRequest.clone());
}
/**
* Funcția implementează o strategie CACHE -> NET -> CACHE -> SERVE
*/
function cacheRequest(request, event) {
  // A.
  return caches
    .match(request.clone())
    .then((cachedResponse) => {
      // B.
      return cachedResponse || fetch(request.clone())
        .then((response) => {
          // C.
          event.waitUntil (
            caches.open(cacheName).then(
              (cache) => cache.put(request, response)
            )
          );
          // D.
          return response.clone();
        });
      });
}
// Oferirea răspunsului la cerere
self.addEventListener('fetch', function fetchHandler (event) {
  // E.
  event.respondWith(
    cacheRequest(event.request, event)
      .catch(defaultResponse)
  );
});

// pentru a completa exemplul, vom folosi evenimentul `activate` pentru a face un precache a răspunsului cu scopul de a fi servit ulterior

self.addEventListener('activate', (event) => {
  clients.claim();

  event.waitUntil(
    caches
      .open(cacheName)
      .then((cache) =>
        cache.add(defaultRequest.clone()))
  );
});
```

Funcția `cacheRequest` gestionează situația în care cererea își găsește răspunsul în cache, dar va gestiona și cazul în care avem situația de reject îm evenimentul fetch.

A. În general, între două situații gestionate, asigură-te de clonarea deopotrivă a cererii, cât și a răspunsului până la momentul în care vor fi consumate de ultima operațiune din lanț.

B. În cazul în care avem o înregistrare în cache, vom răspunde cu aceasta sau vom iniția un apel în rețea care să aducă resursa, pe care o vom cache-ui și abia apoi, o vom servi.

C. Pentru a te asigura că operațiunea de cacheing nu este întreruptă prin terminarea serviceworker-ului, vom *ambala* operațiunea în `event.waitUntil` pentru a menține firul de execuție a workerului până când lucrul este încheiat. Asigură-te că returnezi promisiunea pentru că altfel, metoda `waitUntil` nu va afla despre promisiunile din lanț și va termina firul de execuție înainte de a se finaliza.

D. Este răspunsul care este trimis în urma cererii browserului nu înainte de a fi clonat.

E. Pentru ca service worker-ul să poată gestiona o cerere `fetch`, trebuie să folosim `event.respondWith(Promise)` spre deosebire de metoda `waitUntil`, care ține exclusiv de venimentul `fetch`.


## Referințe

- [CacheStorage, Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage)
- [Cache, Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
- [sw-test | Github](https://github.com/mdn/sw-test/)
- [CacheStorage.match() | Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage/match)
