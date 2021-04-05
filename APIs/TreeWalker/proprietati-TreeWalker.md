# Proprietăți TreeWalker

## TreeWalker.root

Aceasta este o proprietate read-only care reprezintă nodul rădăcină așa cum a fost specificat la momentul creării obiectului `TreeWalker`.

## TreeWalker.whatToShow

Returnează un număr *unsigned long* care este un bitmask constituit din constante ale lui `NodeFilter`. Oferă o descriere a tipurilor de `Node`-uri care pot fi filtrate în funcție de ceea ce ai nevoie. Valoarea din oficiu este `0xFFFFFFFF`, care reprezintă constanta `SHOW_ALL`.
Nodurile care nu se potrivesc nu sunt luate în considerare.

|Constantă| Valoare numerică | Descriere |
|-:|:-|:--|
|NodeFilter.SHOW_ALL|`-1` care este maximum unui unsigned long|Arată toate nodurile|
|NodeFilter.SHOW_ATTRIBUTE (depreciat)|2|Aduce nodurile `Attr`, fiind util doar atunci când constitui un subarbore având un nod `Attr` drept rădăcină.|
|NodeFilter.SHOW_CDATA_SECTION (depreciat)|8|Arată nodurile `CDATASection`|
|NodeFilter.SHOW_COMMENT|128|Arată nodurile `Comment`|
|NodeFilter.SHOW_DOCUMENT|256|Arată nodurile `Document`|
|NodeFilter.SHOW_DOCUMENT_FRAGMENT|1024|Arată noduri `DocumentFragment`|
|NodeFilter.SHOW_DOCUMENT_TYPE|512|Arată nodurile `DocumentType`|
|NodeFilter.SHOW_ELEMENT|1|Arată nodurile `Element`|
|NodeFilter.SHOW_ENTITY (depreciat)|32|Arată noduri `Entity`, fiind util atunci când creezi obiecte `TreeWalker` având un `Entity` drept rădăcină.|
|NodeFilter.SHOW_ENTITY_REFERENCE (depreciat)|16|Arată nodurile `EntityReference`|
|NodeFilter.SHOW_NOTATION (depreciat)|2048|Arată noduri `Notation`, fiind util doar atunci când constitui obiecte `TreeWalker` având un `Notation` drept rădăcină|
|NodeFilter.SHOW_PROCESSING_INSTRUCTION|64|Arată moduri `ProcessingInstruction`|
|NodeFilter.SHOW_TEXT|4|Arată noduri `Text`|

## TreeWalker.filter

Returnează obiectul `NodeFilter` folosit pentru a selecta nodurile relevante. Acest obiect are o metodă `acceptNode` care este apelată de `TreeWalker` pentru a determina dacă un nod care a trecut de `whatToShow` este acceptat sau nu.

## TreeWalker.currentNode

Este `Node`-ul la care se referă curent `TreeWalker`.
