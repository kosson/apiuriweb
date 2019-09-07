# Request.cache

Este o proprietate read-only a interfeței `Request`. Această proprietate este o referință către modul în care se va constitui zona de date tampon - cache-ul și controlează cum va interacționa cererea cu `HTTP cache`-ul browserului.

```javascript
var modulCacheUluiCurent = request.cache;
```

Posibilele valori sunt:

- `default`,
- `no-store`,
- `reload`,
- `no-cache`,
- `force-cache`,
- `only-if-cached`.

## `default`

Comportamentul *din oficiu* - `default` este cel al browserului care se uită după un răspuns în cache-ul HTTP. În cazul în care este găsită o înregistrare `proaspătă`, aceasta va fi cea care va fi returnată din cache.

## Resurse

- [Freshness | HTTP caching , Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#Freshness)
