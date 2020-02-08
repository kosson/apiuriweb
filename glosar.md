# Glosar

## N

### Node

Un `Node` este un punct unic al arborelui de noduri. Entitățile care pot fi noduri sunt însuși documentul, elementele, etc. Obiecte care pot fi noduri:

- `Document`,
- `DocumentType`,
- `DocumentFragment`,
- `Element`,
- `Text`,
- `ProcessingInstruction` și
- `Comment`.

Aceste noduri participă în ceea ce se numește *arbore*. Arborele format de mai multe noduri se numește **node tree**.

Standardul DOM menționează un alt arbore, care se numește **document tree**. Acesta este un arbore a cărui rădăcină este un `document`.

Mai multe noduri, care sunt copii altuia, formează un obiect dinamic (orice modificare se reflectă instantaneu în alcătuirea sa) numit `NodeList`. Pentru a contitui acest obiect, se pot folosi:

- `Node.childNodes` sau
- `document.querySelectorAll()`.

#### Resurse

- [4.2. Node tree | DOM Living Standard](https://dom.spec.whatwg.org/#concept-node)

## Resurse

- [MDN Web Docs Glossary: Definitions of Web-related terms](https://developer.mozilla.org/en-US/docs/Glossary)
