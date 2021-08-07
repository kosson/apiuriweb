# Introducere în Web Components

Componentele web sunt un set de tehnologii care permit crearea de elemente HTML particularizate, care ascund modul de funcționare față de restul codului paginii. Componentele folosesc ceea ce se numește shadow DOM pentru a separa de restul codului paginii conținutul componentei și CSS-ul necesar modelării vizuale. Un lucru important de reținut este faptul că o componentă web din moment ce a fost creată, poate fi folosită de oricâte ori se dorește cu alte date pentru fiecare instanță.

Datele care populează componenta vin prin intermediul atributelor și chiar din alte componente care pot fi înglobate.

Componentele sunt create folosind trei mari tehnologii:

- Custom elements, care sunt un set de API-uri JavaScript ce permit crearea de elemente particularizate și care mai apoi pot fi folosite după necesitate în construcția interfețelor;
- Shadow DOM, care este un set de API-uri necesar atașării unei structuri DOM care stă în *umbră* - shadow DOM. Această structură DOM specială este randată separat de DOM-ul documentului principal. Această caracteristică permite o configurare prin scripting și CSS fără teama că vor intra în coliziune cu alte părți ale documentului;
- HTML templates care se pot realiza prin folosirea elementelor `<template>` și `<slot>`.

## Crearea de componente

Pentru a cerea adevărate componente în aplicația web, poți crea elemente particularizate.

## Resurse

- [4.13 Custom elements | HTML Living Standard](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements)
- [Web Components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
- [Using custom elements | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements)
