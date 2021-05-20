# \<input type="file">

Acest tip de element `input` permite alegerea unui fișier sau a mai multora de pe hardiscul mașinii pe care rulează browserul.

Ulterior momentului selecției, fișierele pot fi încărcate făcând un submit la formular sau pot fi manipulate folosind API-ul `File`.

```html
<label for="avatar">Alege o imagine pentru a o încărca:</label>

<input type="file"
       id="avatar" name="avatar"
       accept="image/png, image/jpeg">
```

Alte atribute care pot fi setate: `accept`, `capture`, `files`, `multiple`.

Atributul `value` al elementului de tip `file` este calea fișierului selecta având formatul `DOMString`. În cazul selectării mai multor fișiere, `value` va fi calea primului selectat. Celelalte fișiere pot fi identificate folosind proprietatea `files` pusă la dispoziție de interfața `HTMLInputElement.files`.



## Resurse

- [<input type="file"> | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file)
