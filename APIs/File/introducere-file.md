# File API

Acesta este un API cu ajutorul căruia se pot reprezenta obiecte de fișiere în browser. Permite obținerea de informații despre fișiere și permite JavaScript-ului să acceseze conținutul.

Obiectele `File` sunt obținute dintr-un obiect `FileList` care este returnat ca rezultat al acțiunii utilizatorului care a selectat un element `<input type="file">` sau a făcut un drag-and-drop, în urma căruia a fost generat un obiect `DataTransfer`.

Un obiect `File` este un anumit tip de `Blob` și poate fi folosit în oricare context în care un astfel de obiect poate fi folosit.

Următoarele metode acceptă `Files` și `Blobs`:

- `FileReader()`,
- `URL.createObjectURL()`,
- `createImageBitmap()` și
- `XMLHttpRequest.send()`

## Constructorul `File()`

Acest constructor returnează un obiect nou de tip `File`.

## Proprietăți

### `File.lastModified`

Este o proprietate read-only care returnează data ultimei modificări aduse fișierului în UNIX epoch.

### `File.name`

Este o proprietate read-only care returnează numele fișierului pentru care s-a creat o reprezentare `File`.

### `File.size`

Această proprietate este disponibilă pentru că interfața `File` o implementează și pe `Blob`. Este o proprietate read-only care returnează dimensiunea în bytes a fișierului.

### `File.type`

Tot datorită implementării interfeței `Blob`, putem returna MIME type-ul fișierului.

## Metode

Interfața `File` nu are propriile metode, ci implementează pe cele pe care `Blob` le pune la dispoziție.

### `Blob.slice([start[, end[, contentType]]])`

Metoda returnează un obiect `Blob` nou care conține date într-o plajă de bytes specificată în contextul `Blob`-ului original. Propriu-zis poți obține un nou `Blob` folosind doar o parte a fișierului. Această metodă își dovedește utilitatea în momentul în care trimiți un fișier în calupuri către server. Prin `start` și `end` precizezi dimensiunea fragmentului de date în bytes pe care dorești să-l trimiți. Pentru o conexiune ADSL, viteza de upload este relativ în jurul valorii de 1.2Mbits/s, adică 150Kb/s. Din motive de siguranță, să limităm fereastra de date la 100.000 Bytes.

```javascript
var slice = file.slice(0, 100000);
```

Fragmentele mari de date vor introduce o lentoare în procesare, pe când cele de dimensiuni mici au o rată de refresh mai mare.
Pentru a citi și trimite către server fragmentele de date, vei folosi `FileReader`, adică `readAsArrayBuffer(blob)`. Verifică dacă este suport și pentru `readAsBinaryString(blob)`. Rezultatul folosirii metodei `readAsArrayBuffer(blob)` este un obiect cu date neprelucrate (*raw*) de o dimensiune fixă. Pentru că `FileReader` face procesările asincron, va declanșa un eveniment `onload` atunci când rezultatul este gata.

### `Blob.prototype.stream()`

Transformă un `File` într-un `ReadableStream` care poate fi folosit pentru a citi conținutul respectivului `File`.

### `Blob.prototype.text()`

Transformă `File` într-un stream și îl citește până la epuizarea acestuia. Returnează un `Promise` care se rezolvă cu un `USVString` (text).

### `Blob.prototype.arrayBuffer()`

Transformă `File` într-un stream și îl citește până la epuizarea acestuia. Returnează un `Promise` care se rezolvă cu un `ArrayBuffer`.

## Resurse

- [File API, W3C](https://www.w3.org/TR/FileAPI/)
- [Blob, javascript.info](https://javascript.info/blob)
- [File | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File)
- [Using files from web applications | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
