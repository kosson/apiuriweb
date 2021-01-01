# EventTarget.removeEventListener()

Metoda șterge un event listener dintr-un obiect de tip `EventTarget` care a fost înregistrat folosind `EventTarget.addEventListener()`. Receptorul care trebuie eliminat poate fi identificat folosind combinații ale tipului de eveniment căruia îi este asociat, identificatorul funcției în sine, ș.a.m.d.

## Semnătura

```text
target.removeEventListener(type, listener[, options]);
target.removeEventListener(type, listener[, useCapture]);
```

## Parametrii

### `type`

Este un string case-sensitive care numește tipul de eveniment pentru care se definește un receptor (*listener*).

### `listener`

Este funcția `EventListener` care trebuie eliminată.

### `options`

Acest parametru este opțional și este un obiect care specifică caracteristici ale evenimentului. Opțiunile disponibile sunt `capture` și `mozSystemGroup`.

#### `capture`

Este o valoare `Boolean` care indică faptul că evenimente de acest tip vor fi deferite listenerului asociat înainte să treacă spre oricare `EventTarget` de mai jos din arborele DOM.

### `useCapture`

Acesta este un parametru opțional care specifică dacă `EventListener`-ul care trebuie înlăturat este înregistrat la momentul capture sau nu. Dacă nu este menționat, valoarea este `false` din oficiu.

## Resurse

- [EventTarget.removeEventListener() | MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
