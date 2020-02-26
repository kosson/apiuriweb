# Blob

Un obiect `Blob` este o reprezentare a unui `blob`, care în sine este un obiect de date ce nu pot fi modificate. Aceste date pot fi citite drept text sau date binare. Aceste date pot fi convertite într-un `ReadableStream` pentru ca metodele sale să poată fi folosite pentru a-l procesa.

Acesta este un constructor folosit pentru a constitui o secvență de bytes. Un `Blob` este un fragment de bytes care ține datele unui fișier. Un `Blob` nu este o referință către fișier. Un `Blob` are dimensiune și MIME exact precum fișierul are. Un `Blob` poate fi folosit ca un fișier.

Conținutul unui `Blob` poate fi citit ca un `ArrayBuffer`, ceea ce indică `Blob`-ul ca un mecanism ideal pentru stocarea de date binare.

**Spune standardul**:

> Un obiect Blob se referă la o secvență de bytes care are un atribut ce indică dimensiunea, fiind numărul total de bytes din secvență și un atribut type, care este un string ASCII în lower case ce reprezintă tipul de media pe care secvența de bytes o reprezintă.


```javascript
 var myBlob = new Blob(["Conținutul Blob-ului"], {type : "text/plain"});
```

Primul argument al constructorului `blobParts` este un array de bytes, iar al doilea argument al opțiunilor menționează tipul resursei, de fapt un MIME-type (`image/png`).

Argumentul `blobParts` poate fi de tip text sau chiar binar. Atunci când folosim date binare, `blobParts` poate fi un `TypedArray`. Pentru a scoate un `TypedArray` dintr-un `Blob`, se va folosi `FileReader`.

Pentru a citi datele dintr-un `Blob`, se poate folosi clasa `FileReader`.

```javascript
var myReader = new FileReader();
//handler executat o singură dată
myReader.addEventListener("loadend", function(e){
    document.getElementById("paragraph").innerHTML = e.srcElement.result;// afișează stringul
});
// pornește citirea
myReader.readAsText(myBlob);
```

## Lucrul cu resurse text

Un `Blob` poate fi folosit ca un URL pentru un `<a>` sau `<img>`, dacă se dorește afișarea resursei. Dacă se folosește pentru a fi încărcată sau descărcată, va trebui specificat `Content-Type`-ul.

Folosind atributul `download` pentru un `<a>`, se va forța descărcarea resursei.

```html
<a download="fisier.txt" href='#' id="link">Descarcă</a>

<script>
let blob = new Blob(["Un fragment de text"], {type: 'text/plain'});
link.href = URL.createObjectURL(blob);
</script>
```

Poți construi și o variantă dinamică în JavaScript.

```javascript
let link = document.createElement('a');
link.download = 'fisier.txt';
let blob = new Blob(["Un fragment de text"], {type: 'text/plain'});

link.href = URL.createObjectURL(blob); // constituirea unei adrese pentru blob
link.click();
URL.revokeObjectURL(link.href); // eliberarea memoriei
```

Pentru a se constitui un link valid pentru un blob, se folosește `URL.createObjectURL`, care va genera un link după următorul tipic: `blob:<origin>/<uuid>`.

Legătura dintre link și blob va fi menținută, câtă vreme documentul este încărcat în browser. Trecerea la altă pagină, va conduce la pierderea link-ului și eliberarea memoriei în care era blob-ul. Legătura dintre URL și blob, va fi generată la momentul folosirii constructorului `URL`.

Poți forța ștergerea legăturii prin folosirea lui `URL.revokeObjectURL(url)`. Este indicată eliberarea memoriei de îndată ce blobul a fost utilizat.

### `Blob` în base64

Dacă nu dorești să creezi o legătură, un link către blob, poți să-l transformi într-un string codat base64. Acest lucru permite constituirea de link-uri de date.

Este o alternativă la `URL.createObjectURL` și poate fi folosită pentru url-uri de date `data:[<mediatype>][;base64],<data>`.

Pentru a transforma un `Blob` într-un base64, vom folosi un obiect `FileReader`. Acest obiect poate citi din `Blob`-uri.

```javascript
let link = document.createElement('a');
link.download = 'fisier.txt';
let blob = new Blob(["Un fragment de text"], {type: 'text/plain'});

let reader = new FileReader();
reader.readAsDataURL(blob); // se face conversia blob-ului în base64
reader.onload = function() {
  link.href = reader.result; // data url
  link.click();
};
```

Pentru lucrul cu imagini, avem exemplul încărcării uneia folosind canvas-ul.

```javascript
let img = document.querySelector('img');

let canvas = document.createElement('canvas'); // creează un canvas de aceeași dimensiune
canvas.width = img.clientWidth;
canvas.height = img.clientHeight;

let context = canvas.getContext('2d');

context.drawImage(img, 0, 0); // metoda drawImage permite și tăierea imaginii, dacă se dorește

// toBlob este o metodă async
canvas.toBlob(function(blob) {
  let link = document.createElement('a');
  link.download = 'example.png';

  link.href = URL.createObjectURL(blob);
  link.click();

  // șterge legătura la blob pentru a curăța memoria
  URL.revokeObjectURL(link.href);
}, 'image/png');

// și varianta async
let blob = await new Promise(resolve => canvasElem.toBlob(resolve, 'image/png'));
```

### Din `Blob` în `ArrayBuffer`

Constructorul `Blob` permite constituirea de blob-uri din orice sursă. Acestea pot fi chiar buffere.

```javascript
let fileReader = new FileReader();

fileReader.readAsArrayBuffer(blob);

fileReader.onload = function(event) {
  let arrayBuffer = fileReader.result;
};
```

`ArrayBuffer` și `Uint8Array` sunt date binare. `Blob`-ul reprezintă date binare, care se încadrează unui tip (*binary data with type*).
Acest avantaj pe care-l prezintă `Blob`-ul îl face preferabil atunci când ai de încărcat și descărcat fișiere în browser.

`XMLHttpRequest` și `fetch` lucrează cu `Blob`-urile în mod nativ.

### Din `Blob` în `File`

Un `Blob` aproape că este un fișier. Îi lipsesc câteva informații:

- `lastModifiedDate` și
- `name`.

Pentru a-l transforma în `File`, vom introduce aceaste informații.

```javascript
function blobToFile(theBlob, fileName){
    //A Blob() is almost a File() - it's just missing the two properties below which we will add
    theBlob.lastModifiedDate = new Date();
    theBlob.name = fileName;
    return theBlob;
}
```

Și o variantă „modernă”:

```javascript
function blob2file(blobData) {
  const fd = new FormData();
  fd.set('a', blobData, 'filename');
  return fd.get('a');
}
```

În Edge și Safari

```javascript
var blob = new Blob(byteArrays, { type: contentType });
blob.lastModifiedDate = new Date();
blob.name = name;
```

### `Base64` în `File`

Uneori ai nevoie să transformi un fișier codat Base64 într-un `File`.

```javascript
function base64ToFile(base64Data, tempfilename, contentType) {
    contentType = contentType || '';
    var sliceSize = 1024;
    var byteCharacters = atob(base64Data);
    var bytesLength = byteCharacters.length;
    var slicesCount = Math.ceil(bytesLength / sliceSize);
    var byteArrays = new Array(slicesCount);

    for (var sliceIndex = 0; sliceIndex < slicesCount; ++sliceIndex) {
        var begin = sliceIndex * sliceSize;
        var end = Math.min(begin + sliceSize, bytesLength);

        var bytes = new Array(end - begin);
        for (var offset = begin, i = 0 ; offset < end; ++i, ++offset) {
            bytes[i] = byteCharacters[offset].charCodeAt(0);
        }
        byteArrays[sliceIndex] = new Uint8Array(bytes);
    }
    var file = new File(byteArrays, tempfilename, { type: contentType });
    return file;
}
```

## Resurse

- [Blob, javascript.info](https://javascript.info/blob)
- [How to convert Blob to File in JavaScript | Stackoverflow](https://stackoverflow.com/questions/27159179/how-to-convert-blob-to-file-in-javascript)
- [Convert blob to file | Stackoverflow](https://stackoverflow.com/questions/27553617/convert-blob-to-file/27565109)
