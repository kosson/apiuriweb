# DocumentFragment

`DocumentFragment` este o interfață care permite crearea unui fragment de cod HTML care, atenție: **nu are părinte**. În momentul în care a fost creat, un fragment de document, **nu face parte din document** încă.

Orice modificare poate fi făcută fragmentului fără a afecta documentul paginii. Acesta poate fi inserat în DOM după ce a fost creat și populat cu date.

Modificarea fragmentului **nu produce reflow** pentru că nu este parte a documentului încă.

Fragmentele pot fi inserate în DOM folosind metodele `appendChild` și `insertBefore` pe care `Node` le pune la dispoziție. Apelarea metodelor ia fragmentul și îl mută în DOM. După ce a fost mutat, `DocumentFragment`-ul **va rămâne gol**.

Pentru că toate elementele din fragment vor fi introduse deodată, se va face reflow o singură dată. MDN oferă un exemplu rapid pentru un `<ul id="list"></ul>`

```javascript
var list = document.querySelector('#list')
var fruits = ['Apple', 'Orange', 'Banana', 'Melon']

var fragment = new DocumentFragment()

fruits.forEach(function (fruit) {
  var li = document.createElement('li')
  li.innerHTML = fruit
  fragment.appendChild(li)
})

list.appendChild(fragment)
```

Această interfață este foarte utilă în cazul în care se dorește realizarea de adevărate componente web. De exemplu, elementele `<template>` conțin un `DocumentFragment` în proprietatea `HTMLTemplateElement.content`.

## Constructorul `DocumentFragment()`

Creeză și returnează un obiect `DocumentFragment` nou.

## Proprietăți

Proprietățile acestei interfețe sunt moștenite de la părinte: `Node` și le implementează și pe cele ale lui `ParentNode`.

### ParentNode.children

Returnează un `HTMLCollection` live ce conține toate obiectele de tip `Element` care sunt copii ai obiectului `DocumentFragment`.

### ParentNode.firstElementChild

Returnează un `Element` care este primul copil al unui obiect `DocumentFragment` sau `null` dacă nu există niciunul.

## Referințe

- [4.7. Interface DocumentFragment | DOM Living Standard](https://dom.spec.whatwg.org/#interface-documentfragment)
- [DocumentFragment | MDN](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment)
