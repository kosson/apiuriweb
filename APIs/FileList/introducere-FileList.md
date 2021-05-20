# FileList

Obiectele de acest tip sunt returnate de proprietatea `files` ale unui element `<input type="file">`.
Același obiect este folosit pentru a obține o listă a fișierelor care sunt într-o operațiune drag and drop (vezi `DataTransfer`).

Un obiect `FileList` conține o listă de obiecte `File`. Fiecare din obiectele `File` sunt o reprezentare a fișierelor selectate de utilizator.

În cazul în care încarci fișiere folosind un `<input id="fileItem" type="file">`, vei putea accesa fișierele dintr-o listă a acestora folosind proprietatea `files`.

```javascript
var file = document.getElementById('fileItem').files[0];
```

Poți accesa un obiect `FileList` la momentul în care fișierele apar în elementul input de tip file.

```html
<input type="file" id="input" onchange="handleFiles(this.files)">
```

Pentru a permite utilizatorului introducerea de mai multe fișiere odată, se va menționa atributul `multiple` pentru elementul input.

```html
<input type="file" id="input" multiple onchange="handleFiles(this.files)">
```

Se poate adăuga dinamic un listener pentru evenimentul `change`, dacă scenariul de lucru o cere.

```javascript
const inputElement = document.getElementById("input");
inputElement.addEventListener("change", handleFiles, false);
function handleFiles() {
  const fileList = this.files; /* acum ai FileList-ul la îndemână */
}
```

## Obținerea de informații despre fișiere

Adu-ți mereu aminte că un `FileFist` este doar o listă ce conține `Files`. Acestea au proprietăți pe care le poți accesa pentru a afla detalii.

## Exemplu

```html
<!DOCTYPE HTML>
<html>
<head>
</head>
<body>
<!--multiple is set to allow multiple files to be selected-->

<input id="myfiles" multiple type="file">

</body>

<script>
  var pullfiles=function(){
      // love the query selector
      var fileInput = document.querySelector("#myfiles");
      var files = fileInput.files;
      // cache files.length
      var fl = files.length;
      var i = 0;

      while ( i < fl) {
          // localize file var in the loop
          var file = files[i];
          alert(file.name);
          i++;
      }
  }

  // set the input element onchange to call pullfiles
  document.querySelector("#myfiles").onchange=pullfiles;
</script>

</html>
```

## Resurse

- [4.10.5.1.17 File Upload state (type=file) | HTML Living Standard](https://html.spec.whatwg.org/multipage/input.html#file-upload-state-(type=file))
- [5. The FileList Interface | File API: Editor’s Draft, 11 September 2019]()https://w3c.github.io/FileAPI/#filelist-section
- [FileList | MDN](https://developer.mozilla.org/en-US/docs/Web/API/FileList)
