## Toate elementele sibling

```javascript
const siblings = (ele) => [].slice.call(ele.parentNode.children).filter((child) => child !== ele);
```

## Verifică dacă elementul există conform unui selector CSS

```javascript
const matches = function (ele, selector) {
    return (
        ele.matches ||
        ele.matchesSelector ||
        ele.msMatchesSelector ||
        ele.mozMatchesSelector ||
        ele.webkitMatchesSelector ||
        ele.oMatchesSelector
    ).call(ele, selector);
};
```

## Caută cel mai apropiat element

```javascript
const result = ele.closest(selector);
```

Metoda `closest` nu are suport în IE.

## Fă o traversare a arborelui până când găsești elementul

```javascript
const matches = function (ele, selector) {
    return (
        ele.matches ||
        ele.matchesSelector ||
        ele.msMatchesSelector ||
        ele.mozMatchesSelector ||
        ele.webkitMatchesSelector ||
        ele.oMatchesSelector
    ).call(ele, selector);
};

// Găsește cel mai apropiat element debug `ele` găsit conform `selector`
const closest = function (ele, selector) {
    let e = ele;
    while (e) {
        if (matches(e, selector)) {
            break;
        }
        e = e.parentNode;
    }
    return e;
};
```
