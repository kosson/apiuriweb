# Request

Este o interfață a API-ului Fetch.

## Constructor `Request()`

Creează un obiect `Request`.

## Exemplu

```javascript
const request = new Request('https://www.mozilla.org/favicon.ico');

const URL = request.url;
const method = request.method;
const credentials = request.credentials;

fetch(request)
  .then(response => response.blob())
  .then(blob => {
    image.src = URL.createObjectURL(blob);
  });
```

sau

```javascript
const request = new Request('https://example.com', {method: 'POST', body: '{"foo": "bar"}'});

const URL = request.url;
const method = request.method;
const credentials = request.credentials;
const bodyUsed = request.bodyUsed;
```
