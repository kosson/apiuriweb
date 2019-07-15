# Headers

Este un constructor care crează obiecte `Headers`. De regulă, se folosește în cuplaj cu API-ul `Request`.

```javascript
var configurareHeadere = new Headers(init);
```

Parametrul `init` este un obiect care configurează headerele cererii.

Un model de lucru ar putea fi crearea unui obiect `Headers` gol, la care se vor adăuga membri folosind metoda `append()`.

```javascript
var configurareHeadere = new Headers(init);
configurareHeadere.append('Content-Type', 'image/jpeg');
configurareHeadere.get('Content-Type'); // image/jpeg
```

Poți predefini un obiect cu toate opțiunile, dacă este mai comod.

```javascript
var setariHeadere = {
  'Content-Type' :      'image/jpeg',
  'Accept-Charset':     'utf-8',
  'X-My-Custom-Header': 'Ceva de la mine'
};
var headereleMele = new Headers(setariHeadere);
```

## Referințe

- [Headers, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Headers/Headers)
