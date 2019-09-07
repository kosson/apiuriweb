# ServiceWorkerRegistration

Interfața reprezintă înregistrarea service worker-ului. Motivul pentru care faci acest lucru este pentru a controla una sau mai multe pagini care au aceeași origine.

Durata de viață a etapei de înregistrare a unui service worker se extinde dincolo de cea a obiectelor `ServiceWorkerRegistration`.

Browserul menține o listă persistentă de obiecte active `ServiceWorkerRegistration`.

## Proprietăți

`ServiceWorkerRegistration` implementează proprietățile lui `EventTarget`.

### `ServiceWorkerRegistration.scope`

Returnează un identificator unic pentru înregistrarea unui service worker. Acest scope trebuie să aibă aceleași origini ale documentului care înregistrează respectivul `ServiceWorker`.

### `ServiceWorkerRegistration.installing`

Proprietatea returnează un service worker a cărei stare este `installing`. Valoarea inițială este `null`.

### `ServiceWorkerRegistration.waiting`

Proprietatea returnează un service worker a cărei stare este `waiting`. Valoarea inițială este `null`.

### `ServiceWorkerRegistration.active`

Returnează un service worker a cărui stare este, fie `activating`, fie `activated`. Valoarea inițială este `null`.

### `ServiceWorkerRegistration.navigationPreload`

Returnează instanța unui `NavigationPreloadManager` asociat unei înregistrări curente de service worker.

### `ServiceWorkerRegistration.pushManager`

Returnează o referință către interfața `PushManager` pentru a gestiona push subscriptions: subscribing, obținerea unei active subscription și accesarea unui status push permission.

## Metodele

Împlementează toate metodele interfeței părinte care este `EventTarget`.

### `ServiceWorkerRegistration.getNotifications()`

Returnează un `Promise` care rezolvă către un array de obiecte `Notification`.

### `ServiceWorkerRegistration.showNotification()`

Afișează notificarea pentru titlul cerut.

### `ServiceWorkerRegistration.update()`

Verifică serverul pentru a vedea dacă sunt versiuni actualizate ale service workerului fără a consulta cache-urile.

### `ServiceWorkerRegistration.unregister()`

Scoate din starea de înregistrat un service worker și returnează o promisiune. Toate poperațiunile pe care service workerul le făcea, vor fi duse la bun final înainte să fie scos ca înregistrat.

## Exemplu de înregistrare

```javascript
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js')
  .then(function(registration) {
    registration.addEventListener('updatefound', function() {
      // dacă este declanșat updatefound înseamnă că
      // este instalat un nou service worker
      var installingWorker = registration.installing;
      console.log('S-a instalat un nou service worker:',
        installingWorker);

      // You can listen for changes to the installing service worker's
      // state via installingWorker.onstatechange
    });
  })
  .catch(function(error) {
    console.log('Operațiunea a eșuat cu detaliile:', error);
  });
} else {
  console.log('Nu ai suport pentru service workeri.');
}
```
