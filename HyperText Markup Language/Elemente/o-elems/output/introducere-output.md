# Elementul output

Este un container în care un site sau o aplicație poate injecta rezultatele unui calcul sau ale interacțiunii utilizatorului cu anumite alte elemente din pagină.

```html
<form oninput="result.value=parseInt(a.value)+parseInt(b.value)">
  <input type="range" id="b" name="b" value="50" /> +
  <input type="number" id="a" name="a" value="10" /> =
  <output name="result" for="a b">60</output>
</form>
```

## Atribute

### `for`

Este o listă de elemente separate prin spații ale id-urilor unor elemente, ceea ce indică că acele elemente vor contribui cu intrări în `output`.

### `form`

Este elementul `form` cu care este asociat elementul `output`. Altfel spus, care form îl deține. Valoarea trebuie să fie id-ul formului. Dacă nu este precizat, valoarea va fi asociată automat cu cel mai apropiat părinte `form`.

Acest atribut permite asocierea unui output oriunde în pagină, fără a-l limita doar la existența în `form`.

### `name`

Este numele elementului.

## Resurse

- [<output>: The Output element | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/output)
