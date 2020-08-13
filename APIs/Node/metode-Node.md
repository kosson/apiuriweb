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

Returnează un `Boolean` care indică dacă elementul are noduri copil.

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

Elimină un nod copil dintre cei ai elementului curent.

```javascript
// eliminarea tuturor copiilor unui nod
function removeAllChildren(element) {
  while (element.firstChild) {
    element.removeChild(element.firstChild)
  }
}
removeAllChildren(document.body); // ca alternativă la `document.body.innerHTML`
```

## Node.replaceChild()

Înlocuiește un `Node` copil al celui curent cu cel oferit drept argument.

## Referințe

- [Node | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node)
