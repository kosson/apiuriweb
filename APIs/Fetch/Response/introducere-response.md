# Response

Standardul spune că „rezultatul unui **fetch** este un **răspuns**”. Ceea ce merită reținut este faptul că un „răspuns evoluează în timp”. De îndată ce un server răspunde cu headere, acest obiect răspuns se formează. Putem investiga acest obiect de răspuns.

```javascript
let response = await fetch(url);
if (response.ok) {
    // response.ok înseamnă că avem un cod HTTP între 200 și 299
    let jsonData = response.json();
} else {
    console.error('Eroarea HTTP: ', response.status);
}
```

Obiectului de răspuns îi este asociat un obiect `Headers` , care inițial are valoarea `null`. Aceluiași obiect îi este asociată o promisiune numită de standard *trailer promise*.

Obiectul de răspuns din punctul de vedere al standardului poate fi de mai multe tipuri: "basic", "cors", "default", "error", "opaque", "opaqueredirect".

Obiectul de răspuns are și un corp (*body*). Acest *body* poate fi:

- un stream (`null` sau `ReadableStream`),
- un `Blob`,
- un `BufferSource`,
- un `FormData`,
- un `URLSearchParams`,
- un `USVString`.

### Corpul unui răspuns - `response.body`

Trebuie reținut un aspect foarte important: obiectul corp, care poate fi accesat cu `response.body` este un obiect `ReadableStream`, ceea ce permite citirea datelor pe fragmentele bine-cunoscute ca `chunks`.

```javascript
const image = document.getElementById('target');

// Fetch the original image
fetch('./tortoise.png')
// Retrieve its body as ReadableStream
.then(response => response.body)
.then(body => {
  const reader = body.getReader();

  return new ReadableStream({
    start(controller) {
      return pump();

      function pump() {
        return reader.read().then(({ done, value }) => {
          // When no more data needs to be consumed, close the stream
          if (done) {
            controller.close();
            return;
          }

          // Enqueue the next data chunk into our target stream
          controller.enqueue(value);
          return pump();
        });
      }
    }
  })
})
.then(stream => new Response(stream))
.then(response => response.blob())
.then(blob => URL.createObjectURL(blob))
.then(url => console.log(image.src = url))
.catch(err => console.error(err));
```

Pentru a exploata datele obiectului răspuns, API-ul pune la dispoziție câteva metode utile în aces sens:

- `response.json()` care parsează răspunsul ca obiect JSON
- `response.text()`, care parsează corpul răspunsului ca pe un text
- `response.formData()`, care returnează un răspuns de tipul `FormData` care are o codare `form/multipart`
- `response.blob()`, returnează răspunsul ca `Blob` (date binare de un anumit tip)
- `response.arrayBuffer()`, care returnează răspunsul ca `ArrayBuffer` (date binare)

Dacă presupunem că accesăm date de la un API extern, iar formatul este *json*, putem decide felul în care vom consuma datele, fie folosind sintaxa `await`, fie folosind promisiunile.

```javascript
let răspuns = await fetch('https://undeva.ro/api/v2/resurse');
let resurse = await răspuns.json(); // citește corpul ca json
console.log(resurse[0].nume);
```

Același parcurs îl putem angaja folosind promisiunile. Ține de propria abordare.

```javascript
fetch('https://undeva.ro/api/v2/resurse').then((raspuns) => raspuns.json()).then(resurse => console.log(resurse[0].nume));
```

Un lucru foarte important de precizat este faptul că prelucrarea corpului obiectului răspuns se poate face o singură dată. Nu este posibilă aplicarea în succesiune a mai multor metode de tratare a corpului. Acest lucru nu este posibil pentru că acele date deja au fost consumate de prima metodă de prelucrare.
