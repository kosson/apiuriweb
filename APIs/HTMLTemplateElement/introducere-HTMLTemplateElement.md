# HTMLTemplateElement

Este o interfață ce permite accesul la conținutul unui element `<template>`. Toate metodele acestei interfețe sunt moștenite de la `HTMLElement`.

Lanțul de moștenire:

EventTarget<--Node<--Element<--HTMLElement<--HTMLTemplateElement

## Proprietăți

### `content`

Este o proprietate read-only a cărei valoare returnată este un `DocumentFragment` ce conține un arbore al elementelor aflate în `<template>`.

```javascript
var documentFragment = templateElement.content;
```

Un posibil model este

```javascript
var templateElement = document.querySelector("#ceva");
var documentFragment = templateElement.content.cloneNode(true);
```

## Exemplul documentației

Pentru a adăuga repetitiv în baza unui template rânduri la un tabel, se va proceda astfel.

```html
<!DOCTYPE html>
<html lang='en'>
<title>Cat data</title>
<script>
 // Data is hard-coded here, but could come from the server
 var data = [
   { name: 'Pillar', color: 'Ticked Tabby', sex: 'Female (neutered)', legs: 3 },
   { name: 'Hedral', color: 'Tuxedo', sex: 'Male (neutered)', legs: 4 },
 ];
</script>
<table>
 <thead>
  <tr>
   <th>Name <th>Color <th>Sex <th>Legs
 <tbody>
  <template id="row">
   <tr><td><td><td><td>
  </template>
</table>
```

Cu scriptul:

```javascript
 var template = document.querySelector('#row');
 for (var i = 0; i < data.length; i += 1) {
   var cat = data[i];
   var clone = template.content.cloneNode(true);
   var cells = clone.querySelectorAll('td');
   cells[0].textContent = cat.name;
   cells[1].textContent = cat.color;
   cells[2].textContent = cat.sex;
   cells[3].textContent = cat.legs;
   template.parentNode.appendChild(clone);
 }
```

## Referințe

- [HTMLTemplateElement.content | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLTemplateElement/content)
- [Cloning steps](https://html.spec.whatwg.org/multipage/scripting.html#dom-template-content)
