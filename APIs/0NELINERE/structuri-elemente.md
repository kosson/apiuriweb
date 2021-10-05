## Append la un element

```javascript
target.appendChild(ele);
```

## Verifică dacă un element este descent al altuia

```javascript
const isDescendant = parent.contains(child);
```

## Pornind de la copil, verifică dacă ai părintele căutat

```javascript
// verifică dacă `child` este descendent al lui `parent`
const isDescendant = function (parent, child) {
    let node = child.parentNode;
    while (node) {
        if (node === parent) {
            return true;
        }

        // Parcurge arborele în sus spre părinte
        node = node.parentNode;
    }

    // Ai mers în sus până la rădăcină dar n-ai găsit părintele
    return false;
};
```

## Returnează nodul părinte

```javascript
const parent = ele.parentNode;
```

## Schimbă două elemente între ele

```javascript
const swap = function (nodeA, nodeB) {
    const parentA = nodeA.parentNode;
    const siblingA = nodeA.nextSibling === nodeB ? nodeA : nodeA.nextSibling;

    // Mută `nodeA` înaintea lui `nodeB`
    nodeB.parentNode.insertBefore(nodeA, nodeB);

    // Mută `nodeB` înaintea sibling-ului lui `nodeA`
    parentA.insertBefore(nodeB, siblingA);
};
```

## Nodul anterior și următorul - siblings

```javascript
const prev = ele.previousSibling;
const next = ele.nextSibling;
```

## Obține toate nodurile sibling

```javascript
// Obține nodul părinte
const parent = ele.parentNode;

// Filtrează copilul și exclude elementul
const siblings = [].slice.call(parent.children).filter(function (child) {
    return child !== ele;
});
```
