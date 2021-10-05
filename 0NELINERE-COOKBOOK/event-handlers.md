## Atașarea și detașarea unui event handler

Folosirea atributului `on` nu este recomandabilă pentru că nu poți atașa decât un singur handler la un eveniment.

```javascript
ele.onclick = function() {
    ...
};

// Șterge event handler
delete ele.onclick;
```

Un alt dezavantaj este că o astfel de opțiune, să zicem `onclick` va suprascrie orice alt event handler pentru evenimentul `click` care există deja.

## Folosirea metodei `addEventListener`

```javascript
const handler = function() {
    ...
};

// Atașează handler evenimentului `click`
ele.addEventListener('click', handler);

// Detașează handlerul de pe evenimentul `click`
ele.removeEventListener('click', handler);
```

## Creează un handler care să fie acționat o singură dată

```javascript
const handler = function (e) {
    // ...
};

ele.addEventListener('nume-event', handler, { once: true });
```

Din nefericire această opțiune nu are suport pentru IE11.

## Handler care se autoelimină

```javascript
const handler = function (e) {
    // Codul event handlerului
    // ...

    // La final, șterge-l!
    e.target.removeEventListener(e.type, handler);
};

ele.addEventListener('nume-event', handler);
```
