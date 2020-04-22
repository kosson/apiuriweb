# Stream

Permite accesarea stream-urilor folosind JavaScript pentru a putea folosi datele primite din rețea.

Stream-urile folosesc un set de interfețe care se încadrează în două categorii `Readable` și `Writable`.

## Interfețe `Readable`

### `ReadableStream`

Reprezintă un stream *readable* de date. Acesta poate fi folosit pentru a gestiona stream-urile de răspuns ale API-ului `Fetch` sau a unui stream definit de un developer în baza constructorului `ReadableStream()`.

### `ReadableStreamDefaultReader`

Reprezintă un reader disponibil din oficiu, care poate fi utilizat pentru a citi date venite din rețea (un posibil *fetch*).

### `ReadableStreamDefaultController`

## Referințe

- [Streams Living Standard](https://streams.spec.whatwg.org)
- [Stream, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)
- [The Streams API](https://flaviocopes.com/stream-api/)
