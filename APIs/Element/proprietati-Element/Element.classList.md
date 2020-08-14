## Element.classList

Returnează un `DOMTokenList` care conține o listă de atribute clasă.

Este o alternativă la accesarea claselor unui element sub formă de string în care numele claselor sunt delimitate prin spații, obținut prin `element.className`.

```javascript
const clase = elementNodeReference.classList;
```

Ceea ce se obține este un array cu numele tuturor claselor care au fost setate. Dacă elementul nu are nicio clasă, atunci dimensiunea array-ului returnat va fi `0`.

### Metode

#### `add( String [, String [, ...]] )`

Această metodă adaugă numele clasei specificat ca valoare string la cele existente deja. Dacă numele de clasă există deja, acțiunea metodei va fi ignorată.

#### `remove( String [, String [, ...]] )`

Elimină numele clasei specificată. Dacă aceasta nu există, nu va fi semnalată vreo eroare.

#### `item( Number )`

Returnează numele clasei de la indexul specificat.

#### `toggle( String [, force] )`

Atunci când metoda primește un singur argument, va seta clasa elementului la această valoare și va returna `true`. Dacă numele clasei deja există, va fi eliminată din listă și va returna `false`.

Dacă există și cel de-al doilea argument, iar acesta poate fi evaluat la `true`, atunci numele respectivei clase va fi adăugat. Dacă valorea celui de-al doilea arument este evaluată la `false`, numele clasei va fi eliminat.

#### `contains(String)`

Metoda verifică dacă numele de clasă care a fost primit ca argument există în lista claselor elementului.

#### `replace( oldClass, newClass `)

Metoda va înlocui numele unei clase existente cu numele menționat la al doilea argument.

## Referințe

- [Element.classList, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
