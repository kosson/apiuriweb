# DocumentFragment

`DocumentFragment` este o interfață care permite crearea unui fragment de cod HTML. Acesta poate fi inserat în DOM după ce a fost creat și populat cu date.

Modificarea fragmenului nu produce reflow pentru că nu este parte a documentului încă.

Fragmentele pot fi inserate în DOM folosind metodele `appendChild` și `insertBefore` pe care `Node` le pune la dispoziție. Apelarea metodelor ia fragmentul și îl mută în DOM. După ce a fost mutat, `DocumentFragment`-ul va rămâne gol.

Pentru că toate elementele din fragment vor fi introduse deodată, se va face reflow o singură dată.

Această interfață este foarte utilă în cazul în care se dorește realizarea de adevărate componente web. De exemplu, elementele `<template>` conțin un `DocumentFragment` în proprietatea `HTMLTemplateElement.content`.
