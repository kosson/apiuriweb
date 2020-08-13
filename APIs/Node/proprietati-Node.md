# Proprietățile interfeței Node

Interfața `Node` pe lângă proprietățile sale, mai moștenește și din `EventTarget`.

## Node.baseURI

Este o proprietate read-only.
Returnează un `DOMString` care reprezintă URL-ul de bază a documentului care conține nodul.

Ref:
- [baseURI | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/baseURI)

## Node.childNodes

Este o proprietate read-only.
Returnează un `NodeList` live cu toți copiii nodului curent. Pentru că este live, obiectul `NodeList` va fi actualizat pentru fiecare modificare care apare.

## Node.firstChild

Este o proprietate read-only.
Returnează un `Node` care reprezintă primul copil al nodului curent sau `null` dacă nu există vreunul.

## Node.isConnected

Este o proprietate read-only.
Este o valoare `Boolean` care indică dacă nodul este conectat (direct sau indirect) la obiectul context, adică la obiectul `Document` în cazul DOM-ului sau la `ShadowRoot` în cazul unui shadow DOM.

## Node.lastChild

Este o proprietate read-only.
Returnează ultimul copil al nodului curent sau `null`, dacă nu există vreunul.

## Node.nextSibling

Este o proprietate read-only.
Returnează un `Node` care reprezintă următorul nod din arbore sau `null` dacă nu există vreunul.

## Node.nodeName

Este o proprietate read-only.
Returnează un `DOMString` care conține numele nodului. Numele va avea o structură care variază în funcție de tipul nodului. De exemplu, un nod `Text` va avea un string `#text`, iar un nod `Document` va avea un string `#document`.

## Node.nodeType

Returnează un `short` care reprezintă tipul nodului.

| Nume | Valoare |
|:--:| :--: |
| ELEMENT_NODE | 1 |
| TEXT_NODE | 3 |
| CDATA_SECTION_NODE | 4 |
| PROCESSING_INSTRUCTION_NODE | 7 |
| COMMENT_NODE | 8 |
| DOCUMENT_NODE | 9 |
| DOCUMENT_TYPE_NODE | 10 |
| DOCUMENT_FRAGMENT_NODE | 11 |

## Node.nodeValue

Returnează sau setează valoarea nodului curent.

## Node.ownerDocument

Este o proprietate read-only.
Returnează `Document`-ul de care ține nodul. Dacă nodul în sine este un alt document, este returnat `null`.

## Node.parentNode

Este o proprietate read-only.
Returnează un `Node` care este părintele nodului curent. Dacă nu există un astfel de nod, cel curent făcând parte din cei din top, sau nu face parte dintr-un arbore, proprietatea returnează valoarea `null`.

## Node.parentElement

Este o proprietate read-only.
Returnează un `Element` care este părintele acestui nod. Dacă nodul nu are părinte sau dacă acel părinte nu este `Element`, această proprietate va returna `null`.

## Node.previousSibling

Este o proprietate read-only.
Returnează un `Node` care reprezintă nodul anterior din arbore sau `null` dacă nu există un astfel de nod.

## Node.textContent

Returnează sau setează conținutul textual al unui element și a tuturor descendenților acestuia.


## Referințe

- [Node | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node)
