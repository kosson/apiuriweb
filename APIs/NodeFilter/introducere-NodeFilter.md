# NodeFilter

Interfața `NodeFilter` reprezintă un obiect folosit pentru a filtra nodurile dintr-un `NodeIterator` sau dintr-un `TreeWalker`.

Un `NodeFilter` nu cunoaște nimic despre structura ce urmează a fi parcursă. Browserul nu va oferi un obiect pentru a gestiona filtrarea. Pentru a realiza acest lucru, va trebui să fie redactat un filtru folosind metoda `acceptNode()`, care va fi utilizată în combinație cu un `NodeIterator` pe un `TreeWalker`.

Un filtru poate fi construit folosind și metoda specifică `acceptNode`, care poate returna următoarele valori:

- `NodeFilter.FILTER_ACCEPT`, fiind valoarea pe care metoda `NodeFilter.acceptNode()` o va returna în cazul în care un nod este acceptat;
- `NodeFilter.FILTER_REJECT`, fiind valoarea pe care `NodeFilter.acceptNode()` o returnează în cazul refuzării unui nod. În cazul utilizării conjugat cu `TreeWalker`, toți copii vor fi refuzați ca făcând parte din rezultatul de căutare. În cazul folosirii cu `NodeIterator` această valoare este sinonimă cu `FILTER_SKIP`;
- `NodeFilter.FILTER_SKIP`, fiind valoarea pe care `NodeFilter.acceptNode()` o returnează în cazul saltului făcut de `NodeIterator` sau `TreeWalker` peste anumite noduri. Copiii nodurilor care sunt sărite, încă fac parte din rezultat în interpretarea *sari peste nodul acesta, dar nu peste copiii săi*.

Pentru ilustrare, vom apela la exemplul oferit de MDN.

```javascript
const nodeIterator = document.createNodeIterator(
  // Nodul utilizat ca rădăcină
  document.getElementById('someId'),

  // Ia în considerare doar nodurile care sunt text (nodeType 3)
  NodeFilter.SHOW_TEXT,

  // Un obiect care conține funcția folosită pentru metoda acceptNode sau pentru NodeFilter
  {
    acceptNode: function (node) {
      // Logica pentru a investiga dacă nodul este acceptat, refuzat sau sărit
      // În acest caz, acceptă doar nodurile care au conținut altul decât caracterele whitespace
      if (/\S/.test(node.data)) {
        return NodeFilter.FILTER_ACCEPT;
      }
    }
  },
  false
);

// Arată conținutul fiecărui nod de text care nu este gol și care este copil al rădăcinii
let node;

while ((node = nodeIterator.nextNode())) {
  alert(node.data)
}
```

## Metode

Acest obiect nu moștenește metode de la nicio altă interfață.

### acceptNode()

Metoda returnează un *unsigned short* care va fi folosit pentru a se decide dacă un anumit nod va fi acceptat sau nu de `NodeIterator` sau algoritmul de iterare al lui `TreeWalker`. Este de așteptat ca programatorul să redacteze metoda.

```javascript
var treeWalker = document.createTreeWalker(
  document.body,
  NodeFilter.SHOW_ELEMENT,
  { acceptNode: (node) => {return NodeFilter.FILTER_ACCEPT} },
  false
);

var nodeList = [];
var currentNode = treeWalker.currentNode;

while(currentNode) {
  nodeList.push(currentNode);
  currentNode = treeWalker.nextNode();
}
```

## Realizarea unei filtrări

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

function FindMainSections () {
    var root = document.getElementById ("content"); // stabilește care este rădăcina sub-arborelui

    // verifică dacă există suport pentru crearea unui `TreeWalker`
    if (document.createTreeWalker) {
        // creează obiectul iterator
        objIterator = document.createTreeWalker(root, NodeFilter.SHOW_ELEMENT, check4div, false);

        // obține o referință la primul nod care este un div
        let nodCopil = objIterator.firstChild();
        // parcurge obiectul iterator
        while (nodCopil) {
            alert ("Conținutul nodului copil este: " + nodCopil.innerHTML);
            nodCopil = objIterator.nextSibling ();
        }
    }
    else {
        alert ("Browserul nu are suport pentru TreeWalker");
    }
}
```

## Resurse

- [NodeFilter | MDN](https://developer.mozilla.org/en-US/docs/Web/API/NodeFilter)
