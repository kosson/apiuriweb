# Evenimentul load

Este declanșat atunci când s-a încărcat complet `window` sau în cazul în care există un set de frame-uri, atunci când toate acestea s-au încărcat. Trebuie subliniat că este declanșat atunci când toate resursele s-au încărcat: JavaScript, CSS și imagini.

Același eveniment este declanșat atunci când o imagine s-a încărcat complet. La fel și pentru elementul `<object>`.

## Încărcarea window

Uneori ai nevoie să te asiguri că toate resursele ncesare afișării paginii s-au încărcat. Cel mai simplu mecanism este atașarea unui receptor pentru evenimentul `load`:

```javascript
window.addEventListener("load", function (event) {
  console.log('Totul s-a încărcat');
});
```

Obiectul la care trimit browserele accesând `event.target` este `document`, nu `window`. Conform DOM 2, evenimentul ar trebui să se declanșeze pe `document`, dar din motive de compatibilitate, browserele atașează evenimentul pe `window`.

## Încărcarea imaginilor

Folosind același eveniment, poți verifica încărcarea imaginilor.

```html
<img src="smile.gif" onload="console.log('Image loaded.')">
```

sau programatic folosind JavaScript:

```javascript
let imagine = document.getElementById("oImagine");
imagine.addEventListener("load", (event) => {
  console.log(event.target.src);
});
```
