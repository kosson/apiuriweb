# Event delegation

Delegarea evenimentelor permite evitarea adăugării de receptori direct pe anumite noduri. În loc de a atașa direct pe nod, poți atașa pe un părinte. Acel eveniment atașat pe un părinte se uită la evenimentele din faza de *bubbling* pentru a descoperi elementul copil dorit în proprietatea `target` a obiectului eveniment.

```javascript
document.getElementById("parinte").addEventListener("click", (event) => {
  if (event.target && event.target.nodeName == "li") {
    // în cazul în care părintele este un ul, dacă un copil (`<li id="copil-1">`) a primit click
    console.log('A fost apăsat elementul cu numărul ', event.target.id.replace("copil-", ""));
  }
});
```

Poți folosi `Element.matches` pentru a atribui evenimentul chiar elementului dorit.

```javascript
document.getElementById("parinte").addEventListener("click", (event) => {
  if (event.target && event.target.matches("a.clasaLnk")) { // 'div.someSelector[some-attribute=true]'
    // în cazul în care părintele este un ul, dacă un copil (`<li id="copil-1">`) a primit click
    console.log('A fost apăsat elementul cu numărul ', event.target.id.replace("copil-", ""));
  }
});
```

În cazul în care vrei să filtrezi elementele care nu trebuie tratate, poți returna: `if(!event.target.matches('input')) return;`

Poți folosi și RegExp pentru testarea claselor.

```javascript
var re = new RegExp('\\b' + class + '\\b');
re.test(e.target.className);
// cand sunt mai multe spații între numele de clase
var classes = e.target.className.replace(/\s+/g," ");
```

Dacă browserul permite: `element.classList.contains(className)`.

```javascript
event.target && event.target.nodeName == "A" && event.target.classList.contains("myClass")
```
