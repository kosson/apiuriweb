# TreeWalker

Acest obiect reprezintă nodurile dintr-un arbore secundar al unui document și o poziție din acesta. Cee ce obții este un obiect iterator care conține toate elementele sub-arborelui, inclusiv elementul root.

Interfețele înrudite sunt `NodeFilter` și `NodeIterator`. Un `TreeWalker` poate fi obținut folosind metoda `Document.createTreeWalker()` (vezi metodele lui `Document`). Metodele pe care le poți folosi pentru a face o traversare a sub-arborelui sunt următoarele:

- `firstChild()`;
- `lastChild()`;
- `nextNode()`;
- `nextSibling()`;
- `parentNode()`;
- `previousNode()`;
- `previousSibling()`.

Mai beneficiem și de o proprietate foarte utilă numită `currentNode` care indică poziția, adică nodul la care a ajuns iterarea la momentul parcurgerii unui iterator `TreeWalker`.

## Semnătura

```javascript
document.createTreeWalker(root[, whatToShow[, filter[, entityReferenceExpansion]]]);
```

## Parcurgerea simplă a unei structuri

Iterarea se pornește cu primul element care este însuși elementul rădăcină. Pentru referiță, vom crea o structură pe care să o parcurgem.

```html
<section id="gazda">
  <div class="alb">
    <p>Test de alb <span>1</span></p>
  </div>
  <div class="negru">
    <p>Test de negru <span>2</span></p>
  </div>
  <div class="alb">
    Doar text
  </div>
</section>
```

Pentru care vom crea un obiect iterabil folosindu-ne de `TreeWalker`.

```javascript
function AfiseazaElementeleStructurii () {
  const root = document.getElementById('gazda');

  if (document.createTreeWalker) {
    // constituie obiectul iterator
    const objIterator = document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT, null, false);

    // obține o referință către elementul rădăcină dacă ai nevoie de acesta
    const elemRoot = objIterator.currentNode; // poți afla care este făcând un chain cu `.tagName`

    // parcurge obiectul
    while (objIterator.nextNode()) {
      alert(objIterator.currentNode.tagName);
    }

    // pentru că am terminat de parcurs structura, reseteaz-o de la capăt
    objIterator.currentNode = root;
  }

}
```

Ceea ce trebuie remarcat este faptul că putem utiliza metode și proprietăți ale elementelor în timp ce parcurgem obiectul iterator. O problemă care ar putea apărea și care poate fi ușor corectată este calcularea de către `TreeWalker` a tuturor nodurilor existente în care sunt incluse și cele de text. Acestea sunt adăugate elementelor distincte.

```html
<ul id="lista">
  <li>Unu</li>
  <li>Doi</li>
  <li>Trei</li>
</ul>
```

O numărătoare a tuturor nodurilor va aduce valoarea 7 pentru că sunt luate în considerare și cele text.

```javascript
const root = document.getElementById('lista');
const objIterator = document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT, null, false);
alert(objIterator.currentNode.childNodes.length); // 7
alert(objIterator.currentNode.getElementsByTagName("*").length); // 3
```

## Manipularea conținuturilor unei structuri

Să presupunem că avem un fragment de HTML care gestionează o frază folosind mai multe elemente. Putem folosi un obiect `TreeWalker` pentru a obține o altă formă a acesteia.

```html
<p id="fraza">
  Am crezut că <span>performanțele</span> se obțin <em>ușor</em>.
</p>
```

Folosind structura de mai sus putem remodela conținutul pentru a avea o versiune *curată*.

```javascript
let root = document.getElementById('fraza');
function remodelare () {
  const objIterator = document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT, null, false);
  // avansează cursorul iteratorului la primul element din interiorul celui rădăcină. Nu uita că lucrăm cu un iterator.
  objIterator.firstChild(); // Iteratorul se află acum pe elementul de tip text al cărui conținut este "Am crezut că "
  // constituim un string care ne va servi la colectarea tuturor componentelor
  let curat = objIterator.currentNode.nodeValue; // am legat `curat` la valoarea "Am crezut că "
  // parcurgem iteratorul pe aceeași ramură
  while (objIterator.nextSibling()) {
    curat += objIterator.currentNode.nodeValue; // adaugă fragmentul de text
  }
  return curat; // Vom obține fraza curată
};
```

## Utilizarea unui obiect TreeWalker cu filtrare

Valoarea obiectului `TreeWalker` se dovedește din filtrarea cu ușurință a nodurilor unui document. Folosirea lui `NodeFilter.SHOW_ELEMENT` la care am apelat anterior, se dovedește a fi un punct de pornire.

Un alt exemplu este parcurgerea unui sub-arbore pentru care se creează o funcție helper pentru a detecta tipul elementului și luarea în considerare doar a celui dorit.

```javascript
// funcția helper pentru filtrare
function check4div (node) {
    // În cazul apariției tipului de tag div, elementul este acceptat
    if (node.tagName.toLowerCase() == 'div') {
        return NodeFilter.FILTER_ACCEPT;
    }
    // în caz contrar, elementul este sărit
    return NodeFilter.FILTER_SKIP;
}

function ParcurgeStructura () {
    const root = document.getElementById ("content"); // stabilește care este rădăcina sub-arborelui

    // verifică dacă există suport pentru crearea unui `TreeWalker`
    if (document.createTreeWalker) {
        // creează obiectul iterator. în cazul în care nu se dorește filtrarea, al treilea argument va avea valoarea `null`
        objIterator = document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT, check4div, false);

        // obține o referință la primul nod care este un div
        let nodCopil = objIterator.firstChild();
        // parcurge obiectul iterator
        while (nodCopil) {
            alert ("Conținutul nodului copil este: " + nodCopil.innerHTML);
            nodCopil = objIterator.nextSibling();
        }
    }
    else {
        alert ("Browserul nu are suport pentru TreeWalker");
    }
}
```

Un alt exemplu oferit de [javascriptkit.com](http://www.javascriptkit.com/dhtmltutors/treewalker2.shtml) prin care se pot ascunde elemente în baza unei funcții de filtrare.

```javascript
let filtreaza = function (nod) {
  if (nod.tagName === 'DIV' || nod.tagName === 'IMG') {
    return NodeFilter.FILTER_ACCEPT;
  } else {
    return NodeFilter.FILTER_SKIP;
  }
};
var objIterator = document.createTreeWalker(document.body, NodeFilter.SHOW_ELEMENT, filtreaza, false)
while (objIterator.nextNode()) {
  objIterator.currentNode.style.display = 'none'; // ascunde toate div-urile și imaginile.
}
```

## Resurse

- [1. Document Object Model Traversal](https://www.w3.org/TR/DOM-Level-2-Traversal-Range/traversal)
