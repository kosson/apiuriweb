# Metode Node

În afară de propriile metode, `Node` moștenește toate metodele de la părintele `EventTarget`.

## Node.appendChild(childNode)

Adaugă copilul specificat prin argument ca ultim copil al nodului curent.
Dacă argumentul este o referință către un nod care există deja în DOM, acesta va fi detașat de unde este și reatașat în noua poziție.

## Node.cloneNode()

Clonează un nod și opțional întregul său conținut. Din oficiu, va fi clonat doar conținutul nodului.

## Node.compareDocumentPosition()

Compară poziția nodului curent cu cea a altui nod din oricare alt document.

## Node.contains()

Returnează un `Boolean` care indică dacă nodul este sau nu un descendent a celui pe care se aplică metoda.

## Node.getRootNode()

Returnează rădăcina obiectului context, care, opțional, poate să includă și shadow root-ul, dacă acesta este disponibil.

## Node.hasChildNodes()

Metoda returnează un `Boolean` care indică dacă elementul are noduri copil.

O posibilă aplicație oferită de MDN este parcurgerea recursivă a copiilor unui nod. Această aplicație utilă implică metoda, dar și proprietatea `Node.childNodes`.

```javascript
function eachNode(rootNode, callback) {
  // cazul în care nu ai un callback
	if (!callback) {
		const nodes = [];
    // pentru fiecare nod, callbackul va completa
		eachNode(rootNode, function (node) {
			nodes.push(node); // adaugă în colecția de noduri
		})
		return nodes; // returnează colecția dacă nu ai callback
	}

  // dacă nu pasezi funcție, `callback` va fi undefined
	if (false === callback(rootNode)) {
		return false; // returnează `false` doar când callback-ul returnează false
  }

  // în cazul în care nodul pasat drept prim argument are copii
	if (rootNode.hasChildNodes()) {
		const nodes = rootNode.childNodes; // constituie lista dinamică
    // parcurge lista recursiv pentru fiecare element
		for (let i = 0, l = nodes.length; i < l; ++i) {
			if (false === eachNode(nodes[i], callback)) {
        // dacă evaluarea callback-ului returnează valoarea false,
        // se iese din ciclare prin return și se reia ciclarea la nivelul părinte
        // poate fi utilizat pentru momentul în care un anumit string este identificat, ș.a.m.d.
				return;
      }
    }
	}
}
```

Tot MDN oferă un exemplu de funcție wrapper care folosește funcționalitatea dezvoltată prin exemplul anterior (`eachNode`), pentru a căuta un fragment de text într-un document.

```javascript
function grep(parentNode, pattern) {
	const matches = [];
	let endScan = false;

	eachNode(parentNode, function (node) {
    // în cazul în care am terminat pe acest nivel, continuă mai sus cu părinții
		if (endScan) {
			return false;
    }

		// Ignoră nodurile care nu sunt noduri text
		if (node.nodeType !== Node.TEXT_NODE) {
			return;
    }

    // cazul în care pasezi direct un string
		if (typeof pattern === "string") {
			if (-1 !== node.textContent.indexOf(pattern)) {
				matches.push(node);
      }
    // cazul în care pasezi un pattern
		} else if (pattern.test(node.textContent)) {
      // în cazul în care pattern-ul nu are atributul global setat
			if (!pattern.global) {
				endScan = true; // ieși după această iterație.
				matches = node; // cu singurul rezultat găsit
			} else {
        matches.push(node);
      }
		}
	})

	return matches;
}

const typos = ["teh", "adn", "btu", "adress", "youre", "msitakes"];
const pattern = new RegExp("\\b(" + typos.join("|") + ")\\b", "gi");
const mistakes = grep(document.body, pattern);
console.log(mistakes);
```

## Node.insertBefore()

Inserează un `Node` înaintea nodului pe care se aplică metoda. Nodul inserat va fi copil al celui părinte.

## Node.isDefaultNamespace()

Acceptă un URI de namespace ca argument și returnează un `Boolean` cu valoarea `true` dacă respectivul namespace este cel din oficiu pentru respectivul nod și `false` în caz contrar.

## Node.isEqualNode()

Returnează o valoare `Boolean` care indică dacă două noduri sunt de același tip și dacă datele definitorii sunt la fel.

## Node.isSameNode()

Returnează o valoare `Boolean` care indică dacă cele două noduri sunt similare sau nu în sensul că fac referință către același obiect.

## Node.lookupPrefix()

Returnează un `DOMString` cu prefixul pentru URI-ul unui namespace dat, dacă acesta este prezent. În caz contrar, valoarea returnată este `null`. Atunci când sunt posibile mai multe prefixe, rezultatul depinde de implementare.

## Node.lookupNamespaceURI()

Acceptă un prefix și returnează URI-ul unui namespace asociat cu acesta pentru nodul respectiv, dacă acesta este găsit. În caz contrar, valoarea returnată este `null`. Dacă se introduce `null` ca argument pentru prefix, va fi returnat namespace-ul din oficiu.

## Node.normalize()

Curăță nodurile text de sub elementul pe al cărui nod se aplică metoda. Rezultatul va fi adunarea celor alăturate, eliminarea de spații, etc.

## Node.removeChild()

Metoda este folosită pentru a elimina din DOM un element. Nodurile sunt întotdeauna copilul unui element din DOM (`parentNode`).

```javascript
let childNode = parentNode.removeChild(childNode);
```

Atunci când elementul este eliminat din DOM, acesta va fi menținut în memorie. Dacă dorești distrugerea obiectului de către colectorul de gunoi (*garbage colector*), folosește aceeași sintaxă fără a mai ține o referință către obiect.

```javascript
parentNode.removeChild(childNode);
```

Obiectul va mai fi ținut în memorie până când colectorul de gunoi îl va elimina.

### Eliminarea atunci când cunoști părintele

Având următoarea structură

```html
<div id="top">
  <div id="nested"></div>
</div>
```

Ai putea șterge folosind următoarea secvență.

```javascript
let d = document.getElementById("top");
let d_nested = document.getElementById("nested");
let throwawayNode = d.removeChild(d_nested);
```

### Eliminare atunci când nu cunoști părintele

```javascript
let node = document.getElementById("nested");
if (node.parentNode) {
  node.parentNode.removeChild(node);
}
```

### Elimină un nod copil dintre cei ai elementului curent

```javascript
// eliminarea tuturor copiilor unui nod
function removeAllChildren(element) {
  while (element.firstChild) {
    element.removeChild(element.firstChild);
  }
}
removeAllChildren(document.body); // ca alternativă la `document.body.innerHTML`
```

Metoda returnează elementul care a fost eliminat.

## Node.replaceChild()

Înlocuiește un `Node` copil al celui curent cu cel oferit drept argument.

## Referințe

- [Node | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node)
