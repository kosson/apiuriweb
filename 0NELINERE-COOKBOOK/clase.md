## Adaugă o clasă unui element

```javascript
ele.classList.add('nume-clasa');

// Adăugarea de clase multiple nu este posibilă în IE 11
ele.classList.add('alte', 'nume', 'clase');
```

## Șterge o clasă pentru un anumit element

```javascript
ele.classList.remove('nume-clasa');

// Eliminarea de clase multiple nu este posibilă în IE 11
ele.classList.remove('alte', 'nume', 'clase');
```

## Toggle pentru o clasă

```javascript
ele.classList.toggle('nume-clasa');
```

## Verifică dacă un element are o anumită clasă

```javascript
ele.classList.contains('nume-clasa');
```

## Resurse

- [HTML DOM](https://htmldom.dev/)
