# Request

Este un constructor cu ajutorul căruia se poate crea un obiect cerere către o resursă la distanță.

```javascript
var cerereNouă = new Request(input[, opțiuni]);
```

Primul parametru este o cale către resursă:

- un URL către resursă,
- un obiect `Request`.

Al doilea parametru are ca valoare un obiect a cărui membri setează felul în care se va face cererea. Acest obiect este opțional.

## Opțiuni de configurare

### `method`

Poate avea ca valoare verbele HTTP: `GET`, `POST`, `HEAD`, etc.
Ține minte faptul că răspunsurile care vin pe `GET` sunt introduse în cache ca în cazul în care apare o cerere ulterioară pe aceeași cale, iar datele de pe server nu diferă față de cererea anterioară, se va servi varianta din cache.

### `headers`

Toate headerele pe care dorești să le adaugi la cerere folosindu-te de contructorul `Headers()`.

### `body`

Constituie corpul cererii. Corpul poate fi oricare din următoarele obiecte:

- Blob,
- BufferSource,
- FormData,
- URLSearchParams,
- USVString,
- ReadableStream

Atenție, cererile folosind metodele `GET` și `HEAD` nu trebuie să aibă corp.

### `mode`

Reprezintă modul în care dorești să faci cererile:

- `cors`
- `no-cors`,
- `same-origin`,
- `navigate`

Valoarea din oficiu este `cors`. Din oficiu în Chrome este `same-origin`.

### `credentials`

Sunt credențialele pe care dorești să le folosești în cerere. Posibilele valori sunt:

- `omit`,
- `same-origin`,
- `include`.

Valoarea din oficiu este `omit`. În Chrome, valoarea din oficiu este `include`.

### `cache`

Această valoare indică cache-ul pe care dorești să-l folosești pentru cerere.

### `redirect`

Precizează modul în care se va face redirectarea:

- `follow`,
- `error` sau
- `manual`.

În Chrome, valoarea din oficiu este `follow`.

### `referrer`

Poate avea valorile:

- `no-referrer`,
- `client` sau un
- URL.

Valoarea din oficiu este `client`.

### `integrity`

Reprezintă valoarea de integritate a unei sub-resurse. Poate fi rezultatul unui algoritm de hashing așa cum este SHA256, cu o posibilă reprezentare `SHA256-a0REd43pp043=)..ș.a.m.d`.

## Referințe

- [Request(), MDN](https://developer.mozilla.org/en-US/docs/Web/API/Request/Request)
