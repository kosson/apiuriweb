# NodeIterator

Această interfață este un iterator care acoperă membrii unei liste de noduri dintr-un sub-arbore al DOM-ului.
Nodurile vor fi returnate în ordinea lor din document.

Un obiect `NodeIterator` se poate crea folosind metoda `Document.createNodeIterator()`, care are următoarea semnătură.

```javascript
const nodeIterator = document.createNodeIterator(root, whatToShow, filter);
```

Acest obiect este folosit, de obicei, în strânsă legătură cu `NodeFilter` și `TreeWalker`.
