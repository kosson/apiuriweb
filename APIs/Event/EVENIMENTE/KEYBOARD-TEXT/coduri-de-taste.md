# Coduri de taste

Pentru evenimentele `keydown` și `keyup`, proprietatea `keyCode` a obiectului `event` indică o valoare numerică corespondentă tastei care a declanșat evenimentul.

```javascript
let textbox = document.getElementById("myText");
textbox.addEventListener("keyup", (event) => {
  console.log(event.keyCode); // afișează codul
});
```

Pentru a prelua corect codul de tastă în compatibilitate cu browserele mai vechi, ar putea fi utilizată o secvență utilă precum cea de mai jos. Să presupunem că avem un formular de căutare.

```javascript
/* === CĂUTAREA UNUI UTILIZATOR === */
var findUser = document.getElementById('findUser');
var findUserBtn = document.querySelector("#findUserBtn");

/* === CERE PROFILUL USERULUI === */
function clbkFindUser (evt) {
    evt.preventDefault();
    pubComm.emit('person', document.querySelector('#findUserField').value);
}
findUserBtn.addEventListener('click', clbkFindUser);
findUser.addEventListener('keypress', (evt) => {
    let charCodeNr = typeof evt.charCode == "number" ? evt.charCode : evt.keyCode;
    console.log('Caracter ', charCodeNr);
    let identifier = evt.key || evt.keyIdentifier; // compatibilitate cu Safari
    if (identifier === "Enter" || charCodeNr === 13) {
        pubComm.emit('person', document.querySelector('#findUserField').value);
    };
});
```

Evenimentul `keypress` generează următoarele coduri numerice pentru tastele speciale.

| KEY | KEY CODE |
|-:|-|
| Backspace | 8 |
| Numpad 8 | 104 |
| Tab | 9|
| Numpad 9 | 105 |
| Enter | 13|
| Numpad + | 107 |
| Shift | 16 |
| Minus (Numpad sau normal) | 109 |
| Ctrl | 17 |
| Numpad . | 110 |
| Alt | 18 |
| Numpad / | 111 |
| Pause/Break | 19 |
| F1 | 112 |
| Caps Lock | 20 |
| F2 | 113 |
| Esc | 27 |
| F3 | 114 |
| Page Up | 33 |
| F4 | 115 |
| Page Down | 34 |
| F5 | 116 |
| End | 35 |
| F6 | 117 |
| Home | 36 |
| F7 | 118 |
| Left Arrow | 37 |
| F8 | 119 |
| Up Arrow | 38 |
| F9 | 120 |
| Right Arrow | 39 |
| F10 | 121 |
| Down Arrow | 40 |
| F11 | 122 |
| Ins | 45 |
| F12 | 123 |
| Del | 46 |
| Num Lock | 144 |
| Left Windows Key | 91 |
| Scroll Lock | 145 |
| Right Windows Key | 92|
| Semicolon (IE/Safari/Chrome) | 186|
| Context Menu Key | 93 |
| Semicolon (Opera/FF) | 59 |
| Numpad 0 | 96
| Less than | 188 |
| Numpad 1 | 97|
| Greater than | 190 |
| Numpad 2 | 98 |
| Forward slash | 191 |
| Numpad 3 | 99 |
| Grave accent ( ' ) | 192 |
| Numpad 4 | 100 |
| Equals | 61 |
| Numpad 5 | 101 |
| Left Bracket | 219 |
| Numpad 6 | 102 |
| Back slash (\\\) | 220 |
| Numpad 7 | 103 |
| Right Bracket | 221 |
| Single Quote | 222 |

DOM Level 3 Events oferă două proprietăți pentru obiectul `event` privitor la taste: `key` și `char`. Proprietatea `key` are în intenție înlocuirea lui `keyCode` și va conține un șir de caractere.
