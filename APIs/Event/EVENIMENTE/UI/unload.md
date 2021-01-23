# Evenimentul unload

Acest eveniment este declanșat atunci când se navighează de la o pagină la alta. Este folosit pentru a ne asigura că nu mai există referințe către obiecte care ar putea să conducă la scurgeri de memorie. Precum în cazul evenimentului `load`, `unload` este aplicat lui `window`.

```javascript
window.addEventListener("unload", (event) => {
  console.log('Am plecat!');
})
```

Obiectul `event` nu conține decât proprietatea `target`.
