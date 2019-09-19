# Body

Acesta este un mixin al API-ului `Fetch` și reprezintă corpul unui `request` sau al unui `response`.
Acest mixin este implementat de API-urile `Request` și `Response`.

## Proprietăți

### `Body.body` - readonly

Este un getter care expune conținutul unui `body` ca `ReadableStream`.

```javascript
var stream = responseInstance.body;
```

### `Body.read`

Este un `Boolean` care indică dacă a fost citit corpul.

## Metode

### `Body.arrayBuffer()`

Metoda ia un stream `Response` și îl citește până la capăt și returnează o promisiune care se rezolvă prin crearea unui `ArrayBuffer`.

### `Body.blob()`

Metoda ia un stream `Response` și îl citește până la capăt și returnează o promisiune care se rezolvă prin crearea unui `Blob`.

### `Body.formData()`

Metoda ia un stream `Response` și îl citește până la capăt și returnează o promisiune care se rezolvă prin crearea unui `FormData`.

### `Body.json()`

Metoda ia un stream `Response` și îl citește până la capăt și returnează o promisiune care se rezolvă prin generarea unui text în format `JSON`.

### `Body.text()`

Metoda ia un stream `Response` și îl citește până la capăt și returnează o promisiune care se rezolvă prin crearea unui `USVString` (text) codat UTF-8.
