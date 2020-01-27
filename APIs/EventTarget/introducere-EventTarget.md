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
var EventTarget = function() {
  this.listeners = {};
};

EventTarget.prototype.listeners = null;
EventTarget.prototype.addEventListener = function(type, callback) {
  if (!(type in this.listeners)) {
    this.listeners[type] = [];
  }
  this.listeners[type].push(callback);
};

EventTarget.prototype.removeEventListener = function(type, callback) {
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

EventTarget.prototype.dispatchEvent = function(event) {
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
