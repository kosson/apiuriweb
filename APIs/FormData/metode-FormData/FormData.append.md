# FormData.append()

Metoda introduce o nouă valoare unei chei existente din obiectul `FormData` sau adaugă cheia dacă aceasta nu există deja. Diferența dintre `FormData.set()` și `append` este aceea legată de comportamentul în cazul existenței unei chei. În cazul folosirii lui `set`, acesta va suprascrie valorile existente cu cea nouă. În cazul utilizării lui `append`, această metodă, va adauga noua valoare la finalul celor existente.

## Parametrii

### name

Este numele câmpului în care este valoarea.

### value

Este valoarea câmpului. Această valoare poate fi un `USVString` sau `Blob`, fiind incluse subclase așa cum este `File`. Dacă niciuna dintre aceste valori nu este folosită, valoarea este convertită la string.

### filename

Acest parametru este opțional și este numele fișierului sub formă de `USVString`. Acesta reprezintă denumirea care reprezintă un `Blob` sau un `File` al cărui identificator este pasat în al doilea parametru. În cazul în care este atașat un `Blob` unui obiect `FormData`, numele raportat serverului prin headerul "Content-Disposition" variază conform detaliilor specifice fiecărui browser.

## Lucrul cu metoda append

### Lucrul cu fișiere

```javascript
formData.append('nume', 'Otilia');
formData.append('avatar', myFileInput.files[0], 'otilia.jpg');
```

Poți adăuga mai multe valori unui singur `name` dacă folosești o convenție precum în următorul exemplu.

```javascript
formData.append('avatar[]', myFileInput.files[0], 'otilia1.jpg');
formData.append('avatar[]', myFileInput.files[1], 'otilia2.jpg');
```

Acest artificiu permite procesarea mai multor fișiere pentru că structura de date rezultată poate fi parcursă folosind o buclă.

### Lucru cu șiruri de caractere

Dacă valoarea trimisă într-un `FormData` este alta decât un `String` sau un `Blob`, acestea vor fi transformate în `String`.

```javascript
formData.append('nume', false);
formData.append('nume', 12);
formData.append('nume', 'Otilia');

formData.getAll('nume'); // ["false", "12", "Otilia"]
```
