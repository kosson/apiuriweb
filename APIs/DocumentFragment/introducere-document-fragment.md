# DocumentFragment

`DocumentFragment` este o interfață care permite crearea unui fragment de cod HTML care, atenție: **nuare părinte**. În momentul în care a fost creat, un fragment de document, **nu face parte din document** încă și orice modificare poate fi făcută fragmentului fără a afecta documentul paginii. Acesta poate fi inserat în DOM după ce a fost creat și populat cu date.

Modificarea fragmentului **nu produce reflow** pentru că nu este parte a documentului încă.

Fragmentele pot fi inserate în DOM folosind metodele `appendChild` și `insertBefore` pe care `Node` le pune la dispoziție. Apelarea metodelor ia fragmentul și îl mută în DOM. După ce a fost mutat, `DocumentFragment`-ul **va rămâne gol**.

Pentru că toate elementele din fragment vor fi introduse deodată, se va face reflow o singură dată.

Această interfață este foarte utilă în cazul în care se dorește realizarea de adevărate componente web. De exemplu, elementele `<template>` conțin un `DocumentFragment` în proprietatea `HTMLTemplateElement.content`.

## Constructorul `DocumentFragment()`

Creeză și returnează un obiect `DocumentFragment` nou.

## Proprietăți

Proprietățile acestei interfețe sunt moștenite de la părinte: `Node` și le implementează și pe cele ale lui `ParentNode`.
