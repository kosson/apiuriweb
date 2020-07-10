# MutationObserver

Este o interfață care oferă posibilitatea de a observa modificări ale arborelui DOM. Intenția este să înlocuiască *Mutation events* din specificațiile DOM3 Events.

## Constructor - MutationObserver()

Creezi un nou MutationObserver care va invoca o funcție callback specifică atunci când apar modificări în DOM. Funcția callback așteaptă ca argument un obiect `MutationRecord`. Acesta va oferi starea elementelor observate.

## Obiectul MutationRecord

Acest obiect reprezintă o mutație petrecută în DOM la un anumit moment. Acest obiect este pasat callback-ului `MutationObserver`.

### Proprietățile lui MutationRecord

#### MutationRecord.type

Tipul este `String`.

Această proprietate returnează:
- atributele (`"attributes"`) mutației în cazul în care mutația s-a petrecut pe unul din atributele unui element.
- `characterData` în cazul în care mutația s-a petrecut pe un nod `CharacterData`.
- `childList` în cazul în care arborele de copii a suferit vreo mutație.

```javascript
let paragraf = document.querySelector('#para'),
    options = {
      attributes: true
    },
    observer = new MutationObserver(clbkM);

function clbkM (mutations) {
  let mutation;
  for (mutation in mutations) {
    if (mutation.type === 'attributes') {
      // prelucrează datele, etc
    }
  };
};

observer.observe(paragraf, options);
```

Un posibil scenariu va implica apelarea callback-ului ori de câte ori se modifică clasa unui element, fie că este adăugată sau ștearsă.

Dacă dorești să lucrezi cu datele tip text ale unui element, ai putea să le observi atunci când acestea se modifică pentru a actualiza versiunea dintr-o posibil bază de date, dacă acest scenariu este unul dorit. Pentru a face acest lucru posibil, trebuie să pui o opțiune în obiectul `options`.

```javascript
let paragraf = document.querySelector('#para'),
    options = {
      characterData: true
    },
    observer = new MutationObserver(clbkM);

function clbkM (mutations) {
  let mutation;
  for (mutation in mutations) {
    if (mutation.type === 'characterData') {
      // prelucrează datele, etc
    }
  };
};

observer.observe(paragraf, options);
```

În cazul textului, trebuie notat faptul că în cazul folosirii atributului global `contenteditable`, în urma interacțiunii cu nodul de text, acesta va fi spart în mai multe noduri de text iar `MutationObserver` nu va mai răspunde cu excepția momentului în care este editat textul considerat a fi parte a nodului original. În cazul în care ștergi integral textul, `MutationObserver` nu va mai apela callback-ul.

#### MutationRecord.target

Tipul este `Node`.



## Metoda `disconnect()`

Oprește o instanță `MutationObserver` din primirea notificărilor până când `observe()` este apelat din nou, dacă este apelat.

## Metoda `observe()`

Semnătura metodei: `mutationObserver.observe(target, options)`. Valoarea pe care o returnează este `undefined`.

Configurează `MutationObserver` ca acesta să înceapă primirea notificărilor prin intermediul funcției callback atunci când apar modificări la DOM ce corespund respectivei opțiuni.
Primul parametru pe care metoda îl primește este elementul DOM pentru care vor fi urmărite proprietățile. Acesta poate fi un element care are copii, fapt care implică observarea tuturor copiilor.
Această metodă primește drept al doilea parametru, un obiect tip dicționar [MutationObserverInit](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserverInit) care configurează observatorul.
Dacă este necesar, se poate apela `observe()` de mai multe ori pe același `MutationObserver` pentru a vedea ce s-a modificat. Totuși acest lucru implică câteva aspecte pe care trebuie să le ai în vedere:
- toți observatorii sunt eliminați din target-uri înainte de a se activa noul observer.
- dacă același `MutationObserver` nu este deja în uz pe target, atunci observatorii existenți nu sunt modificați, fiind adăugați doar cei noi.

### Proprietățile obiectului de configurare

Cel puțin una din proprietățile următoare trebuie să existe pentru a configura observatorul: `childList`, `attributes` și/sau `characterData`. Aceasta trebuie să aibă valoarea `true` la momentul apelării metodei `observe()`. Dacă nu le ai, va fi emisă o excepție `TypeError`.
Toate proprietățile sunt opționale.

#### `subtree`

Setarea la `true`, extinde monitorizarea întregului arbore de dedesubt. Pentru acesta, elementul vizat este `root`. În acest caz, toate proprietățile menționate în obiectul de configurare vor fi setate tuturor elementelor pentru care cel target are rol de `root`.
Valoarea din oficiu este `false`.

#### `childList`

Dacă are setată valoarea `true`, elementul target va fi monitorizat privind adăugarea sau eliminarea de noduri copil.
Valoarea din oficiu este `false`.

#### `attributes`

Setarea la `true` va observa modificările aduse atributelor elementului target și ale copiilor dacă este cazul.
Valoarea din oficiu este `true`, dacă sunt specificate `attributeFilter` sau `attributeOldValue`.

#### `attributeFilter`

Această opțiune permite specificarea strictă a atributelor care trebuie urmărite ignorându-le pe restul.
Acesta este un array al numelor de atribute care să fie monitorizate. Dacă această proprietate nu este introdusă, modificarea tuturor atributelor generează notificări privind mutații.

```javascript
let paragraf = document.querySelector('#para'),
    options = {
      attributes: true,
      attributeFilter: ['hidden', 'contenteditable', 'data-par']
    },
    observer = new MutationObserver(clbkM);

function clbkM (mutations) {
  let mutation;
  for (mutation in mutations) {
    if (mutation.type === 'attributes') {
      // prelucrează datele, etc
    }
  };
};

observer.observe(paragraf, options);
```

De fiecare dată când una dintre atributele menționate îți modifică valoarea, `MutationObserver` va invoca callback-ul. În exemplul de mai sus, în obiectul opțiunilor, valoarea lui `attributes` este setată explicit la `true`. Dar dacă setezi valori în array-ul `attributeFilter`, valoarea lui `attributes` va fi automat setată la `true` din oficiu.

#### `attributeOldValue`

Dacă este setat la `true` se înregistrează valoarea anterioară a unui atribut al unui element monitorizat.
Valoarea din oficiu este `false`.

#### `characterData`

Setarea la valoarea `true`, elementul țintă va fi monitorizat pentru orice modificare a conținutului text sau pentru copii, dacă acesta are rol de `root`.
Valoarea din oficiu este `true` doar dacă `characterDataOldValue` este specificată. În caz contrar, valoarea din oficiu este `false`.

#### `characterDataOldValue`

Dacă este setată la `true`, observatorul va reține vechea valoare text a nodului în cazul în care aceasta se modifică.

## Metoda `takeRecords()`

Metoda elimină toate notificările care sunt în așteptare din coada lui `MutationObserver` și returnează un `Array` nou cu obiecte `MutationRecord`.
Valoarea din oficiu este `false`.

## Apariția excepției TypeError

Circumstanțele în care apare această excepție sunt:

- Atunci când opțiunile sunt configurate de așa manieră încât nimic nu va fi monitorizat, de fapt. De exemplu, `childList`, `attributes` și `characterData` au toate valoarea `false`.
- Toate atributele au valoarea `false`, ceea ce înseamnă că nimic nu va fi monitorizat cu excepția `attributeOldValue` care este `true` și/sau `attributeFilter` este prezentat.
- Opțiunea `characterDataOldValue` are valoarea `true`, dar `characterData` este `false`, indicând că modificările aduse caracterelor nu trebuie să fie urmărite.

## Exemplu

Să pornim de la o listă neordonată pentru care vrem să aflăm când a fost eliminat sau adăugat un element copil.

```html
<ul id="elementul">
  <li>Ceva</li>
  <li>Altceva</li>
</ul>
```

Avem următorul fragment de cod posibil.

```javascript
let targetNode = document.querySelector('#elementul');
let observer = new MutationObserver(callback);

function callback (mutations) {
  // fă prelucrări de date în funcție de modificările apărute
  let mutation;
  for (mutation in mutations) {
    if (mutation.type === 'childList') {
      console.log('Am detectat o modificare. A fost adăugat sau eliminat un nod copil');
    }
  }
}

let obiect_de_configurare = {
  childList: true,
  attributes: true,
  characterData: false,
  subtree: false,
  attributeFilter: ['checked', 'data-ceva'],
  attributeOldValue: false,
  characterDataOldValue: false
};

observer.observe(targetNode, obiect_de_configurare);

// când ai terminat, fă un disconect
observer.disconnect();
```

## Resurse

- [MutationObserver|MDN](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver)
- [Capture DOM Changes with MutationObservers|YouTube](Capture DOM Changes with MutationObservers)
- [DOM MutationObserver – reacting to DOM changes without killing browser performance.|hacks.mozilla.org](https://hacks.mozilla.org/2012/05/dom-mutationobserver-reacting-to-dom-changes-without-killing-browser-performance/)
- [Getting To Know The MutationObserver API|smashingmagazine.com](https://www.smashingmagazine.com/2019/04/mutationobserver-api-guide/)
- [4.3.1. Interface MutationObserver|DOM living standard](https://dom.spec.whatwg.org/#interface-mutationobserver)
