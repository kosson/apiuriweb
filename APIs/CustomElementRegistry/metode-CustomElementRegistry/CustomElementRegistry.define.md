# CustomElementRegistry.define()

Această metodă este cea care permite crearea unui element specific nou.

Este permisă crearea a două elemente specifice:

- elemente specifice autonome (*autonomous custom element*), care sunt elemente de sine stătătoare ce nu moștenesc din elementele HTML existente;
- elemente existente adaptate (*customized built-in element*), care moștenesc și extind elementele HTML existente.

Semnătura: `customElements.define(name, constructor, options);`

## Parametrii

### `name`

Acesta va fi numele noului element. Regula spune că trebuie să conțină o linie, precum în `element-nou`.

### `constructor`

Acesta este constructorul pentru noul element.

### `options`

Este un obiect opțional care controlează modul în care elementul este definit. În acest moment suportul este doar pentru o singură opțiune: `extends`, fiind numele elementului built-in care se dorește a fi extins.
