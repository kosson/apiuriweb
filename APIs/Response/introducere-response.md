# `Response`

Aceasta este o interfață a API-ului `Fetch`.

Chiar dacă ai putea crea un răspuns prin instanțierea constructorului `Response`, mai curând, un obiect `Response` va fi returnat ca rezultat al unei alte operațiuni API. De exemplu un `FetchEvent.respondWith()`) al unui webworker sau un simplu `fetch()` (`WindowOrWorkerGlobalScope.fetch()`).

## Proprietăți

### `Response.headers`

Conține un obiect `Headers` asociat răspunsului.

### `Response.ok`

Este o valoare `Boolean` care indică dacă răspunsul este unul de succes sau nu. Succesul este în plaja 200 - 299.

### `Response.redirected`

Indică dacă răspunsul este rezultatul unei redirectări sau nu, ceea ce înseamnă că lista URL are mai multe intrări.

### `Response.status`

Este un mesaj de stare cu un cod de stare.

### `Response.statusText`

Conține mesajul codului de stare.

### `Response.type`

Conține tipul răspunsului - `basic` sau `cors`.

### `Response.url`

Conține URL-ul răspunsului.

### `Response.useFinalURL`

Conține o valoare `Boolean` care indică dacă aceasta este varianta finală a URL-ului răspunsului.
