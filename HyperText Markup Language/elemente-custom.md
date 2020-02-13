# Elemente custom

Aceste elemente sunt create de programator, care spre deosebire de tagurile HTML cu care suntem obișnuiți deja, trebuie să aibă o liniuță precum în `<nou-element>`.

Elementele custom pot avea propria semnatică. Realizarea de elemente particularizate implică realizarea unei adevărate componente de pagină web. Nu poți constitui un același tag custom de mai multe ori.

De exemplu, să presupunem că dorim ca de fiecare dată când introducem un nou element `<ceva-nou>`, să fie afișat un paragraf de text.

```html
<ceva-nou></ceva-nou>
```

Acest nou element are nevoie de cod în JavaScript pentru a produce efectul necesar. În acest sens, se va face o extindere a interfeței `HTMLElement`.

```javascript
class ComponentaNoua extends HTMLElement {
  unCallback() {
    this.innerHTML = `<h1>Salutare!</h1>`;
  }
}

customElements.define('ceva-nou', ComponentaNoua);
```

Pentru a crea un element nou, se utilizează obiectul global `customElements`. O alternativă la structura de cod de mai sus ar fi cea în care clasa este introdusă direct și folosește un template pregătit.

```javascript
customElements.define('ceva-nou', class extends HTMLElement {
    constructor () {
      super(); // apelează întotdeauna super()
    }
    connectedCallback() {
      this.innerHTML = `<h1>Salutare!</h1>`;
    }
  }
);
```

## Shadow DOM

Shadow DOM este un Document Object Model într-o capsulă izolată de restul DOM-ului. Shadow DOM oferă posibilitatea de a compune fragmente DOM, care atunci când reprezintă elemente custom, se deschide un tărâm de posibilități infinite. Pur și simplu, prin introducerea în DOM a unui tag custom, ai posibilitatea de a introduce adevărate aplicații.

Să presupunem că vom crea un template.

```javascript
let sablon = document.createElement('<template>');
sablon.innerHTML = `
  <style>.ceva {}</style>
  <em>Ceva interesant</em>
  <unitate-bibliografica></unitate-bibliografica>
`;

customElements.define('ub-noua', class extends HTMLElement {
  constructor(){
    super();
    let radacinaShadow = this.attachShadow({
      mode: 'open'
    });
    radacinaShadow.appendChild(sablon.content.cloneNode(true));
  }
});
```

## Crearea elementelor folosind un `<template>`

Introducând conținut într-un element `template` prezintă posibilitatea de a crea adevărate componente.

```html
<template id="un-template">

</template>
```

## Resurse

- [An Introduction to Web Components | css-tricks.com](https://css-tricks.com/an-introduction-to-web-components/)
- [4.13 Custom elements | HTML Living standard](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements)
- [Custom Elements v1: Reusable Web Components | developers.google.com](https://developers.google.com/web/fundamentals/web-components/customelements)
- [Window.customElements | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/customElements)
