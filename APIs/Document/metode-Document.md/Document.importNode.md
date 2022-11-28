# document.importNode()

Returnează o clonă a unui `Node` sau a unui `DocumentFragment` dintr-un document extern. Această copie nu este insertată în DOM.

Pentru a introduce fragmentul în DOM va trebui să folosești metodele `appendChild()` sau `insertBefore()` ale unui nod existent deja.

## Parametrii

Parametrii posibili sunt:

- primul parametru este nodul unde se face atașarea;
- al doilea parametru este un Boolean care dacă este `true` va copia întregul arbore a clonei. Valoarea din oficiu este `false`.

## Resurse

- [Document.importNode() | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/importNode)