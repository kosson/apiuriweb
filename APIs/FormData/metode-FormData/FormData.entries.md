# FormData.entries()

Metoda Returnează un iterator care permite parcurgerea chei/valorilor. Cheile sunt de tip `USVString`, valorile fiind ori `USVString`, ori `Blob`.

```javascript
// Creează un obiect FormData
var formData = new FormData();
formData.append('cheia1', 'valoarea1');
formData.append('cheia2', 'valoarea2');

// afișarea chei/valorilor
let pereche;
for(pereche of formData.entries()) {
   console.log(pereche[0]+ ', '+ pereche[1]);
}
