# IndexedDB

Este un API din nivelul de bază care oferă posibilitatea de a stoca date structurate și chiar fișiere sau blob-uri. Natura acestui mecanism de stocare este una asincronă ceea ce îl face pretabil lucrului cu web worker-ii.

IndexedDB este o bază de date tranzacțională, dar spre deosebire de oricare alt RDBMS avem de-a face cu o bază de date care stochează datele folosind chei pe baza cărora se face indexarea.

IndexedDB are suport pentru un model tranzacțional dar nu este o bază de date relațională care are tabele ce reprezintă colecții de rânduri și coloane.

IndexedDB folosește obiecte `requests` care ascultă reușita sau eșecul unor evenimente DOM pentru că acest mecanism de stocare se folosește de evenimentele DOM pentru a semnala disponibilitatea unor rezultate. Aceste obiecte au proprietăți `onsuccess`, `onerror`, `readyState`, `result` și `errorCode`. Li se pot adăuga metode `addEventListener` sau `removeEventListener`. Proprietatea `result` este ceva care depinde foarte mult de modul în care s-a contituit obiectul `request`.


## Concepte de lucru

De regulă, vei avea câte o bază de date per aplicație. O bază de date are mai multe obiecte care oferă stocarea. Sunt numite *object stores*. dar nu sunt tabele.

### Baza de date

#### *database*

Este un depozit care constă din `object store`-uri. Fiecare bază de date trebuie să aibă un nume, care este orice valoare de tip string și în plus trebuie să aibă atribuită o versiune. În cazul versiunii, dacă acesta nu este precizată la momentul constituirii bazei, din oficiu va primi valoarea 1.

#### *object store*

Este forma în care datele sunt stocate în bază. Object store ține datele fără a le șterge, care la rândul lor sunt perechi de chei/valori. Înregistrările dintr-un *object store* sunt sortate în funcție de chei în ordine ascendentă.

Fiecare *object store* trebuie să aibă un nume care să fie unic în baza de date. Opțional, un *object store* poate avea un *key generator* și un *key path*. Dacă *object store*-ul are un *key path*, va folosi *in-line keys*.

#### *versiune*

Orice bază de date are o versiune.

#### *database connection*

Când deschizi o bază de date, spui că ai realizat o conexiune la aceas bază de date. O bază de date poate avea mai multe conexiuni deschise în același timp.

#### *transaction*

Este un set atomic de operațiuni de accesare și modificare a datelor privind o anumită bază de date. Este modul în care interacționezi cu datele din bază.

Tranzacțiile se desfășoară într-un domeniu asupra căruia au control. Acesta este denumit *scope* și ete definit la momentul creării bazei de date indicând un *object store*.

#### *request*

Este operațiunea prin care se face citirea sau scrierea într-o bază de date. Fiecare *request* reprezintă, fie o operațiune de citire, fie una de scriere.

#### *index*

Un index este un *object store* specializat pentru căutarea în înregistrări, care este numite object store-ul referit - *referenced object store*.

Indexul este un mecanism de stocare cu perechi cheie/valoare în care valorile sunt de fapt chei ale înregistrărilor din *referenced object store*. Ori de câte ori este modificat object store-ul pentru care s-a constituit indexul, acesta va fi actualizat. Fiecare înregistrare dintr-un index indică câte o înregistrare în *referenced object store*-ul corespondent, dar mai multe indexuri pot referi același *object store*.

### Cheile și valorile

#### `key`

Este valoarea prin care alte valori sunt organizate și pot fi accesate dintr-un *object store*. Un *object store* poate deriva chei din una sau mai multe surse:
- un generator de chei,
- un *key path* sau
- o cheie menționată explicit.

Toate cheile dintr-un object store trebuie să fie unice.

Cheile pot fi un string, date, float, un blob sau un array. Array-urile de array-uri sunt permise.

#### `key generator`

Este un mecanism folosit pentru a produce chei noi într-o manieră ordonată. Dacă un *object store* nu are un key generator, aplicația trebuie să ofere cheile pentru ca noile înregistrările să poată fi stocate. Acest mecanism ține de producătorul browserului.

#### `in-line key`

Este o cheie care este stocată ca parte a valorii care este stocată. Poate fi regăsită folosind un *key path*. O cheie `in-line` poate fi generată folosind un generator. După ce a fost generată cheia, poate fi stocată în valoarea care folosește *key path*-ul sau pur și simplu poate fi utilizată ca o cheie.

#### `out-of-line key`

Este o cheie care este stocată separat de valoare.

#### `key path`

Definește locul în care browserul ar trebui să extragă cheia din *object store* sau din *index*. O cheie validă poate să includă una din următoarele:

- un string vid,
- un identificator JavaScript
- mai mulți identificari JavaScript separați prin virgule sau
- un array care să conțină oricare dintre cele menționate.

un *key path* nu poate avea spații.

#### `value`

Valorile pot fi orice valori sunt acceptate în JavaScript: `boolean`, `number`, `string`, `date`, `object`, `array`, `regexp`, `undefined` și `null`.

Mai pot fi introduse date binare `Blob` și fișiere.

### Range și scope

#### `scope`

Este setul de `object stores` și indexurile pentru care se aplică o tranzacție. Scope-urile tranzacțiilor se pot suprapune și executa în același timp. Pe de altă parte scope-urile tranzacțiilor în scriere nu se pot suprapune. Poți iniția câteva tranzacții în același scope în același timp, dar acestea sunt executate secvențial una după cealaltă.

#### `cursor`

Este un mecanism pentru iterarea a mai multor înregistrări cu un *key range*. Cursorul are o sursă care indică care index sau *object store* este iterat. Are o poziție în range și se mișcă într-o direcție crescătoare sau descrescătoare în ordinea cheilor înregistrărilor.

#### `key range`

Este un interval continuu peste niște tipuri de date folosite drept chei. Sunt intervale de chei care pot fi extrase din *object stores* sau *indexes*.

## Testarea suportului browserului

Înainte de a porni la drum, mai întâi de toate trebuie testat browserul pentru a vedea nivelul de suport.

```javascript
// Este posibil ca suportul să fie oferit prin prefixare
window.indexedDB = window.indexedDB || window.mozIndexedDB || window.webkitIndexedDB || window.msIndexedDB;
// Nu se va face vreun identificator numit indexedDB. Se vor face referințe către obiecte window.IDB*
window.IDBTransaction = window.IDBTransaction || window.webkitIDBTransaction || window.msIDBTransaction || {READ_WRITE: "readwrite"}; // e necesară doar dacă browserul este vechi și nu are suport pentru constante
window.IDBKeyRange = window.IDBKeyRange || window.webkitIDBKeyRange || window.msIDBKeyRange;
// Mozilla nu are nevoie de window.mozIDB* pentru că nu a prefixat aceste obiecte.
```

## Deschiderea unei baze de date

Pentru a porni la drum, este nevoie de a deschide baza de date.

```javascript
var request = window.indexedDB.open("BazaDeTest", 3);
```

Cererea deschiderii unei baze în urma aplicării metodei `open()` va returna un obiect `IDBOpenDBRequest` care conține valori pentru succes și pentru eroare. Marea majoritate a metodelor IndexedDB au același comportament.

Rezultatul operațiunii `open()` este o instanță `IDBDatabase`.

## Referințe

- [IndexedDB API, MDN](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
- [Indexed Database API 3.0, Editor’s Draft, 15 July 2019](https://w3c.github.io/IndexedDB/)
- [Using IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)
- [IndexedDB with usability, Github](https://github.com/jakearchibald/idb)
