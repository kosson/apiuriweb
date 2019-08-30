# Web Storage

Acesta este un API care oferă mecanismele prin care browserul îți oferă posibilitatea de a stoca perechi cheie/valoare mult mai eficient decât ar face-o mecanismul de cookie.

Este o interfață care oferă acces la stocare locală și la stocare de sesiune.

Există două mecanisme oferite: `sessionStorage` și `localStorage`.

Obiectul `Storage` folosit de `sessionStorage` va constitui câte o zonă de stocare pentru fiecare origine câtă vreme browserul este deschis. Datele supraviețuiesc reîncărcării paginii.

Dacă dorești ca datele să persiste chiar dacă browserul este închis, se va folosi `localStorage`.

## `sessionStorage`

Oferă câte o zonă de stocare separată pentru fiecare origine dată pentru întreada durată a sesiunii de lucru cu pagina curentă. Acest lucru înseamnă câtă vreme pagina este deschisă, reîncărcată sau este una restaurată. În momentul în care pagina sau tab-ul este închis aceste date vor fi șterse.

Aceste date nu vor fi transferate niciodată către server.

Limita de stocare este în jurul a 5MB.

## `localStorage`

Este un mecanism de stocare similar lui `sessionStorage` cu excepția că acesta va ține minte datele chiar dacă browserul este închis și redeschis.

Ștergerea datelor se poate face programatic folosind JavaScript sau prin curățarea cache-ul browserului, secțiunea *localy stored data*.

Ambele mecanisme permit scrierea de chei - valori folosind și notația cu punct așa cum este caracteristic obiectelor, dar mai permit și introducerea de chei-valori prin notația cu paranteze drepte.

```javascript
sessionStorage.cheie = 'ceva';
sessionStorage.getItem('cheie'); // ceva
sessionStorage['alta'] = 'altceva';
sessionStorage.getItem('alta'); // altceva
```



## Referințe

- [Web Storage, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)
- [Using the Web Storage API, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
