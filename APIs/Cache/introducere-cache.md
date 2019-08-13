# Cache

Este un mecanism de stocare în baza unor obiecte `Request` / `Response` care sunt introduse într-o zonă tampon a browserului. Obiectele request pot fi percepute drept cheile din obiectul cache creat.

Acest mecanism joacă un rol central în lucrul cu `ServiceWorker`-ii, dar trebuie reținut faptul că odată inițiat este disponibil atât serviceworker-ului, cât și browser-ului.

Elemetele care sunt introduse în cache, nu sunt actualizate decât atunci când se face asta înadins și nu sunt șterse decât dacă acest lucru este necesar.

Pentru a folosi `Cache`-ul, acesta trebuie deschis folosind metoda `open()`. Ceea ce se petrece este instanțierea unui obiect `CacheStorage`.

Mecanismul `Cache` folosește interfața `CacheStorage` care oferă o serie de metode necesare lucrului.
Interfața `CacheStorage` oferă și un director principal în care se găsesc cache-uri cu nume ce pot fi accesate de un `ServiceWorker` sau de programele JavaScript care lucrează în `window`.

Cache-urile pot fi gândite ca zone care poartă un nume în care se pot pune resurse necesare.
Atunci când instanțiezi un obiect `CacheStorage` cu metoda `open()`, trebuie să dai un nume acestui nou cache. Numele poate fi pasat metodei `open()` ca argument string.

## Metode

### Metoda `Cache.match(request, options)`

Metoda returnează o promisiune care rezolvă către un răspuns asociat cererii corespondente făcute obiectului `Cache`.

Primul arument pasat metodei (`request`) poate fi înțeles ca o veritabilă cheie pentru elementele existente în obiectul cache.

### Metoda `Cache.matchAll(request, options)`

Returnează o promisiune care rezolvă către un array de cereri către obiectul cache.

### Metoda `Cache.add(request)`

Metoda preia un URL, aduce resursele la care acesta trimite și adaugă respectivul obiect de răspuns cache-ul construit. Funcțional vorbind, este echivalent operațiunilor făcute cu `fetch()` combinat cu metoda `put()` pentru a adăuga rezultatele în cache.

### Metoda `Cache.addAll(requests)`

Metoda preia un array de URL-uri, aduce resursele și adaugă respectivul obiect de răspuns în cache.

### Metoda `Cache.put(request, response)`

Adaugă în cache deopotrivă obiectul request și response.

### Metoda `Cache.delete(request, options)`

Caută în obiectul cache o cheie reprezentată de request și returnează o promisiune care rezolvă la `true` dacă datele există și au fost șterse. Dacă nu au fost găsite date, atunci promisiunea va rezolva la `false`.

### Metoda `Cache.keys(request, options)`

Returnează o promisiune care rezolvă la un array de chei existente în obiectul cache.

## Referințe

- [CacheStorage, Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage)
- [Cache, Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
