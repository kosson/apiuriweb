# Web components

Componentele web folosesc trei tehnologii diferite care sunt folosite împreună:

- [Elemente custom](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements), fiind elemente HTML perfect valide,
- [Shadow DOM](https://dom.spec.whatwg.org/#shadow-trees) ce permit izolarea CSS-ului și a JavaScript-ului în ceva asemănător iframe-urilor și
- [HTML templates](https://html.spec.whatwg.org/multipage/scripting.html#the-template-element) care sunt fragmente de HTML, dar care nu sunt afișate până când nu sunt apelate.

## Elementele custom

Sunt elemente pe care le putem numi cum dorim cu mențiunea că trebuie să conțină o linie (caracterul minus) în numele lor: `<elementul-meu>` (kebab-style).

Aceste elemente personalizate au propria semantică, au propriul comportament și markup. Companiile care construiesc browsere, nu introduc elemente custom în browsere pentru a preveni orice conflict. Tag-urile HTML5 au drept corespondent în DOM un singur element. În cazul elementelor particularizate, acestea pot avea multiple elemente la rândul lor.

API-ul `Window.customElements` oferă posibilitatea de a crea elemente noi. Un element nou este compus din două lucruri: numele elementului nou redactat cu liniuță (minus) și numele unei clase care va extinde clasa `HTMLElement`.

Pentru a defini comportamentul unui element personalizat, trebuie creat comportamentul care va guverna viitorul element folosind JavaScript. În exemplul alăturat, vom crea elementul `<componenta-proprie>`.

```javascript
class ComponentaProprie extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<h1>Conținutul elementului</h1>`;
  }
}
customElements.define('componenta-proprie', ComponentaProprie);
```

Reține faptul că legătura `this` se va face instanța elementului nou creat.

Din moment ce este introdus tag-ul, componenta va expune conținutul.

```html
<my-component></my-component>
```

Dacă ai un `<template>` pe care l-ai creat deja, poți indica ca de fiecare dată când apare în DOM numele noului element, să fie introdus conținutul template-ului.

```javascript
class NouElement extends HTMLElement {
  connectedCallback() {
    const template = document.getElementById('nou-element');
    const node = document.importNode(template.content, true);
    this.appendChild(node);
  }
}
```

Metoda `connectedCallback()` nu este constructorul. Această metodă adaugă conținut componentei și, în general, o inițializează.

### lifecycle methods

## Shadow DOM

Acest fragment de DOM este izolat de conținutul DOM-ului existent în pagină (*light DOM*). Trebuie să-ți imaginezi că acel fragment de document este închis într-o capsulă care îl separă de restul documentului. Accesul se poate face doar într-un anumit context. Acest comportament se numește încapsulare.

Selecția elementelor în *light DOM* se face cu ajutorul metodelor `document.querySelector('selectorul)`, iar pentru elementele care stau în *shadow root*, selecția se face cu aceleași metode, dar care în acest caz sunt puse la dispoziție de `shadowRoot`: `shadowRoot.querySelector('selector')`. Din *light DOM* nu poți selecta elemente aflate în *shadow DOM*.

Pentru a atașa un *shadow root* într-un document vei folosi metoda `attachShadow()`.

```javascript
const shadowRoot = document.getElementById('insertie').attachShadow({ mode: 'open' });
shadowRoot.innerHTML = `
  <style>
    p {
      color: red;
    }
  </style>
  <p>Ceva foarte simplu>
`;
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
  // Instanțiază conținutul template-ului
  const instance = document.importNode(fragment.content, true);
  // Introdu datele în template (hidratează)
  instance.querySelector('.title').innerHTML = book.title;
  instance.querySelector('.author').innerHTML = book.author;
  // Inserează instanța creată în locul desemnat din DOM
  document.getElementById('books').appendChild(instance);
});
```

Secvența standard ar fi următoarea:

```javascript
const template = document.querySelector('template');
const node = document.importNode(template.content, true);
document.body.appendChild(node);
```

Magia este realizată prin metoda `importNode` care va face o copie de adâncime (`true`) a conținutului (`template.content`) care va fi gata să fie inserată în document sau într-un document fragment. Dacă am fi utilizat `template.content` direct, l-am fi atașat DOM-ului, dar o funcție care are rolul să genereze mai multe noduri utilizând template-ul, nu va mai avea conținul acestuia la dispoziție (`null`) pentru că acesta a fost utilizat fără copiere prin mutare.

Metoda `importNode` permite utilizarea repetată a conținutului unui template.

Un `template` poate folosi orice fel de cod HTML.

```html
<template>
  <script></script>
  <style></style>
  <!-- Restul codului HTML -->
</template>
```

## Referințe

- [An Introduction to Web Components | css-tricks.com | Caleb Williams | Mar 18, 2019](https://css-tricks.com/an-introduction-to-web-components/)
- [Web Components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
- [A Complete Introduction to Web Components in 2022 | Craig Buckler, September 30, 2022](https://kinsta.com/blog/web-components/)
