# Construcția elementelor

Ai posibilitatea de a crea de la zero elemente al căror comportament să-l construiești după bunul plac sau poți modifica elementele HTML existente pentru a le oferi un nou comportament și înfățișare.

Pentru a construi elementele specializate ai nevoie să definești elementul pe care îl instanțiezi folosind o clasă. Clasa trebuie neapărat să aibă în constructor `super()` ca prim pas.

```javascript
const nume_template = document.createElement('template');
nume_template = `
  <style>
    h3 {
      color: coral;
    }
  </style>
  <div class="componenta-noua">
    <img />
    <h3></h3>
  </div>
`;

customElements.define('nume-tag', class NumeTag extends HTMLElement {
  // pas 1
  constructor () {
    super(); // creează linia de moștenire de la HTMLElement
  }
  // pas 2
  this.attachShadow({mode: 'open'}); // creează `shadowRoot`

  // pas 3
  this.shadowRoot.innerHTML = `
    <style>
      :host {
        font-size: 24px;
      }
      ::sloted(*) {
        color: inherit;
      }
    </style>
    <div>
      <p>Ceva acolo <slot></slot></p>
      <alt-element></alt-element>
      <ul id="lista" class="hidden">
        <li>Demo</li>
      </ul>
      <button id="acesta"></button>
    </div>
  `;

  // pas 3 bis -> Introducerea unui template [aici doar pentru demo]
  this.shadowRoot.appendChild(nume_template.content.cloneNode(true));
  this.shadowRoot.querySelector('img').src = this.getAttribute('avatar');

  // adăugarea unui receptor pe evenimentele butonului
  this.selectat = this.shadowRoot.querySelector('#id');
  this.selected.addEventListener('click', () => {
    this.shadowRoot.querySelector('#lista').classList.remove('hidden');
  });
});
```

Apoi este necesar să fie atașat un shadow DOM care să *ambaleze*  întregul cod HTML intern al componentei pe care o creezi: `this.attachShadow({mode: 'open'})`. Această opțiune din obiectul pasat, `mode` este setată cu valoarea `open`, ceea ce înseamnă că interiorul componentei este acționabil folosind JavaScript. Metoda `attachShadow` creează un `shadowRoot`. În `shadowRoot` poți introduce direct cod HTML sau un template HTML așa cum este ilustrat în exemplu la pasul 3 bis.

Poți vedea `shadowRoot`-ul dacă selectezi elementul componentei: `document.querySelector('nume-componenta').shadowRoot`.

Odată având aceste două lucruri setate, `super()`, care face legătura cu, clasa mamă pe care o extindem și atașăm și un shadowRoot, putem introduce codul HTML dorit în `shadowRoot`. Aici putem introduce template-uri sau putem scrie direct HTML. Să presupunem că punem elementul în pagina HTML.

```html
<nume-tag mentiune="interesant" avatar="https://randomuser.me/api/portraits/men/1.jpg"></nume-tag>
```

Modelare vizuală cu CSS se poate face prin redactarea directivelor direct în codul HTML, dar poate fi folosită și o foaie de stil externă pe care să o încarci. În CSS sunt câteva pseudo-selectori specifici componentelor precum `:host` care selectează întreaga componentă.

Componentelor poți să le adaugi atribute ale căror valoare va fi disponibilă în codul intern. De exemplu, prin `this.attributes.nume_atribut.value` sau `this.getAttribute('numeatribut')`.

În cazul în care am dori să introducem conținut în interiorul componentei în momentul în care o declarăm în HTML, de fapt am introduce conținutul în `shadowRoot` și nu ar fi vizibil nimic.

```html
<nume-tag mentiune="interesant">
  (mergi la <a href="www.ceva.ro">ceva</a>)
</nume-tag>
```

Pentru a vedea conținutul pe care l-a *înghițit* shadow DOM-ul, vom folosi un element `<slot>` care *perforează* zidul protector pe care-l ridică shadow DOM-ul. Are comportamentul unui symlink între lightDOM și *shadowDOM*. Regula ar fi ca în cazul în care ai conținut în componentă atunci când este declarată în document, acolo unde dorești să fie afișat respectivul conținut, pui în codul componentei `<slot />`. Ca prin magie, conținutul va fi vizibil. Dacă dorești să pasezi date din conținutul introdus în componentă la momentul declarării în documentul HTML către elementul `<slot>` care va face vizibil conținutul, se va introduce un atribut `slot` a cărei valoare va putea fi accesată în slot. Să presupunem că avem următoarea componentă în document.

```html
<nume-tag mentiune="interesant" avatar="https://randomuser.me/api/portraits/men/1.jpg">
  <p slot="email">cineva@undeva.ro</p>
  <p slot="adresa">Undeva, nr 12</p>
</nume-tag>
```

În codul HTML al template-ului sau a valorii `this.shadowRoot.innerHTML` vom avea următoarea configurare pentru `slot`.

```javascript
const nume_template = document.createElement('template');
nume_template = `
  <style>
    :host {
      font-size: 24px;
    }
    ::sloted(*) {
      color: inherit;
    }
    h3 {
      color: coral;
    }
  </style>
  <div class="componenta-noua">
    <img />
    <h3></h3>
    <p><slot name="email"/></p>
    <p><slot name="adresa"/></p>
  </div>
`;
customElements.define('nume-tag', class NumeTag extends HTMLElement {
  // pas 1
  constructor () {
    super(); // creează linia de moștenire de la HTMLElement
  }
  // pas 2
  this.attachShadow({mode: 'open'}); // creează `shadowRoot`

  // pas 3
  this.shadowRoot.appendChild(nume_template.content.cloneNode(true)); // introduci template-ul aici
  this.shadowRoot.querySelector('img').src = this.getAttribute('avatar');
});
```

În acest caz, pentru a aplica stilizare pe codul din slot, trebuie ca în CSS-ul componentei să folosim un pseudo-selector numit `::sloted()`. Acum, în interior trebuie menționat care elemente dorești să le modelezi. Pentru a afecta toate elementele, pasezi `*`: `::sloted(*) {}`. Dacă setăm proprietate `color: inherit`, shadowDOM-ul va permite preluarea culorii setate în lightDom pentru respectivele elemente.

În interiorul unor elemente specializate, poți introduce alte elemente specializate fără nicio problemă.

Pentru a adăuga receptori pe evenimente, se va selecta elementul.

## Elementele autonome de la zero

În cazul în care sunt construite astfel de elemente, este necesată extinderea clasei `HTMLElement`.

```javascript
class WordCount extends HTMLElement {
  constructor() {
    // Apelează mereu super în constructor
    super();

    // Creează un shadow root
    this.attachShadow({mode: 'open'}); // setează și returnează 'this.shadowRoot'

    // Creează câteva elemente span imbricate

    const wrapper = document.createElement('span'); // creezi un element rădăcină (portantul sub-arborelui)
    wrapper.setAttribute('class', 'wrapper');       // introduci primul atribut `class="wrapper"`

    const icon = wrapper.appendChild(document.createElement('span')); // introdu în wrapper un prim element span
    icon.setAttribute('class', 'icon'); // introduci primul atribut `class="icon"`
    icon.setAttribute('tabindex', 0);   // introduci al doilea atribut `tabindex="0"`

    // Inserează un icon la definirea atributului sau unul din oficiu
    const img = icon.appendChild(document.createElement('img')); // creezi al treilea element img pe care-l introduci
    img.src = this.hasAttribute('img') ? this.getAttribute('img') : 'img/default.png';
    /*
    SIMILAR CU
        var imgUrl;
        if(this.hasAttribute('img')) {
          imgUrl = this.getAttribute('img');
        } else {
          imgUrl = 'img/default.png';
        }
        var img = document.createElement('img');
        img.src = imgUrl;
    */

    const info = wrapper.appendChild(document.createElement('span')); // introdu în wrapper al doilea element span
    info.setAttribute('class', 'info'); // creează-i atributul `class="info"`
    info.textContent = this.getAttribute('data-text'); // Ia textul din atributul `data-text="ceva"` și pune-l drept conținutul text al lui info

    // Create some CSS to apply to the shadow dom
    const style = document.createElement('style');
    style.textContent = `
      .wrapper {
        position: relative;
      }
      .info {
        font-size: 0.8rem;
        width: 200px;
        display: inline-block;
        border: 1px solid black;
        padding: 10px;
        background: white;
        border-radius: 10px;
        opacity: 0;
        transition: 0.6s all;
        position: absolute;
        bottom: 20px;
        left: 10px;
        z-index: 3;
      }
      img {
        width: 1.2rem;
      }
      .icon:hover .info, .icon:focus .info {
        opacity: 1;
      }
    `;

    // Atașează elementele create la shadow DOM
    this.shadowRoot.append(style, wrapper);
  }
}
customElements.define('popup-info', PopUpInfo);
```

și apoi în HTML vom introduce elementul:

```html
<popup-info img="img/alt.png" data-text="Your card validation code (CVC)
  is an extra security feature — it is the last 3 or 4 numbers on the
  back of your card."></popup-info>
```

În exemplul de mai sus, avem elementul căruia i se aplică stilizarea CSS folosind un element `<style>`, dar acest lucru este posibil și prin referirea unui stylesheet extern accesat printr-un element `<link>`. Am putea avea următorul amendament al codului de exemplificare de mai sus.

```javascript
// Aplică stilizări externe la shadow dom
const linkElem = document.createElement('link');
linkElem.setAttribute('rel', 'stylesheet');
linkElem.setAttribute('href', 'style.css');

// Atașează elementul de legătură cu css-ul la shadow dom
shadow.appendChild(linkElem);
```

## Elemente HTML existente modificate

În cazul în care ai nevoie să particularizezi element HTML canonice, poți face acest lucru extinzând clasa lor specifică. Exemplul oferit de MDN este cel al unei liste de elemente neordonate a cărui element `<li>` este modificat astfel încât să colapseze.

```javascript
class ExpandingList extends HTMLUListElement {
  constructor() {
    // Always call super first in constructor
    // Return value from super() is a reference to this element
    self = super();

    // Get ul and li elements that are a child of this custom ul element
    // li elements can be containers if they have uls within them
    const uls = Array.from(self.querySelectorAll('ul'));
    const lis = Array.from(self.querySelectorAll('li'));

    // Hide all child uls
    // These lists will be shown when the user clicks a higher level container
    uls.forEach(ul => {
      ul.style.display = 'none';
    });

        // Look through each li element in the ul
    lis.forEach(li => {
      // If this li has a ul as a child, decorate it and add a click handler
      if (li.querySelectorAll('ul').length > 0) {
        // Add an attribute which can be used  by the style
        // to show an open or closed icon
        li.setAttribute('class', 'closed');

        // Wrap the li element's text in a new span element
        // so we can assign style and event handlers to the span
        const childText = li.childNodes[0];
        const newSpan = document.createElement('span');

        // Copy text from li to span, set cursor style
        newSpan.textContent = childText.textContent;
        newSpan.style.cursor = 'pointer';

        // Add click handler to this span
        newSpan.onclick = self.showul;

        // Add the span and remove the bare text node from the li
        childText.parentNode.insertBefore(newSpan, childText);
        childText.parentNode.removeChild(childText);
      }
    });
  }

  // li click handler
  showul = function (e) {
    // next sibling to the span should be the ul
    const nextul = e.target.nextElementSibling;

    // Toggle visible state and update class attribute on ul
    if (nextul.style.display == 'block') {
      nextul.style.display = 'none';
      nextul.parentNode.setAttribute('class', 'closed');
    } else {
      nextul.style.display = 'block';
      nextul.parentNode.setAttribute('class', 'open');
    }
  };
}

// Define the new element
customElements.define('expanding-list', ExpandingList, { extends: 'ul' });
```

Pagina HTML ar putea fi:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Expanding list web component</title>
    <style>
        ul {
            list-style-type: none;
        }

        li::before {
            display:inline-block;
            width: 1rem;
            height: 1rem;
            margin-right: 0.25rem;
            content:"";
        }

        .open::before, .closed::before {
            background-size: 1rem 1rem;
            position: relative;
            top: 0.25rem;
            opacity: 0.3;
        }

        .open::before {
            background-image: url(img/down.png);
        }

        .closed::before {
            background-image: url(img/right.png);
        }

        .closed .closed::before, .closed .open::before {
            display: none;
        }
    </style>
</head>
<body>
    <h1>Expanding list web component</h1>
    <ul is="expanding-list">
        <li>UK
            <ul>
                <li>Yorkshire
                    <ul>
                        <li>Leeds
                            <ul>
                                <li>Train station</li>
                                <li>Town hall</li>
                                <li>Headrow</li>
                            </ul>
                        </li>
                        <li>Bradford</li>
                        <li>Hull</li>
                    </ul>
                </li>
            </ul>
        </li>
        <li>USA
            <ul>
                <li>California
                    <ul>
                        <li>Los Angeles</li>
                        <li>San Francisco</li>
                        <li>Berkeley</li>
                    </ul>
                </li>
                <li>Nevada</li>
                <li>Oregon</li>
            </ul>
        </li>
    </ul>

    <ul>
        <li>Not</li>
        <li>an</li>
        <li>expanding</li>
        <li>list</li>
    </ul>

    <script src="main.js"></script>
</body>
</html>
```

Un alt exemplu pe care documentația de la `CustomElementRegistry.define()` ni-l oferă este cel al modificării unui paragraf.

```javascript
// Create a class for the element
class WordCount extends HTMLParagraphElement {
  constructor() {
    // Always call super first in constructor
    super();

    // count words in element's parent element
    var wcParent = this.parentNode;

    function countWords(node){
      var text = node.innerText || node.textContent
      return text.split(/\s+/g).length;
    }

    var count = 'Words: ' + countWords(wcParent);

    // Create a shadow root
    var shadow = this.attachShadow({mode: 'open'});

    // Create text node and add word count to it
    var text = document.createElement('span');
    text.textContent = count;

    // Append it to the shadow root
    shadow.appendChild(text);

    // Update count when element content changes
    setInterval(function() {
      var count = 'Words: ' + countWords(wcParent);
      text.textContent = count;
    }, 200)

  }
}

// Define the new element
customElements.define('word-count', WordCount, { extends: 'p' });
```

Acesta se inserează în DOM astfel: `<p is="word-count"></p>`.

## Callback-urile ciclului de viață al componentei

Aceste metode oferă posibilitatea de a adăuga interactivitate.

```javascript
customElements.define('nume-tag', class NumeTag extends HTMLElement {
  // pas 1
  constructor () {
    super(); // creează linia de moștenire de la HTMLElement
  }
  // pas 2'
  this.attachShadow({mode: 'open'}); // creează `shadowRoot`

  // pas 3
  this.shadowRoot.appendChild(nume_template.content.cloneNode(true)); // introduci template-ul aici

  // introdu datele pe care le iei din atributele componentei
  this.shadowRoot.querySelector('h3').innerText = this.getAttribute('nume');
  this.shadowRoot.querySelector('img').src = this.getAttribute('avatar');

  toggleInfo () {
    console.log('Este');
  }

  // introducerea receptorilor pe evenimente
  connectedCallback () {
    this.shadowRoot.querySelector('#toggle-info').addEventListener('click', () => {
      this.toggleInfo();
    });
  }

  // eliminarea receptorilor de pe evenimente
  disconnectedCallback () {
    this.shadowRoot.querySelector('#toggle-info').removeEventListener();
  }
});
```

### `connectedCallback()`

Acest callback este invocat de fiecare dată când elementul specializat este introdus (*appended*) într-un element al documentului la care se conectează. Se va mai executa ori de câte ori nodul va fi mutat. Altfel spus, ori de câte ori se încarcă elementul nostru specializat/componenta, tot codul din acest callback va fi executat. Aici este locul în care, de exemplu poți seta toate receptoarele pentru evenimentele elementelor din componentă.

Este posibil ca execuția să se întâmple înainte ca întregul conținut să fie parsat. În cazul în care se întâmplă să fie apelat când elementul nu mai este conectat, folosești pentru test `Node.isConnected()` pentru a te asigura.

### `disconnectedCallback`

Acest callback este invocat de fiecare dată când un element specializat este deconectat de la DOM. Este locul în care ar trebui șterse funcțiile cu rol de receptor în cazul în care au fost setate în callback-ul `connectedCallback()`.

### `adoptedCallback`

Acest callback este invocat de fiecare dată când un element specializat este mutat în alt document.

### `attributeChangedCallback`

Acest callback este invocat de fiecare dată când unui element specializat i se adaugă câte un atribut, când i se șterge unul sau când este modificat. Atributele pentru care se face observarea sunt menționate prin metoda statică `get observedAttributes`.

### Exemplul MDN

Documentația MDN oferă un exemplu pentru a înțelege.

```javascript
// Creează clasa elementului
class Square extends HTMLElement {
  // Specifici atributele observate pentru ca attributeChangedCallback să fie executat
  static get observedAttributes() {
    return ['c', 'l'];
  }

  constructor() {
    // Fă apelul necesar mereu
    super();

    // constituie shadow DOM-ul
    const shadow = this.attachShadow({mode: 'open'});

    // creează un div și un element style
    const div = document.createElement('div');
    const style = document.createElement('style');
    shadow.appendChild(style);
    shadow.appendChild(div);
  }

  connectedCallback() {
    console.log('A fost adăugat un element pătrat în pagină.'); // la introducere se declanșează
    updateStyle(this); // apelează un helper definit mai jos
  }

  disconnectedCallback() {
    console.log('Elementul pătrat a fost șters din pagină.');
  }

  adoptedCallback() {
    console.log('Elementul pătrat a fost mutat.');
  }

  attributeChangedCallback(name, oldValue, newValue) {
    console.log('Elementul pătrat și-a modificat atributele.');
    updateStyle(this);
  }
}

// definește elementele specializate
customElements.define('custom-square', Square);

/*
* Aceasta este o funcție helper apelată la momentul inserției în DOM-ul paginii și la modificarea atributelor
* @param {*} elem este chiar obiectul elementului creat
*/
function updateStyle (elem) {
  const shadow = elem.shadowRoot; // faci o referință la shadow root-ul elementului

  // selectezi elementul style căruia îi modifici conținutul
  shadow.querySelector('style').textContent = `
    div {
      width: ${elem.getAttribute('l')}px;
      height: ${elem.getAttribute('l')}px;
      background-color: ${elem.getAttribute('c')};
    }
  `;
}

// faci referințe către butoanele care acționează callback-urile
const add = document.querySelector('.add');
const update = document.querySelector('.update');
const remove = document.querySelector('.remove');

// referință către elementul pătrat
let square;

// pornești cu butoanele `update` și `remove` dezactivate din start
update.disabled = true;
remove.disabled = true;


/**
 * random - helper de randomizare
 *
 * @param  {Number} min description
 * @param  {Number} max description
 * @return {Number}     description
 */
function random (min, max) {
  return Math.floor(Math.random() * (max - min + 1) + min);
}


/**
 * anonymous function - Handler onclick pentru butonul `.add`
 *
 * @return {type}  description
 */
add.onclick = function () {
  // Creează elementul specializat pătrat
  square = document.createElement('custom-square');
  square.setAttribute('l', '100');
  square.setAttribute('c', 'red');
  document.body.appendChild(square);

  update.disabled = false;
  remove.disabled = false;
  add.disabled = true;
};

update.onclick = function() {
  // Actualizează random valorile atributelor
  square.setAttribute('l', random(50, 200));
  square.setAttribute('c', `rgb(${random(0, 255)}, ${random(0, 255)}, ${random(0, 255)})`);
};

remove.onclick = function() {
  // Remove the square
  document.body.removeChild(square);

  update.disabled = true;
  remove.disabled = true;
  add.disabled = false;
};
```

Exemplul se folosește de următorul document.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Life cycle callbacks test</title>
    <style>
      custom-square {
        margin: 20px;
      }
    </style>
    <script defer src="main.js"></script>
  </head>
  <body>
    <h1>Life cycle callbacks test</h1>

    <div>
      <button class="add">Add custom-square to DOM</button>
      <button class="update">Update attributes</button>
      <button class="remove">Remove custom-square from DOM</button>
    </div>

  </body>
</html>
```

## Starea anumitor elemente

Starea anumitor elemente poate fi controlată prin pseudo-elementul `:state()` - https://developer.mozilla.org/en-US/docs/Web/CSS/:state și https://developer.mozilla.org/en-US/docs/Web/API/ElementInternals/states.

```css
custom-element:state(foo) {
  /* Styles to apply when `custom-element` is in the `foo` state */
}
```

## Resurse

- [Webcomponents](https://www.webcomponents.org/);
- [Using custom elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements);
- [Web Components: It’s about Time | Erin Zimmer](https://www.youtube.com/watch?v=zZ1YMJydqR0);
- [Using the lifecycle callbacks | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements#using_the_lifecycle_callbacks);
- [Custom Elements Everywhere](https://custom-elements-everywhere.com/);
- [::part and ::theme, an ::explainer](https://meowni.ca/posts/part-theme-explainer/)
- [The Gold Standard Checklist for Web Components | github](https://github.com/webcomponents/gold-standard/wiki)
- [WebComponents.org](https://webcomponents.github.io/)
