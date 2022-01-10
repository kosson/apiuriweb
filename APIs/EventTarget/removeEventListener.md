# EventTarget.removeEventListener()

Metoda șterge un *event listener* dintr-un obiect de tip `EventTarget` care a fost înregistrat folosind `EventTarget.addEventListener()`. Receptorul care trebuie eliminat poate fi identificat folosind combinații ale tipului de eveniment căruia îi este asociat, identificatorul funcției în sine, ș.a.m.d.

Motivul pentru care un eveniment trebuie eliminat ține de resursele pe care le *blochează*. În momentul în care evenimentele sunt atribuite elementelor, o conexiune se formează între codul browserului și codul JavaScript. Cu cât sunt mai multe astfel de conexiuni, cu atât pagina va rula mai greu. Pentru a contracara aceste pierderi de performanță, se poate apela la *event delegation*, iar cea de-a doua metodă este aceea de a elimina event handler-urile dacă nu mai sunt folosite.

Aceste probleme apar în două momente ale ciclului de viață al paginii. Primul este atunci când un element este eliminat din DOM (`removeChild` sau `replaceChild`), dar care încă avea atașat un event handler. Iar al doilea este atunci când folosești `innerHTML` pentru a înlocui porțiuni de pagină. Toți receptorii vor ține o legătură la variabilele din scope și astfel, va fi împiedicată colectarea la gunoi. Pentru a preveni acest lucru, se va aplica `removeEventListener` sau elementul DOM asociat este eliminat.

Cel mai rapid este să setezi handler-ul la valoarea `null`: `buton.onclick = null;`.

Este o bună practică să elimini toate event handler-urile înainte ca pagina să fie *unloaded*, folosind chiar evenimentul `onunload`.

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
- [Causes of Memory Leaks in JavaScript and How to Avoid Them](https://www.ditdot.hr/en/causes-of-memory-leaks-in-javascript-and-how-to-avoid-them)
