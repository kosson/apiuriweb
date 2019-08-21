#  IDBOpenDBRequest

Este o interfață a API-ului IndexedDB care oferă acces la rezultatele apărute în urma cererii de a deschide sau șterge o bază de date.

Această interfață este obținută prin apelarea metodei `open()` a lui `IDBFactory.open` sau `delete` a lui `IDBFactory.delete()`.

Aceste API-uri sunt disponibile spre utilizarea și web worker-ilor.

## Moștenire

`EventTarget` <- `IDBRequest` <- `IDBOpenDBRequest`

## Evenimente

### `blocked`

Este declanșat atunci când o conexiune este deja deschisă și blochează o tranzacție `versionchange` pe aceeași bază de date. Evenimentul este disponibil și ca `onblocked`.

### `upgradeneeded`

Este declanțat atunci când se dorește deschiderea unei baze de date care este cu un număr mai mare decât versiunea curentă. Este disponibil și ca `onupgradeneeded`.

## Referințe

- [IDBOpenDBRequest, MDN](https://developer.mozilla.org/en-US/docs/Web/API/IDBOpenDBRequest)
