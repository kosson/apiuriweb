# WindowOrWorkerGlobalScope

Este un obiect mixin care are câteva caracteristici comune interfețelor `Window` și `WorkerGlobalScope`.

Pentru că este un mixin, nu se poate instanția un obiect `WindowOrWorkerGlobalScope`.

## Proprietăți

### `WindowOrWorkerGlobalScope.caches`

Proprietatea returnează obiectul `CacheStorage` asociat contextului curent. Acest obiect permite stocarea offline a resurselor pentru utilizarea lor în scenarii offline. Mai poate fi folosit pentru a genera răspunsuri personalizate către cereri.

### `WindowOrWorkerGlobalScope.indexedDB`

Această proprietate oferă aplicațiilor un mecanism prin care să poată accesa asincron baze de date indexate. Proprietatea returnează un obiect `IDBFactory`.

### `WindowOrWorkerGlobalScope.isSecureContext`

Proprietatea returnează un `Boolean` care indică dacă prezentul context de execuție este securizat sau nu.

### `WindowOrWorkerGlobalScope.origin`

Proprietatea returnează originea scope-ului global serializat ca șir de caractere.

## Metode

Aceste metode sunt definite prin acest mixin, dar sunt implementate de `Window` și `WorkerGlobalScope`.

### `WindowOrWorkerGlobalScope.atob()`

Metoda decodează date care au fost codate ca base-64.

### `WindowOrWorkerGlobalScope.btoa()`

Creează un string ASCII codat conform base-64 dintr-un string de date binare. Mai simplu, codează base-64 date binare.

### `WindowOrWorkerGlobalScope.clearInterval()`

Anulează execuția repetată a unei funcții inițiată prin `WindowOrWorkerGlobalScope.setInterval()`.

### `WindowOrWorkerGlobalScope.clearTimeout()`

Anulează temporizarea realizată prin `setTimeout()`.

### `WindowOrWorkerGlobalScope.createImageBitmap()`

Metoda acceptă surse de imagine și returnează o promisiune care rezolvă un `ImageBitmap`. Opțional, sursa este tăiată prin specificarea unui dreptunghi din care vor fi colectați pixerii, având originea la (`sx` și `sy`) cu `sw` ca lățime și `sh`, ca înălțime.

### `WindowOrWorkerGlobalScope.fetch()`

Este instrumentul prin care aduci o resursă de pe internet.

### `WindowOrWorkerGlobalScope.queueMicrotask()`

Reprezintă o mică funcție care este executată după ce task-ul curent a fost terminat, în condițiile în care nu mai există cod care așteaptă să fie rulat înainte de a returna controlul event loop-ului.

### `WindowOrWorkerGlobalScope.setInterval()`

Metoda programează o funcție care va fi rulată la un anumit interal de timp specificat în milisecunde.

### `WindowOrWorkerGlobalScope.setTimeout()`

Programaează o funcție care să fie executată după trecerea perioadei specificate în milisecunde.
