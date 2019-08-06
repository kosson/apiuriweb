# Fetch

Pentru a înțelege și opera cu API-ul Fetch, trebuie să înțelegi ce este o promisiune în JavaScript, cum funcționează și care este structura sa. Înțelegerea promisiunilor va netezi calea către înțelegerea acestui instrument care uțurează lucrul cu resursele la distanță.

Scopul acestui API este acela de a unifica componentele folosite pentru a aduce resurse din rețea. Api-ul `fetch` este deja disponibil ca parte al API-ului browserului și nu necesită un pas suplimentar pentru a-l accesa.

`fetch()` este o metodă a obiectului global sau a unui **worker** care returnează o promisiune.

```javascript
fetch('x'); // x fiind, de regulă calea către o resursă la distanță (URI)
// Promise { <state>: "rejected", <reason>: TypeError }
fetch('x').then(raspuns => console.log('am primit raspuns'));
// Promise { <state>: "pending" }
```

Pentru a face un apel `fetch`, metoda acceptă drept prim parametru o adresă către resursa dorită urmată de un obiect de configurare.

```javascript
fetch('https://httpbin.org/post', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  },
  mode: 'cors',
  body: JSON.stringify({mesaj: 'Salutare!'})
}).then(function(raspuns){
  console.log(raspuns);
  return raspuns.json();
}).then(function(date){
  console.log(date);
}).catch(function(eroare){
  console.log(eroare);
});
```

Ceea ce oferă un `fetch` este o promisiune pe care se pot înlănțui metodele `then` cu ajutorul cărora se pot prelucra rezultatele.

## Obiectul de configurare

Pentru a constitui obiectul de configurare, avem următoarele posibile componente configurabile:

- metoda, care specifică verbul HTTP folosit,
- headerele
- modului de acces la resurse
- corpul.

Headerele pot fi constituite și prin instanțierea constructorului `Headers()`.

```javascript
var headers = new Headers();
```

Odată instanțiat obiectul, se pot adăuga headere, se pot poate verifica dacă un anumit header există deja folosind metodele specifice:

```javascript
headers.append('Content-Type', 'text/plain');
headers.append('X-My-Custom-Header', 'CustomValue');

// Verificare, get și set
headers.has('Content-Type'); // true
headers.get('Content-Type'); // "text/plain"
headers.set('Content-Type', 'application/json');

// Ștergerea unui header
headers.delete('X-My-Custom-Header');
```

Obiectul headerelor poate fi populat inițial cu setări considerate a fi esențiale.

```javascript
var headers = new Headers({
	'Content-Type': 'text/plain',
	'X-My-Custom-Header': 'OValoare'
});
```



## Exemple practice

### Metoda `GET` - aducere date

Să presupunem că lucrezi cu API-ul Europeana.eu. Putem foarte simplu să construim un exemplu complet de utilizarea a lui `fetch()` pentru a accesa o înregistrare unică.

```javascript
var adresa = "https://www.europeana.eu/api/v2/search.json?wskey=XXXXXXXXX&query=The%20Fraternity%20between%20Romanian%20and%20French%20Army";

// înlocuiește cheia API din link, cu una personală
// wskey=XXXXXXXXX - obține o cheie de la https://pro.europeana.eu/get-api
// dacă nu introduci cheia personală vei avea o eroare
// Cross-Origin Request Blocked

fetch(adresa)
  .then( function aduRes (raspuns) {
    // dacă e JSON, trimite-l ca atare,
    if (raspuns.ok && raspuns.headers.get('Content-Type') === 'application/json') {
      return raspuns.json();
    } else if (raspuns.status == 404) {
      throw new Error('Calea către resursă nu există');
    }
    // dacă nu, trimite ce primești
    return raspuns.text();
  }).then(function vizualizeaza (reprezentareDate) {
    console.log(reprezentareDate); // sau
    // console.log(JSON.stringify(reprezentareDate))
  }).catch(function (eroarea) {
    console.log("Eroarea apărută: ", eroarea.message);
  });
```

Observă faptul că primul `then(raspuns)` are rolul de a constitui o reprezentare a datelor venite într-un format pe care să-l putem consuma. Abia cel de-al doilea `then(reprezentareDate)` are rolul de a lucra ceva cu datele aduse.

### Metoda `POST` - trimitere date

API-ul `Fetch` poate fi utilizat și pentru a trimite date. Pentru acest lucru va trebui să construim un obiect `Request` (vezi API-ul `Request` pentru detalii).

```javascript
var referintaForm = document.getElementById('descriere');
var dateleDinFormular = new FormData(referintaForm);
var radacinaURI = 'http://site.org/';
var cale = `resurse`;
var URIcomplet = `${radacinaURI}${cale}`;
var optiuni = {
  method: 'POST',
  mode: 'cors',
  body: dateleDinFormular
};
const request = new Request(optiuni);
fetch(request).then((raspuns) => {
  if(raspuns.ok){
    return raspuns.json();
  } else {
    throw new Error('Ceva nu a mers bine');
  }
}).then((raspuns) => {
  var ref = document.querySelector('#ulprimire');
  var fragment = new DocumentFragment();
  raspuns.forEach((persoana) => {
    let li = document.createElement('li');
    li.textContext = persoana.nume;
    li.className = 'verde';
    li.className.add('adaugat');
    fragment.appenChild(li);
  });
  ref.appenChild(fragment);
}).catch((eroare) => {
  console.log('Eroare: ', eroare.message);
});
```

Pentru mai multe detalii despre obiectul `FormData`, vezi acest API.

## Referințe

-   [Standardul fetch](https://fetch.spec.whatwg.org/),
-   [Fetch - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
-   [Working with the Fetch API](https://developers.google.com/web/ilt/pwa/working-with-the-fetch-api)
-   [Fetch API (100 Days of Google Dev)](https://www.youtube.com/watch?v=g6-ZwZmRncs)

### Video

- [Fundamentals of the JavaScript fetch method for AJAX, Steve Griffith, Jul 22, 2017](https://www.youtube.com/watch?v=_5yhmkDQqIQ),
- [JavaScript AJAX with fetch](https://www.youtube.com/playlist?list=PLyuRouwmQCjkWu63mHksI9EA4fN-vwGs7)
