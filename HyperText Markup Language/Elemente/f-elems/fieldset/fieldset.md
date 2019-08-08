# Elementul `fieldset`

Acest element este folosit pentru a grupa împreună un set de controale ale unui formular.

```html
<form>
  <fieldset>
    <legend>Alege regnul</legend>

    <input type="radio" id="ceva" name="animal">
    <label for="ceva">Lumea animalelor</label><br/>

    <input type="radio" id="altceva" name="vegetal">
    <label for="altceva">Lumea plantelor</label><br/>

  </fieldset>
</form>
```

## Atributele elementului fieldset

### `disabled`

Acest atribut poate fi setat cu o valoare `Boolean`, ceea ce va conduce la setarea tuturor elementelor descendente în cascadă.
Atunci când avem atributul `disabled` setat la `false`, toate elementele descendent, nu vor putea fi editate. Spre deosebire de elementele individuale din formular cărăra li se aplică `disabled` la `false` și nu sunt trimise datele, cele din fieldset, chiar dacă sunt `disabled`, va fi permisă trimiterea datelor la momentul submit.

### `form`

Acest atribut poartă valoarea id-ului setat pentru formularul din care face parte `fieldset`-ul, chiar dacă nu este introdus în formular în codul HTML.

### `name`

Este numele asociat cu prezentul set de elemente strâns în `fieldset`.
