# Element

Această interfață este clasa de bază din care toate obiectele ce reprezintă elemente dintr-un `Document` vor moșteni metode și proprietăți. Este un obiect al interfeței `Document`. Această interfață cuprinde metode și proprietăți comune tuturor elementelor din DOM.
Există alte interfețe care moștenesc metodele și proprietățile oferite de `Element`, dar care implementează seturi de funcționalități specifice.
De exemplu, interfața `HTMLElement` este baza tuturor elementelor HTML. Sau interfața `SVGElement`, care aduce suport pentru elementele SVG.

Moștenește din interfața părinte `Node` și prin extensie din interfața părinte a lui `Node` care este `EventTarget`.

Implementează proprietățile din `ParentNode`, `ChildNode`, `NonDocumentTypeChildNode` și `Animatable`.

Nodurile `Elements` sunt pur și simplu cunoscute sub denumirea de `elements`.
Elementele au asociate:

- un namespace
- un prefix de namespace și
- un nume local

Chiar dacă namespace-ul și prefixul pot să nu fie specificate, fiind în acest caz `null`, numele trebuie dat.
Elementele au și câte o listă de atribute care sunt ordonate. Dacă nu sunt întroduse atribute, lista acestora va fi goală.

## Proprietăți

### `Element.attributes`

### `Element.classList`

Aceasta este o proprietate read-only, care returnează o listă `DOMTokenList` live ce reprezintă clasele unui element.

### `Element.className`

### `Element.clientHeight`

### `Element.clientLeft`

### `Element.clientTop`

### `Element.clientWidth`

### `Element.computedName`

### `Element.computedRole`

### `Element.id`

### `Element.innerHTML`

### `Element.localName`

### `Element.namespaceURI`

### `NonDocumentTypeChildNode.nextElementSibling`

### `NonDocumentTypeChildNode.previousElementSibling`

### `Element.outerHTML`

### `Element.part`

### `Element.prefix`

### `Element.scrollHeight`

### `Element.scrollLeft`

### `Element.scrollTop`

### `Element.scrollWidth`

### `Element.shadowRoot`

### `Element.tagName`

## Metode

### `EventTarget.addEventListener()`

### `Element.attachShadow()`

### `EventTarget.dispatchEvent()`

### `Element.getAttribute()`

### `Element.getAttributeNames()`

### `Element.getAttributeNS()`

### `Element.getBoundingClientRect()`

### `Element.getClientRects()`

### `Element.getElementsByClassName()`

### `Element.getElementsByTagName()`

### `Element.getElementsByTagNameNS()`

### `Element.hasAttribute()`

### `Element.hasAttributeNS()`

### `Element.hasAttributes()`

### `Element.hasPointerCapture()`

### `Element.insertAdjacentElement()`

### `Element.insertAdjacentHTML()`

### `Element.insertAdjacentText()`

### `Element.querySelector()`

### `Element.querySelectorAll()`

### `Element.releasePointerCapture()`

### `Element.removeAttribute()`

### `Element.removeAttributeNS()`

### `EventTarget.removeEventListener()`

### `Element.scroll()`

### `Element.scrollBy()`

### `Element.scrollTo()`

### `Element.setAttribute(name, value)`

Metoda setează valoarea unui atribut al elementului specificat. Dacă atributul deja există, va fi actualizat. Pentur a obține valoarea unui atribut, se va folosi metoda `getAttribute()`, iar pentru a elimina un atribut se va folosi `removeAttribute()`.

Metoda returnează `undefined`.

### `Element.setAttributeNS()`

### `Element.setPointerCapture()`

### `Element.toggleAttribute()`

## Events

### `cancel`

### `error`

### `scroll`

### `select`

### `show`

### `wheel`

---

### Evenimente legate de clipboard

### `copy`

### `cut`

### `paste`

---

### Evenimente legate de composition

### `compositionend`

### `compositionstart`

### `compositionupdate`

---

### Evenimente specifice focalizării

### `blur`

### `focus`

### `focusin`

### `focusout`

---

### Evenimente fullscreen

### `fullscreenchange`

### `fullscreenerror`

---

### Evenimente de keyboard

### `keydown`

### `keypress`

### `keyup`

---

### Evenimente de mouse

### `auxclick`

### `click`

### `contextmenu`

### `dblclick`

### `mousedown`

### `mouseenter`

### `mouseleave`

### `mousemove`

### `mouseout`

### `mouseover`

### `mouseup`

### `webkitmouseforcechanged`

### `webkitmouseforcedown`

### `webkitmouseforcewillbegin`

### `webkitmouseforceup`

---

### Evenimente touch

### `touchcancel`

### `touchend`

### `touchmove`

### `touchstart`

## Event handlers

### `Element.onfullscreenchange`

### `Element.onfullscreenerror`

## Resurse

- [Element | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element)
- https://www.w3.org/TR/domcore/#concept-element
