# Introducere CustomElementRegistry

Această interfață oferă metodele pentru evidența (*registering*) elementelor personalizate și pentru interogarea elementelor personalizate care deja există. Pentru a obține o instanță ai la îndemână proprietatea `window.customElements`. Folosind instanțe `CustomElementRegistry` poți introduce un element nou necanonic care să aibă un comportament specific.

Metode:

- `CustomElementRegistry.define()`: definești un nou element personalizat pentru a-l introduce în pagină;
- `CustomElementRegistry.get()`: returnează un constructor pentru noul element personalizat sau `undefined` dacă acesta nu există;
- `CustomElementRegistry.upgrade()`: upgradează un element personalizat în mod direct chiar înainte să fie conectat la shadow root;
- `CustomElementRegistry.whenDefined()`: returnează o promisiune goală care se rezolvă atunci când un element personalizat este definit folosind un anumit nume.

## Exemplu

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

## Resurse

- [Web Components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
