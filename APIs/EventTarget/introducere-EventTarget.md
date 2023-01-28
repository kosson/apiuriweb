# EventTarget

`EventTarget` este o interfață DOM care este implementată de obiectele care pot primi evenimente și pot atașa funcții cu rol de receptori (*listeners*) pentru acestea.

![](img/EventTarget-Node.png)

`Element`. `Document` și `Window` sunt cele mai întâlnite ținte ale evenimentelor.

## Constructorul `EventTarget()`

Acest constructor creează o nouă instanță a unui obiect `EventTarget`. Mai pot avea evenimente și `XMLHttpRequest`, `AudioNode` și `AudioContext`.

Multe ținte ale unui eveniment, permit setarea unor *event handlers* via proprietăți on*numeeveniment*.

## Metode

### `EventTarget.addEventListener()`

Atașează (*registers*) o funcție cu rol de receptor (*listener*) pentru un anumit tip de eveniment -`EventTarget`.

### `EventTarget.removeEventListener()`

Șterge un eveniment de pe un element.

### `EventTarget.dispatchEvent()`

Trimite un eveniment către un `EventTarget`.

## Exemplu de implementare de la zero

```javascript
var EventTarget = function () {
  this.listeners = {};
};

EventTarget.prototype.listeners = null;
EventTarget.prototype.addEventListener = function (type, callback) {
  if (!(type in this.listeners)) {
    this.listeners[type] = [];
  }
  this.listeners[type].push(callback);
};

EventTarget.prototype.removeEventListener = function (type, callback) {
  if (!(type in this.listeners)) {
    return;
  }
  var stack = this.listeners[type];
  for (var i = 0, l = stack.length; i < l; i++) {
    if (stack[i] === callback){
      stack.splice(i, 1);
      return;
    }
  }
};

EventTarget.prototype.dispatchEvent = function (event) {
  if (!(event.type in this.listeners)) {
    return true;
  }
  var stack = this.listeners[event.type].slice();

  for (var i = 0, l = stack.length; i < l; i++) {
    stack[i].call(this, event);
  }
  return !event.defaultPrevented;
};
```

## Practică

Cel mai des țintite de evenimente sunt: `Element`, `document`, `window` dar și alte API-uri precum `XMLHttpRequest`.

Evenimentele țintesc obiecte pentru a semnala că ceva s-a întâmplat, precum activitate nouă pe rețea sau o interacțiune din partea utilizatorului. Aceste obiecte implementează interfața `EventTarget`. Evenimentele la rândul lor sunt obiecte care implementează interfața `Event`. Să explorăm cazul în care am dori să tratăm în toate amănuntele un eveniment.

```javascript
// creăm o funcție cu rol de callback
function onClick (eveniment) {
  console.log('onClick', 'Tocmai a fost dat un clic');
};

// țintim un nod DOM pentru care dorim să ascultăm evenimentele
var button = document.querySelector('button');

// si atașăm răspunsul nostru la posibilul eveniment
button.addEventListener('click', onClick);

// Interfața EventTarget permite emiterea de evenimente
button.dispachEvent(new Event('click'));
```

Cel mai adesea vei vedea în cod evenimentele sub forma exemplul de mai jos:

```javascript
obiect.addEventListener("aparDate", function (date) { /*prelucrează date */ });
```

Pentru a crea un eveniment folosești metoda `dispatchEvent()`. Pentru asta, mai întâi creezi un eveniment, care este un obiect, ține minte și apoi îl *expediezi* (în engleză i se spune `dispatch`).

```javascript
var evenimentSpecial = new EvenimentSpecial("urlet", {"animal": "gorilă"});
obiect.dispatchEvent(evenimentSpecial);
```

Atunci când obiectelor DOM li se trimit evenimente, acel eveniment poate să ajungă și la *receptorii* (*listeners*) obiectelor părinte ale respectivului element pentru care este obiectul DOM țintit. Toți receptorii din părinți ai căror variabilă `capture` este setată la `true`, vor fi invocați în ordinea ierarhiei părinților. Atenție, dacă atributul `bubbles` al evenimentului rămâne la valoarea `true`, receptorii părinților vor fi invocați din nou, dar în acest caz în ordine inversă.

## Debouncing

Aceasta este operațiunea care apare ca necesitate atunci când frecvența evenimentelor este foarte mare. De exemplu, mișcarea mouse-ului pe ecran sau navigarea în sus sau în jos prin pagină (*scroll*). Gândește-te ce-ar însemna să răspunzi la toate aceste sute de evenimente. În practică, le vei ignora și vei răspunde doar la pozițiile finale în care ajunge o anumită acțiune a utilizatorului cum ar fi ultimele coordonatele ale mouse-ului la momentul în care s-a oprit. Această operațiune se numește **debouncing** și înseamnă că dintr-o succesiune de evenimente care se petrec într-o perioadă foarte scurtă de timp, doar ultimele vor fi luate în considerare.

## Lucrul cu resurse la distanță

Pentru a face apeluri care să aducă date din backend, vom folosit tot această interfață pentru că este nevoie să setăm *receptori* (*listeners*) pentru a fi avertizați atunci când resursele au venit.

```javascript
// declararea unei funcții de prelucrare a răspunsului primit
function onDate (eveniment) {
  console.log('raspuns', JSON.parse(this.responseText));
};
// În caz de eroare
function onError () {
  console.error('retea', this.statusText ||  'eroare ciudată');
};
// cazul în care anulezi apelul
function onAbandon () {
  console.warn('abandonez');
};
// construiește AJAX-ul
var cerere = new XMLHttpRequest();

// Foloseste interfata EventTarget pentru a atașa evenimente
// ascultând după fiecare dintre ele
cerere.addEventListener('raspuns', onDate);
cerere.addEventListener('eroare', onError);
cerere.addEventListener('anulez', onAbandon);

// Trimite o cerere pentru date.json
cerere.open('get', 'date.json');
cerere.send();
```

O astfel de cerere este una asincronă pentru că nu cunoaștem cu exactitate când vom avea răspunsul.

## Resurse

- [2.7. Interface EventTarget | DOM Living Standard](https://dom.spec.whatwg.org/#callbackdef-eventlistener)
- [Creating and triggering events | MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/Events/Creating_and_triggering_events)
- [2.1. Introduction to "DOM Events](https://dom.spec.whatwg.org/#introduction-to-dom-events)
