# Metodele Interfeței `Document`

## Document.adoptNode()

Adoptă un node dintr-un document extern.

## Document.caretPositionFromPoint()

metoda returnează un obiect `CarretPosition` care conține nodul DOM ce conține la rîndul său carret-ul, precum și poziția la care se află.

## `createElement(numeTag, [opțiuni])`

Creează un element pentru care este specificat tipul. Instanța returnată la momentul creării implementează și interfața `Element` (adică este returnat un obiect ca `new` Element), ceea ce permite specificarea oricăror atribute direct folosind obiectul returnat.

Ca parametru introduci numele tag-ului. Vezi că în cazul XML-ului, numele este sensibil la majuscule (case-sensitive).

## createEvent()

Metoda creează un obiect eveniment.

## createNodeIterator()

Metoda creează un obiect `NodeIterator`.

## createProcessingInstruction()

Metoda creează un obiect `Processinginstruction`.

## createRange()

Metoda creează un obiect `Range`.

## `createDocumentFragment()`

Creează un obiect `DocumentFragment` gol. Este returnat un `new DocumentFragment`.

## `createTextNode()`

Creează un nod de `Text` având conținutul specificat printr-un șir de caractere.
Ca parametru primește șirul de caractere.

## createTreeWalker()

Creează un obiect `TreeWalker`.

## elementFromPoint()

Returnează cel mai de sus element de la coordonatele specificate.

## elementsFromPoint()

Returnează un array de elemente de la coordonatele specificate.

## `createComment()`

Creează un node de `Comment` prin returnarea unui nou obiect de tip `Comment`.

## `createCDATASection()`

Creează un nod `CDATASection` care va avea valoarea specificată în parametru.

## `createProcessingInstruction()`

Pentru a crea un astfel de nod trebuie să specifici prin parametri `target`-ul, adică unde vrei să se aplice, și intrucțiunile în sine.

## `createAttribute()`

Creează un atribut de un anume tip specificat prin parametru. După creare, poate fi atașat la un element existent folosind metoda `setAttribute`.

## `createEntityReference()`

Creează un obiect `EntityReference` și primește un parametru care va indica numele acestui `EntityReference`.

## exitPictureInPicture()

Trimite video înapoi în containerul original.

## getAnimations()

Returnează un array al tuturor obiectelor `Animation` care sunt în efect ale căror elemente țintite sunt descendenții documentului.

## getElementsByClassName()

Returnează o listă de elemente care au o anumită clasă.

## getElementById(String id)

Returnează referința către un obiect care care are un id specificat.

## `getElementsByTagName()`

Returnează un `NodeList` al tuturor `Elements` care au un anume nume de tag. Drept parametru, primește numele tagului după care să genereze colecția de `NodeList`. Dacă-i pasezi ca argument caracterul `*`, atunci va genera o colecție cu toate tagurile existente în document.

## getElementsByTagNameNS()

Returnează o listă cu toate elementele cu un anumit tag și namespace.

## getSelection()

Metoda returnează un obiect `Selection` care reprezintă fragmentul de text selectat de utilizator de la poziția curentă a carret-ului.

## importNode()

Returnează o clonă a nodului dintr-un document extern.

## requestStorageAccess()

Returnează un `Promise` care se rezolvă dacă este oferit accesul la un serviciu terț.

## querySelector()metode

Returnează primul element din document care se potrivește cu selectorul/ii CSS specificați ca argumente.

## querySelectorAll()

Returnează o listă cu toate nodurile elementelor care se potrivesc selectorilor CSS specificați.

## Extinderea interfeței `Dcocument` cu `XPathEvaluator`

### Document.createExpression()

Compilează un `XPathExpression` care poate metodefi folosit apoi pentru evaluări repetate.

### Document.createNSResolver()

Creează un obiect `XPathNSResolver`.

### Document.evaluate()

Evaluează o expresie XPath.
