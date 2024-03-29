# Obiectul event

În momentul în care se declanșează un eveniment, toate informațiile relevante sunt introduse într-un obiect numit generic `event`. Acest obiect este pasat ca unic argument al unei funcții cu rol de receptor. Cele mai multe evenimente sunt legate de obiectul `window` sau de controlul elementelor unui formular.

Obiectul `event` există câtă vreme se execută receptorii. Imediat după executarea acestora, obiectul `event` este distrus.

## Proprietăți

### `event.type`

Returnează care este tipul evenimentului care a declanșat apelul callback-ului. este foarte util atunci când dorești să setezi mai multe receptoare pe același element.

```javascript
let elem = document.getElementById("ceva");
let receptor = function(event) {
    switch(event.type) {
      case "click":
      console.log("Salutare!");
    break;
      case "mouseover":
      event.target.style.backgroundColor = "green";
    break;
      case "mouseout":
      event.target.style.backgroundColor = "";
    break;
  }
};
elem.onclick = receptor;
elem.onmouseover = receptor;
elem.onmouseout = receptor;
```

### `event.bubbles`

Este un Boolean care indică dacă se declanșează apelul receptorului la faza de bubbling.

### `event.cancelable`

Este un Boolean care indică dacă poate fi anulat comportamentul din oficiu pentru eveniment.

### `event.currentTarget`

Este o legătură către elementul căruia i s-a atașat evenimentul. Obiectul la care se face legătura `this` pentru funcția cu rol de receptor este chiar `currentTarget`.

### `event.defaultPrevented`

Este un Boolean care în cazul în care prezintă valoarea `true`, înseamnă că a fost apelat `preventDefault()`.

### `event.detail`

Este un număr intreg care aduce informații suplimentare necesare.

### `event.eventPhase`

Este un număr întreg care indică în care fază s-a declanșat evenimentul:

- 1 pentru capturing;
- 2 pentru at target;
- 3 pentru bubbling.

### `event.target`

Este elementul țintă care a declanșat evenimentul. A nu se confunda cu elementul care are handler-ul ce tratează evenimentul. Acela este accesibil folosind `currentTarget`. Acesta este strict elementul care a fost *țintit* de interacțiunea utilizatorului. Nu este obiectul la care se face legătura `this` a funcției cu rol de callback. Doar dacă *receptorul* este setat direct pe element (DOM 2), atunci, `this`, `currentTarget` și `target` indică același obiect.

```javascript
let element = document.getElementById("ceva");
element.onclick = function (event) {
  console.log(event.currentTarget === this); // true
  console.log(event.target === this); // true
};
```

În cazul în care receptorul ar fi setat pe un element părinte celui care a fost acționat, atunci `target` ar fi elementul acționat, nu cel care are atribuit receptorul.

```javascript
document.body.onclick = function (event) {
  console.log(event.currentTarget === document.body); // true
  console.log(this === document.body); // true
}
```

Este cazul în care apeși pe un element care nu are atașat propriul receptor.

### `event.trusted`

Aceasta este o valoare Boolean, care în cazul `true` indică faptul că elementul a fost creat de browser. În cazul `false` indică faptul că elementul a fost creat programatic (Javascript).

### `event.key`

În cazul elementelor care permit input de text, atunci când se apasă o tastă, proprietatea va returna caracterul asociat. Pentru tastele care nu sunt caractere, va fi returnată denumirea lor în clar: "Enter", "Shift", "Down".

### `event.char`

Această proprietate are același comportament precum al lui `event.key` cu specificația că pentru tastele care nu sunt caractere, va returna valoarea `null`.

## Metode

### `event.preventDefault()`

Metoda anulează comportamentul din oficiu al evenimentului. Poate fi utilizată doar dacă proprietatea `cancelable` are valoarea `true`.

### `event.stopImmediatePropagation()`

Este o metodă care întrerupe propagarea indiferent că este capturing sau bubbling. Anulează posibilitatea ca alți receptori să fie declanșați.

### `stopPropagation()`

Este o metodă care anulează propagarea evenimentului, fie că vorbim de capturing, fie de bubbling. Pentru a putea fi folosită, proprietatea `bubbling` trebuie să fie setată la `true`.

## Resurse

- [Can you target an elements parent element using event.target? | stackoverflow](https://stackoverflow.com/questions/29168719/can-you-target-an-elements-parent-element-using-event-target)