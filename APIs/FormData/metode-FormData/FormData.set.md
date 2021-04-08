# FormData.set()

Această metodă setează o valoare nouă pentru o cheie existentă dintr-un obiect `FormData`. Dacă există deja cheia, valoarea este suprascrisă.

```javascript
formData.set(name, value);
formData.set(name, value, filename);
```

## Parametrii

### name

Este numele câmpului în care este valoarea.

### value

Este valoarea câmpului. Această valoare poate fi un `USVString` sau `Blob`, fiind incluse subclase așa cum este `File`. Dacă niciuna dintre aceste valori nu este folosită, valoarea este convertită la string.

### filename

Acest parametru este opțional și este numele fișierului sub formă de `USVString`. Acesta reprezintă denumirea care reprezintă un `Blob` sau un `File` al cărui identificator este pasat în al doilea parametru. În cazul în care este atașat un `Blob` unui obiect `FormData`, numele raportat serverului prin headerul "Content-Disposition" variază conform detaliilor specifice fiecărui browser.

### Lucrul cu fișiere

```javascript
formData.set('nume', 'Otilia');
formData.set('avatar', myFileInput.files[0], 'otilia.jpg');
```

### Lucru cu șiruri de caractere

Dacă valoarea trimisă într-un `FormData` este alta decât un `String` sau un `Blob`, acestea vor fi transformate în `String`.

```javascript
formData.set('nume', 12);
formData.get('nume'); // "12"
```
