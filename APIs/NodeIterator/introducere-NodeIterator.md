# NodeIterator

Această interfață este un iterator care acoperă membrii unei liste de noduri dintr-un sub-arbore al DOM-ului.
Nodurile vor fi returnate în ordinea lor din document. Similar lui `HTMLCollection` sau `NodeList` poți continua utilizarea obiectului fiind unul care ține referințe live spre deosebire de un `NodeList` static returnat de `querySelectorAll`, de exemplu, pe care trebuie să-l reinițiezi ori de câte ori apare o modificare.

Un obiect `NodeIterator` se poate crea folosind metoda `Document.createNodeIterator()`, care are următoarea semnătură.

```javascript
const nodeIterator = document.createNodeIterator(root, whatToShow, filter);
```

Acest obiect este folosit, de obicei, în strânsă legătură cu `NodeFilter` și `TreeWalker`.

## Resurse

- [6.1. Interface NodeIterator | DOM Living Standard — Last Updated 23 March 2021](https://dom.spec.whatwg.org/#nodeiterator)
- [When to use NodeIterator | Stack Overflow](https://stackoverflow.com/questions/7941288/when-to-use-nodeiterator/7945404)
