# FormData

Această interfață oferă posibilitatea de a constitui perechi cheie/valoare din câmpurile unui formular. În cazul în care datele formularului sunt trimise printr-o metodă POST, datele vor fi codate conform "multipart/form-data". Un obiect ce este o instanță `FormData` poate fi parcurs cu un `for...of`.

Constructorul este `FormData()` și instanțierea se face cu `new`, precum în exemplul dat.

```javascript
var formData = new FormData();
```

Să presupunem că avem un formular deja.

```html
<form id="descriere" name="descriere">
  <div>
    <label for="nume">Introdu nume:</label>
    <input type="text" id="nume" name="nume">
  </div>
  <div>
    <label for="fisier">Încarcă fișier:</label>
    <input type="file" id="fisier" name="fisier">
  </div>
  <input type="submit" value="Trimite">
</form>
```
Pentru a constitui obiectul `FormData`, va fi nevoie să pasăm o referință către elementul din DOM. Elementele care vor fi introduse în obiect vor fi doar cele care au un `name`, nu sunt `disabled` și cele care au fost bifate, având valoarea `checked` sau `selected`.

```javascript
let form = document.getElementById('descriere');
var dateFormular = new FormData(form);
```

Parametrul acceptat este un element HTML `<form>`. În urma execuției constructorului, ceea ce va rezulta este un obiect ale cărui chei sunt valorile proprietăților `name` ale elementelor formularului, iar valorile, cele introduse de utilizator.

Acest obiect se poate instanția gol și apoi completat folosind metoda `append()`.

```javascript
var dateFormular = new FormData();
dateFormular.append('Nume', 'Kosson');
```

## Referințe

- [FormData, javascript.info](https://javascript.info/formdata)
- [FormData, Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
- [Using FormData Objects | MDN](https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects)
