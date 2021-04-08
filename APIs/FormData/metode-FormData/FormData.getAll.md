# FormData.getAll()

Metoda returnează toate valorile asociate unei chei dintr-un obiect `FormData`. Numele cheii este un `USVString`.

```javascript
formData.getAll('nume_cheie');
```

Metoda returnează un array cu valori de tipul `FormDataEntryValue`. Aceste valori pot fi de tip string sau `File` reprezentând o singură valoare dintr-un set de perechi chei/valori a unui obiect `FormData`.
