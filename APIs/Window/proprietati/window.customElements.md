# window.customElements

Este o referință către un obiect `CustomElementRegistry`. Cu ajutorul metodelor acestui obiect, se pot înregistra obiecte noi sau se pot obține informații despre alte element custom.

Metode oferite prin interfața `CustomElementRegistry`:

- `define()`,
- `get()`,
- `upgrade()`,
- `whenDefined()`.

De cele mai multe ori, va fi folosită această metodă pentru a obține accesul la metoda `define` care permite înregistrarea unui nou element.

```javascript
let customElementRegistry = window.customElements;
customElementRegistry.define('my-custom-element', MyCustomElement);
```

Versiunea de mai sus este o prescurtare a ceea ce se petrece în mai mare detaliu așa cum este exemplificat de MDN.

```javascript
customElements.define('element-details',
  class extends HTMLElement {
    constructor() {
      super();
      const template = document
        .getElementById('element-details-template')
        .content;
      const shadowRoot = this.attachShadow({mode: 'open'})
        .appendChild(template.cloneNode(true));
    }
  }
);
```

Mai multe exemple la https://github.com/mdn/web-components-examples/.

## Resurse

- [Window.customElements | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/customElements)
