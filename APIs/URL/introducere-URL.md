# API-ul URL

Această interfață este folosită pentru a citi, construi, normaliza și coda URL-uri.

Avantajul de a lucra cu `URL` este că poți citi URL-uri și poți folosi părțile componente sau poți să le modifici.

## Constructorul `new URL()`

Folosind constructorul, poți crea un obiect URL folosind un string al unui url absolut sau relativ și o bază a URL-ului.

## Proprietăți

### `hash`

Este un `USVString` care conține un caracter `#` urmat de un fragment al identificatorului URL-ului.

### `host`

Este un `USVString` care conține domeniul urmat de un caracter `:` în cazul în care avem specificat un port.

### `hostname`

Este un `USVString` care conține domeniul URL-ului.

### `href`

Este un string `USVString` chiar a întregul URL.

### `origin` - readonly

Este o proprietate care returnează un string `USVString` care indică originea URL-ului, adică schema, domeniul și portul.

### `password`

Este un `USVString` care conține parola specificată înainte de numele domeniului.

### `pathname`

Este un `USVString` care conține un caracter inițial `/` urmată de calea URL-ului.

### `port`

Este un `USVString` care conține numărul portului URL-ului.

### `protocol`

Este un string `USVString` care indică protocolul schemei URL-ului incluzând caracterul `:` la final.

### `search`

Este un șir `USVString` care indică parametrii de căutare dacă aceștia există în URL. Este inclus și caracterul `?` cu care aceștia încep.

### `searchParams` - readonly

Este un obiect `URLSearchParams` din care pot fi obținuți fiecare dintre parametri.

### `URL.username`

Este un string `USVString` care conține username-ul specificat înainte de numele domeniului.

## Metode

### `toString()`

Returnează un string `USVString` care conține întregul URL. Poate fi considerat un sinonim al lui `URL.href`, dar nu poate fi folosită pentru a modifica valoarea.

### `toJSON()`

Returnează un string `USVString` ce conține întregul URL. Returnează același string precum proprietatea `href`.

### `createObjectURL`

Returnează un `DOMString` care conține un blob URL unic, adică un URL care are drept schemă `blob:`, urmat de un string opac unic ce identifică obiectul în browser.

### `revokeObjectURL()`

Metoda revocă un obiect URL care a fost creat anterior cu `URL.createObjectURL()`.

## Referințe

- [URL | Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/URL)
- [Get URL and URL Parts in JavaScript | css-tricks.com](https://css-tricks.com/snippets/javascript/get-url-and-url-parts-in-javascript/)
