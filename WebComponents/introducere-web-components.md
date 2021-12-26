# Web components

Componentele web folosesc trei tehnologii diferite:

- [Elemente custom](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements), fiind elemente HTML perfect valide,
- [Shadow DOM](https://dom.spec.whatwg.org/#shadow-trees) ce permit izolarea CSS-ului și a JavaScriptului în ceva asemănător iframe-urilor și
- [HTML templates](https://html.spec.whatwg.org/multipage/scripting.html#the-template-element) care sunt fragmente de HTML, care nu sunt afișate până când nu sunt apelate.

## Elementele custom

Sunt elemente pe care le putem numi cum dorim cu mențiunea că trebuie să conțină o linie (caracterul minus) în redactarea lor: `<elementul-meu>` (kebab-style).

Aceste elemente personalizate au propria semantică, au propriul comportament și markup. Companiile care construiesc browsere, nu introduc elemente custom pentru a preveni orice conflict. Tag-urile HTML5 au drept corespondent în DOM un singur element. În cazul elementelor particularizate, acestea pot avea multiple elemente la rândul lor.

Pentru a defini comportamentul unui element personalizat, trebuie creat comportamentul care va guverna viitorul element folosind JavaScript. În exemplul alăturat, vom crea elementul `<componenta-proprie>`.

```javascript
class ComponentaProprie extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<h1>Conținutul elementului</h1>`;
  }
}
customElements.define('componenta-proprie', ComponentaProprie);
```

Din moment ce este introdus tag-ul, componenta va expune conținutul.

```html
<my-component></my-component>
```

## Șabloane HTML

Elementul `<template>` ne permite să constituim șabloane reutilizabile de cod în fluxul normal al HTML. Aceste fragmente nu vor fi afișate imediat.

```html
<template id="book-template">
  <li><span class="title"></span> &mdash; <span class="author"></span></li>
</template>

<ul id="books"></ul>
```

Exemplul de mai sus nu va fi afișat, așteptând să fie consumat de un script care va introduce conținut și va instrui browserul ce să facă cu el.

```javascript
const fragment = document.getElementById('book-template');
const books = [
  { title: 'The Great Gatsby', author: 'F. Scott Fitzgerald' },
  { title: 'A Farewell to Arms', author: 'Ernest Hemingway' },
  { title: 'Catch 22', author: 'Joseph Heller' }
];

books.forEach(book => {
  // Create an instance of the template content
  const instance = document.importNode(fragment.content, true);
  // Add relevant content to the template
  instance.querySelector('.title').innerHTML = book.title;
  instance.querySelector('.author').innerHTML = book.author;
  // Append the instance ot the DOM
  document.getElementById('books').appendChild(instance);
});
```

## Referințe

- [An Introduction to Web Components | css-tricks.com](https://css-tricks.com/an-introduction-to-web-components/)
- [Web Components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
