# HTMLElement.style

Este o proprietate read-only care returnează stylurile inline pentru un element sub forma unui obiect `CSSStyleDeclaration`. Acest obiect conține o listă a tuturor proprietăților care au fost setate inline pentru elementul în cauză. Acest lucru înseamnă că nu vor fi returnate și proprietățile CSS setate cu o foaie de stil. Pentru a obține toate aceste proprietăți, se va folosi `Window.getComputedStyle()`.

Chiar dacă proprietatea este considerată a fi read-only, este posibilă setarea unui stil inline atribuind un string direct proprietății `style`. Problema este că astfel se vor rescrie toate proprietățile inline. Pentru a evita acest comportament, se va seta individual proprietate cu proprietate (a obiectului `CSSStyleDeclaration`) și astfel nu se vor pierde celelalte existente. De exemplu `element.style.backgroundColor = "red"`.

Pentru a reseta o declarație inline, se va seta valoarea acesteia la `null`: `elt.style.color = null`.

## Resurse

- [HTMLElement.style | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
- [CSSStyleDeclaration | MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration)