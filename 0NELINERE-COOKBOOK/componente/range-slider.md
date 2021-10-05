# Range slider

Mai întâi verifică dacă input-ul de tip range are suport în browser.

Elementul care creează un slider este un input `<input type="range" />`.

```javascript
const isRangeInputSupported = function () {
    const ele = document.createElement('input');
    ele.setAttribute('type', 'range');
    // Dacă browserul nu are suport, va fi transformat în tip text
    return ele.type !== 'text';
};
```

## Crearea unui slider particularizat

Structura HTML prezintă câteva `div`-uri care sunt în linie.

```html
<div class="container">
    <div class="left"></div>
    <div class="knob" id="knob"></div>
    <div class="right"></div>
</div>
```

Elementul din dreapta ia întregul spațiu (`width`).

```css
.container {
    align-items: center;
    display: flex;
    height: 1.5rem;
}
.right {
    /* Ia tot width-ul rămas */
    flex: 1;
    height: 2px;
}
```

### Evenimente

Faci `knob`-ul draggable.

```javascript
// Query the element
const knob = document.getElementById('knob');
const leftSide = knob.previousElementSibling;

// The current position of mouse
let x = 0;
let y = 0;
let leftWidth = 0;

// Handle the mousedown event
// that's triggered when user drags the knob
const mouseDownHandler = function (e) {
    // Get the current mouse position
    x = e.clientX;
    y = e.clientY;
    leftWidth = leftSide.getBoundingClientRect().width;

    // Attach the listeners to `document`
    document.addEventListener('mousemove', mouseMoveHandler);
    document.addEventListener('mouseup', mouseUpHandler);
};
```

Când se mișcă `knob`-ul în baza poziției curent și cea de origine a mouse-ului, vom ști cât de departe s-a mutat mouse-ul. În acel moment, se va seta dimensiune `width` din partea stângă.

```javascript
const mouseMoveHandler = function (e) {
    // How far the mouse has been moved
    const dx = e.clientX - x;
    const dy = e.clientY - y;

    const containerWidth = knob.parentNode.getBoundingClientRect().width;
    let newLeftWidth = ((leftWidth + dx) * 100) / containerWidth;
    newLeftWidth = Math.max(newLeftWidth, 0);
    newLeftWidth = Math.min(newLeftWidth, 100);

    leftSide.style.width = `${newLeftWidth}%`;
};
```

Curăță evenimentele

```javascript
// Triggered when user drops the knob
const mouseUpHandler = function() {
    ...

    // Remove the handlers of `mousemove` and `mouseup`
    document.removeEventListener('mousemove', mouseMoveHandler);
    document.removeEventListener('mouseup', mouseUpHandler);
};
```

## Resurse

- [Create a range slider](https://htmldom.dev/create-a-range-slider/)
