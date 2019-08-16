# EventTarget

`EventTarget` este o interfață DOM care este implementată de obiectele care pot primi evenimente și pot atașa funcții cu rol de receptori (*listeners*) pentru acestea.

`Element`. `Document` și `Window` sunt cele mai întâlnite ținte ale evenimentelor.

## Metode

### `EventTarget.addEventListener()`

Atașează (*registers*) o funcție cu rol de receptor (*listener*) pentru un anumit tip de eveniment -`EventTarget`.

### `EventTarget.removeEventListener()`

Șterge un eveniment de pe un element.

### `EventTarget.dispatchEvent()`

Trimite un eveniment către un `EventTarget`.
