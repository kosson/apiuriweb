# File API

Acesta este un API cu ajutorul căruia se pot reprezenta obiecte de fișiere în browser. Permite obținerea de informații despre fișiere și permite JavaScript-ului să acceseze conținutul.

Obiectele `File` sunt obținute dintr-un obiect `FileList` care este returnat ca rezultat al acțiunii utilizatorului care a selectat un element `<input type="file">` sau a făcut un drag-and-drop, în urma căruia a fost generat un obiect `DataTransfer`.

Un obiect `File` este un tip specific de `Blob` și poate fi folosit în oricare context în care un astfel de obiect poate fi folosit.

Urrmătoarele acceptă `Files` și `Blobs`:

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

Metoda returnează un obiect `Blob` nou care conține date într-o plajă de bytes specificată în contextul `Blob`-ului original.

## Resurse

- [File API, W3C](https://www.w3.org/TR/FileAPI/)
- [Blob, javascript.info](https://javascript.info/blob)
- [File | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File)
- [Using files from web applications](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
