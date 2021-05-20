# FileReader

Este o interfață care permite citirea asincronă a conținutului fișierelor care sunt stocate pe computerul utilizatorului. Acest obiect oferă metodele necesare citirii unui fișier sau a unor buffere raw (`File` sau `Blob`) aflate pe computerului pe care rulează browser-ul.

Interfața `FileReader` are câteva stări care pornesc de la cea din oficiu care este `empty`, la `loading` și `done`.
Interfața are și un rezultat asociat, care poate fi `null`, un `DOMString` sau un `ArrayBuffer`. Starea inițială este `null`.
Atunci când apar erori acestea sunt semnalate printr-un `DOMException`, iar dacă acestea nu există, valoarea este `null`.

## Constructorul `FileReader()`

Returnează un obiect `FileReader`.

## Proprietăți

### `FileReader.error`

Este o proprietate read-only care returnează un obiect `DOMException` care conține eroarea apărută la citirea fișierului.

### `FileReader.readyState`

Această proprietate este read only și este un număr care indică starea în care se află `FileReader`.
Stările pot fi următoarele:

- `EMPTY`; proprietatea este codată prin `0`,
- `LOADING`; proprietatea fiind codată cu 1, indicând faptul că datele se încarcă,
- `DONE`; are valoarea `2`, indicând faptul că s-a încheiat citirea datelor.

### `FileReader.result`

Această proprietate este chiar conținutul fișierului care este disponibil doar după ce s-a încheiat operațiunea de citire. Formatul datelor este determinat de metoda folosită pentru inițierea operațiunii de citire.

## Evenimente

API-ul `FileReader` moștenește din `EventTarget`, ceea ce permite atașarea unor funcții cu rol de receptor pentru toate evenimentele acestuia. Pentru a face acest lucru, se va folosi `addEventListener()` sau folosing proprietatea `on*numeeveniment*`.

### `abort`

Declanșat la momentul în care se anulează citirea fișierului prin apelul metodei `FileReader.abort()`. Poate fi instrumentat și prin proprietatea `onabort`.

### `error`

Eveniment declanșat în momentul în care citirea fișierului a eșuat din cauza unei erori. Poate fi instrumentat și prin proprietatea `onerror`.

### `load`

Eveniment declanșat în momentul în care fișierul a fost încărcat cu succes. Poate fi instrumentat și prin proprietatea `onload`.

### `loadend`

Eveniment declanșat în momentul în care fișierul a fost încărcat cu succes sau a eșuat. Poate fi instrumentat și prin proprietatea `loadend`.

### `loadstart`

Eveniment declanșat în momentul în care a pornit citirea fișierului. Poate fi instrumentat și prin proprietatea `loadstart`.

### `progress`

Este un eveniment declanșat periodic pe măsură ce datele unui fișier sunt citite. Poate fi instrumentat și prin proprietatea `progress`.

## Event handlers

### `FileReader.onabort`

Este o funcție folosită pentru a gestiona un eveniment `abort`. Acest eveniment este declanșat ori de câte ori operațiunea de citire este anulată.

### `FileReader.onerror`

Este o funcție care gestionează evenimentul `error`, fiind declanșată ori de câte ori apare o eroare.

### `FileReader.onload`

Este o funcție care gestionează evenimentul `load`, fiind invocată atunci când operațiunea de citire este încheiată cu succes.

### `FileReader.onloadstart`

Este o funcție care gestionează evenimentul `loadstart`, fiind invocată atunci când operațiunea de citire a început.

### `FileReader.onloadend`

Este o funcție care gestionează evenimentul `loadend`, fiind invocată atunci când operațiunea de citire s-a încheiat, fie cu succes, fie a eșuat.

### `FileReader.onprogress`

Este o funcție care gestionează evenimentul `progress`, fiind invocată este citit un `Blob`.

## Metode

### `FileReader.abort()`

Folosești această metodă pentru a opri încărcarea fișierului. Atunci când este apelată, se va seta proprietatea `readyState` cu valoarea pentru `DONE`: `2`.

### `FileReader.readAsArrayBuffer()`

Metoda pornește citirea conținutului `Blob`-ului specificat și în momentul în care s-a încheiat, atributul `result` va conține un `ArrayBuffer` care reprezintă datele fișierului. Rezultatul folosirii metodei `readAsArrayBuffer(blob)` aplicate pe un obiect de tip `Blob`, este un obiect cu date neprelucrate (*raw*) de o dimensiune fixă. Pentru că `FileReader` face procesările asincron, va declanșa un eveniment `onload` atunci când rezultatul este gata.

Mai jos este un exemplu de încărcare a unei imagini folosind drept nivel de transport Socket.io așa cum se desprinde din articolul [How do I send image to server via socket.io? | stackoverflow.com](https://stackoverflow.com/questions/59478402/how-do-i-send-image-to-server-via-socket-io).

```javascript
// client
document.getElementById('file').addEventListener('change', function() {
  const reader = new FileReader();
  reader.onload = function () {
    const bytes = new Uint8Array(this.result);
    socket.emit('image', bytes);
  };
  reader.readAsArrayBuffer(this.files[0]);
}, false);

// server
socket.on('image', async image => {
    // image is an array of bytes
    const buffer = Buffer.from(image);
    await fs.writeFile('/tmp/image', buffer).catch(console.error); // fs.promises
});
```

Pentru a emite o imagine către client folosind Socket.io.

```javascript
// Server side
socket.emit('image', image.toString('base64')); // image should be a buffer
// Client side
socket.on('image', image => {
    // create image with
    const img = new Image();
    // change image type to whatever you use, or detect it in the backend
    // and send it if you support multiple extensions
    img.src = `data:image/jpg;base64,${image}`;
    // Insert it into the DOM
});
```

### `FileReader.readAsBinaryString()`

Metoda pornește citirea conținutului `Blob`-ului specificat și în momentul în care s-a încheiat, atributul `result` va conține datele binare brute din fișier ca string.

### `FileReader.readAsDataURL()`

Metoda pornește citirea conținutului `Blob`-ului specificat și în momentul în care s-a încheiat, atributul `result` va conține un `data`: URL-ul către reprezentarea datelor fișierului.

### `FileReader.readAsText()`

Metoda pornește citirea conținutului `Blob`-ului specificat și în momentul în care s-a încheiat, atributul `result` va conține un string text. Opțional, se poate specifica un nume pentru schema de codare a caracter

## Referințe

-   [File API, 6.3. The FileReader API](https://w3c.github.io/FileAPI/#dfn-filereader)
-   [Using files from web applications](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
-   [Understanding FileReader](https://blog.shovonhasan.com/using-promises-with-filereader/)
-   [Using files from web applications | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
-   [Reading files in JavaScript using the File APIs](https://www.html5rocks.com/en/tutorials/file/dndfiles/)
