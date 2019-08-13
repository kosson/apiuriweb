# Service Worker

Un service worker este un tip de web worker.

Un service worker este un script JavaScript care rulează continuu în background, având un comportament de interpus între apelurile pe care le face browserul și web. Tot traficul va trece prin service worker: `self.addEventListener('fetch', function (event) {});`.

Toate apelurile vor fi interceptate pentru că service workerul reacționează la evenimente. Astfel, va trata orice cerere pentru o resursă ca un eveniment `fetch`. Chiar poți inspecta o cerere pentru o resursă ca un `event.request`, fiind un obiect în sine.

## Înregistrarea unui service worker

Dat fiind faptul că un service worker este un fișier JavaScript care rulează în background pentru a putea reacționa la evenimente. Acest fișier trebuie înregistrat cu motorul browserului.
Browserul pune la dispoziție obiectul `navigator.serviceWorker`, care expune metoda `register`.

```javascript
if ('serviceWorker' in navigator) {
    window.addEventListener('load', function() {
        navigator.serviceWorker.register('/service-worker.js')
        .then( function (registration) {
            // Registration was successful
            console.log('ServiceWorker are următorul scope: ', registration.scope);
        })
        .catch( function(err) {
            // registration failed :
            console.log('N-am putut înregistra pentru că: ', err);
        });
    });
}
```

Metoda `navigator.serviceWorker.register` returnează o promisiune. La momentul înreistrării trebuie avut în vedere și ceea ce se numește `scope`, care poate fi setat dacă se trimite un obiect de configurare metodei register al cărui membru este.

Scope, adică zona pentru care workerul va acționa, este din oficiu locul în care este fișierul JavaScript care definește workerul. De exemplu, dacă service workerul este definit în `/aplicatie/zonaUnu/swervice-worker.js`, scope-ul implicit este `/aplicatie/zonaUnu/`. Dar poate fi definit pentru anumite rădăcini.

```javascript
if ('serviceWorker' in navigator) {
    window.addEventListener('load', function() {
        navigator.serviceWorker.register('/service-worker.js', {
          scope: '/aplicatia-mea/'
        })
        .then( function (registration) {
            // Registration was successful
            console.log('ServiceWorker are următorul scope: ', registration.scope);
        })
        .catch( function(err) {
            // registration failed :
            console.log('N-am putut înregistra pentru că: ', err);
        });
    });
}
```

Fii foarte atent cum redactezi scope-ul. De exemplu, calea `/aplicatia-mea/` nu este aceeași cu `/aplicatia-mea`.

## Evenimentele principale

Fișierul JavaScript care joacă rolul unui service worker ascultă anumite evenimente importante. Sunt trei evenimente importante pe care service worker-ul ascultă:

- `install`,
- `activate` și
- `fetch`

```javascript
// service-worker.js
self.addEventListener('install', function (event) {});
self.addEventListener('activate', function (event) {});
self.addEventListener('fetch', function (event) {});
```

## Referințe

- [Web workers, HTML: Living Standard, WHATWG](https://html.spec.whatwg.org/multipage/workers.html#workers)
- [Service Workers Nightly, W3C](https://w3c.github.io/ServiceWorker/)
- [Service Worker, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
- [Service Worker Cookbook, Mozilla](https://serviceworke.rs/)
- [Lighthouse, Tools for Web Developers, Google](https://developers.google.com/web/tools/lighthouse/#devtools)
- [Your First Progressive Web App](https://codelabs.developers.google.com/codelabs/your-first-pwapp/#0)
- [Workbox](https://developers.google.com/web/tools/workbox/)
- [Service Workers: an Introduction](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [The offline cookbook, ](https://jakearchibald.com/2014/offline-cookbook)
