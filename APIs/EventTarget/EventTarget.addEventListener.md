# EventTarget.addEventListener()

Este o metodă căreia îi poți pasa o funcție sau un obiect care implementează care implementează `EventTarget` în lista event listener-ilor pentru tipul de eveniment specificat.

## Semnătura

```text
target.addEventListener(type, listener [, options]);
target.addEventListener(type, listener [, useCapture]);
```

Atunci când pasezi drept al treilea paramentru o valoare `Boolean`, indici opțiunea pentru modul în care se va face propagarea evenimentului (*bubbling* sau *capture*). Acel al treilea parametru se numește *useCapture*. Dacă are valoarea `true`, *listener*-ul va fi executat doar la faza de capture. Valoarea din oficiu este `false`, ceea ce înseamnă că evenimentul va face *bubbling*.

În acest moment, cel mai bine ar fi să fie pasat un obiect drept al treilea parametru în care să fie menționate opțiunile.

```javascript
document.querySelector('body p').addEventListener('click', functie, {
  capture: false,
  once: false,
  passive: false
});
```

## Parametrii

### `type`

Este un string case-sensitive care numește tipul de eveniment pentru care se definește un receptor (*listener*).

### `listener`

Este un obiect care primește o notificare. Acest obiect implementează interfața `EventListener` sau poate fi o funcție JavaScript.

### `options`

Acest parametru este opțional și este un obiect. Membrii acestui obiect sunt `capture`, `once` și `passive`. Toate acestea au valori `Boolean`.

#### `capture`

Indică faptul că pentru evenimentul specificat, se va trimite către *listener*-ul întregistrat. Dacă are valoarea `true`, listener-ul va fi declanșat în momentul în care este acționat părintele. Dacă are valoarea `false`, evenimentul va face *bubbling*.

#### `once`

Dacă are valoarea `true`, evenimentul va declașa execuția pentru o singură dată a funcției cu rol de *listener*.

#### `passive`

Dacă are valoarea `true` indică faptul că funcția cu rol de *listener* nu va apela `preventDefault()` chiar dacă aceasta este activată în listener (`ev.preventDefault()`). În această configurare, va fi emis un avertisment în consolă.

## Resurse

- [Fine Tune your Touch Events with Passive mode | Steve Griffith | YouTube](https://www.youtube.com/watch?v=J06Uz7m-Jn8)
- [EventTarget.addEventListener() | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events)
- [JavaScript Event Bubbling and Propagation | Steve Griffith | YouTube](https://www.youtube.com/watch?v=JYc7gr9Ehl0)
