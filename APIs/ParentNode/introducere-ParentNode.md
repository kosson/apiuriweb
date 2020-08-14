# Introducere ParentNode

Acesta este un obiect mixin care oferă proprietățile și metodele comune tuturor tipurilor de obiecte `Node` care au copii. Proprietățile și metodele sunt implementate și de obiectele `Element`, `Document` și `DocumentFragment`.

## Proprietăți

### ParentNode.childElementCount

Este o proprietate read-only.
Returnează numărul copiilor unui `ParentNode` care sunt elemente DOM.

### ParentNode.children

Este o proprietate read-only.
Returnează un `HTMLCollection` live care conține toate obiectele `Element` care sunt copiii `ParentNode`-ului curent. Sunt omise toate nodurile care nu sunt `Element`.

### ParentNode.firstElementChild

Este o proprietate read-only.
Returnează primul nod care este copil al lui `ParentNode`, dar care este și `Element`. În caz că nu există, este returnat `null`.

### ParentNode.lastElementChild

Returnează ultimul nod care este copil al lui `ParentNode`, dar care este și `Element`. În caz că nu există, este returnat `null`.

## Metode

### ParentNode.querySelector()

Metoda va returna primul `Element` având elementul curent ca rădăcină și care satisface grupul de selectori menționați în argument.

### ParentNode.querySelectorAll()

Metoda returnează un `NodeList` care reprezintă o listă de elemente care are elementul curent drept root și care satisface grupul de selectori menționați în argument.

### ParentNode.replaceChildren()

Metoda înlocuiește copiii unui nod cu un nou set de copii.

## Referințe

- [ParentNode | MDN](https://developer.mozilla.org/en-US/docs/Web/API/ParentNode)
