## Calcularea poziției mouse-ului relativ la un element

```javascript
ele.addEventListener('mousedown', function (e) {
    // Obține target-ul
    const target = e.target;

    // Obține bounding rectangle target-ului
    const rect = target.getBoundingClientRect();

    // Poziția mouse-ului este:
    const x = e.clientX - rect.left;
    const y = e.clientY - rect.top;
});
```
