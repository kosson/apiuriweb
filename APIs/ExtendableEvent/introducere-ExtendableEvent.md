# ExtendableEvent

Este o interfață care prelungește viața evenimenteleor `install` și `activate`. Acest lucru permite ca evenimentele funcționale așa cum este `fetch` să nu fie declanșate până când nu se actualizează schemele bazelor de date și intrările vechi din cache nu sunt curățate.

Această interfață moștenește proprietățile și metodele din `Event`, fiind discutabilă doar atunci când scope-ul global este `ServiceWorkerGlobalScope`. Nu este disponibilă din `Window` sau din scope-ul altui tip de worker.

Constructorul este `ExtendableEvent()`.

## Metode proprii

### `ExtendableEvent.waitUntil()`

Metoda `waitUntil` extinde viața evenimentului. Este proiectat să fi apelat în contextul evenimentului `install`.
