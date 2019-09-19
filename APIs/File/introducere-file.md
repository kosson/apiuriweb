# File API

Acesta este un API cu ajutorul căruia se pot reprezenta obiecte de fișiere în browser. Permite obținerea de informații despre fișiere și permite JavaScript-ului să acceseze conținutul.

Obiectele `File` sunt obținute dintr-un obiect `FileList` care este returnat ca rezultat al acțiunii utilizatorului care a selectat un element `<input>` sau a făcut un drag-and-drop, în urma căruia a fost generat un obiect `DataTransfer`.

Un obiect `File` este un tip specific de `Blob` și poate fi folosit în oricare context în care un astel de ofiect poate fi folosit:

- `FileReader`,
- `URL.createObjectURL()`,
- `createImageBitmap()` și
- `XMLHttpRequest.send()`


## Resurse

- [File API, W3C](https://www.w3.org/TR/FileAPI/)
- [Blob, javascript.info](https://javascript.info/blob)
- [File | MDN](https://developer.mozilla.org/en-US/docs/Web/API/File)
- [Using files from web applications](https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications)
