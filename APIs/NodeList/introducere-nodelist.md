# Introducere NodeList

Un `NodeList` este un obiect care conține nodurile copil ale unui nod. Acest obiect nu este un array și se constituie care rezultat returnat de

- `Node.childNodes` (colecție live) sau
- `document.querySelectorAll()` (colecție statică).

Chiar dacă acest obiect nu este un array, poate fi iterat folosind `forEach()`. În cazul în care se dorește convertirea la un array, acest lucru este posibil folosind metoda obiectului intern `Array.from()`.

## Live și static

Există două posibilități pentru obiectele `NodeList`. Unele pot fi live, iar altele statice.

Live înseamnă că acea colecție de noduri va fi actualizată ori de câte ori DOM-ul este actualizat.

## Proprietăți

### `NodeList.length`

Returnează numărul de noduri din colecție.

## Metode

### `NodeList.item()`

Metoda returnează nodul de la un anumit index din colecție. Dacă indexul precizat, nu există, este returnat `null`.

```javascript
var paragrafe = document.getElementsByTagName("p");
paragrafe.item(0); // este nodul corespondent primului paragraf.
```

### `NodeList.entries()`

Metoda returnează un obiect iterator ce permite parcurgerea perechile cheie/valoare din obiectul colecției de noduri. Valorile sunt noduri.

```javascript
var parinte = document.getElementsByTagName('p');
var lista = parinte.childNodes;

for(var nod of lista.entries()) {
  console.log(nod);
}
```

### `NodeList.forEach()`

Metoda execută o funcție cu rol de callback pentru fiecare nod din `NodeList`. Fiecare nod este pasat drept argument funcției cu rol de callback.

Funcția cu rol de callback acceptă trei argumente:

- `currentValue`, fiind elementul procesat curent.
- `currentIndex` | opțional, fiind indexul elementului curent,
- `listObj` | opțional, fiind însuși obiectul pe care este aplicat `forEach()`.

Suplimentar funcției cu rol de callback, se mai poate menționa opțional un obiect la care să se stabilească legătura `this`.

### `NodeList.keys()`

Metoda returnează un iterator, care parcurge obiectul oferind cheile obiectului pornind de la valoarea 0.

### `NodeList.values()`

Metoda returnează un iterator, care parcurge obiectul oferind valorile obiectului (nodurile) pornind de la valoarea 0.
