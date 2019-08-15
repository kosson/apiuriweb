# Web Storage

Acesta este un API care oferă mecanismele prin care browserul îți oferă posibiltatea de a stoca perechi cheie/valoare mult mai eficient decât ar face-o mecanismul de cookie.

Cele două mecanisme sunt `sessionStorage` și `localStorage`.

## `sessionStorage`

Oferă câte o zonă de stocare separată pentru fiecare origine dată pentru întreada durată a sesiunii de lucru cu pagina curentă. Acest lucru înseamnă câtă vreme pagina este deschisă, reîncărcată sau este una restaurată. În momentul în care pagina sau tab-ul este închis aceste date vor fi șterse.

Aceste date nu vor fi transferate niciodată către server.

Limita de stocare este în jurul a 5MB.

## `localStorage`

Este un mecanism de stocare similar lui `sessionStorage` cu excepția că acesta va ține minte datele chiar dacă browserul este închis și redeschis.

Ștergerea datelor se poate face programatic folosind JavaScript sau prin curățarea cache-ul browserului, secțiunea localy stored data.

## Referințe

- [Web Storage, MDN]](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)
- [Using the Web Storage API, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
