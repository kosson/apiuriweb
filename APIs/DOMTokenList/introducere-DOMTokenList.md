# Introducere DOMTokenList

Această interfață oferă accesul la un set de entități separate prin spațiu. Este rezultatul aplicării următoarelor:

- `Element.classList`,
- `HTMLLinkElement.relList`,
- `HTMLAnchorElement.relList`,
- `HTMLAreaElement.relList`,
- `HTMLIframeElement.sandbox`,
- `HTMLOutputElement.htmlFor`.

Acest set este unul indexat similar unui array JavaScript.

## Proprietăți

`DOMTokenList` oferă două proprietăți utile: `length` și `value`.

### `DOMTokenList.length`

Este un număr întreg care indică câte obiecte sunt stocate în `DOMTokenList`.

### `DOMTokenList.value`

Această proprietate returnează valoarea unui `DOMTokenList` ca șir de text `DOMString`.

## Metode

### `DOMTokenList.item(index)`

Parametrul pe care îl pasezi metodei reprezintă indexul elementului pe care dorești să-l returnezi. În cazul în care numărul pasat este mai mare decât dimensiunea array-ului, metoda returnează `null`. Metoda returnează un `DOMString` care este valoarea de la indexul specificat.

### `DOMTokenList.contains(token)`

Metoda returnează un `Boolean` cu valaorea `true`, dacă `token`-ul este găsit în listă, `false` în caz contrar.

Pentru un element dat

```html
<span class="a b c"></span>
```

putem investiga

```javascript
let span = document.querySelector("span");
let classes = span.classList;
let result = classes.contains("c");
if (result) {
  span.textContent = "În classList există 'c'";
} else {
   span.textContent = "classList nu-l are pe 'c'";
}
```

### `DOMTokenList.add(token1[, token2[, ...tokenN]])`

Folosind metoda, poți adăuga `token`-ul la lista existentă. Metoda returnează `undefined`.

Pentru un element dat

```html
<span class="a b c"></span>
```

putem introduce un token (clasă) nou

```javascript
let span = document.querySelector("span");
let classes = span.classList;
classes.add("d");
span.textContent = classes; // a b c d
// poți adăuga mai multe clase deodată
span.classList.add("e", "f");
```

### `DOMTokenList.remove(token1[, token2[, ...tokenN]])`

Metoda este folosită pentru a elimina un `token` din lista claselor. Dacă șirul de caractere care reprezintă numele clasei nu se află în listă, nu se întâmplă nimic și nu apare vreo eroare.
În caz că este nevoie poți șterge mai multe clase deodată.

```javascript
classes.remove("c", "b");
```

### `DOMTokenList.replace(oldToken, newToken)`

Metoda va înlocui numele unei clase existente cu un alt string care este introdus drept al doilea parametru. Dacă primul parametru nu există, metoda va returna `false`, fără a adăuga noua clasă în listă. Dacă înlocuirea a fost efectuată, metoda returnează valoarea `true`.

### `DOMTokenList.supports(token)`

Metoda este experimentală deocamdată. Este folosită pentru a investiga dacă `token`-ul care indică o anumită tehnologie are suport pe elementul curent. Returnează o valoare Boolean.

```javascript
let iframe = document.getElementById('display');

if (iframe.sandbox.supports('an-upcoming-feature')) {
  // codul care va fi rulat în cazul în care este suport pentru un anumit feature
} else {
  // fallback code
}

if (iframe.sandbox.supports('allow-scripts')) {
  // instruct frame to run JavaScript
  //
  // (NOTE: This feature is well-supported; this is just an example!)
  //
}
```

### `DOMTokenList.toggle(token [, force])`

Această metodă elimină un anumit token din `DOMTokenList` și returnează `false`. În cazul în care `token`-ul nu există în listă, acesta va fi adăugat și metoda va returna valoarea `true`.
Cel de-al doilea parametru este în Boolean care va face ca toogle-ul să funcționeze într-un singur sens. Dacă are valoarea `true`, atunci, token-ul va fi adăugat, dar nu va mai fi șters.

```javascript
let span = document.querySelector("span");
let classes = span.classList;

span.addEventListener('click', function() {
  let result = classes.toggle("c");

  if (result) {
    span.textContent = `'c' adăugat; classList are acum valorile: "${classes}".`;
  } else {
    span.textContent = `'c' eliminat; classList are acum valorile: "${classes}".`;
  }
})
```

### `DOMTokenList.entries()`

Această metodă returnează un iterator care permite parcurgerea cuplurilor cheie/valaore care sunt în obiectul `DOMTokenList`. Valorile sunt `DOMString`-uri fiecare reprezentând un singur token.

```javascript
let span = document.querySelector("span");
let classes = span.classList;
let iterator = classes.entries();

for (let value of iterator) {
  span.textContent += value + ' # ';
}
```

### `DOMTokenList.forEach(callback [, thisArg])`

Metoda permite aplicarea unui callback pentru fiecare pereche cheie/valoare în ordinea în care a fost făcută inserția claselor.
Funcția callback poate avea următorii parametri:

- `currentValue` - elementul procesat din array,
- `currentIndex` - indexul elementului curent procesat,
- `listObj` - array-ul pe care se aplică callback-ul (întregul array).

Callback-ul poate primi și un al doilea argument, referința către obiectul la care se va face legătura `this`.

Metoda returnează `undefined`.

```javascript
let span = document.querySelector("span");
let classes = span.classList;
let iterator = classes.values();

classes.forEach(
  function(value, key, listObj) {
    span.textContent += `${value} ${key}/${this}  ++  `;
  },
  "arg"
);
```

### `DOMTokenList.keys()`

Metoda returnează un iterator, care permite parcurgerea tuturor cheilor. Cheile sunt `unsigned integer`.

```javascript
var span = document.querySelector("span");
var classes = span.classList;
var iterator = classes.keys();

for(var value of iterator) {
  span.textContent += value + ' ++ ';
}
```

### `DOMTokenList.values()`

Metoda permite parcurgerea valorilor unui obiect `DOMTokenList`. Fiecare valoare este un obiect `DOMString`.

```javascript
var span = document.querySelector("span");
var classes = span.classList;
var iterator = classes.values();

for(var value of iterator) {
  span.textContent += value + ' ++ ';
}
```


## Resurse

- [7.1. Interface DOMTokenList | DOM Living Standard, 10 sept. 2020](https://dom.spec.whatwg.org/#interface-domtokenlist)
- [DOMTokenList | MDN](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList)
