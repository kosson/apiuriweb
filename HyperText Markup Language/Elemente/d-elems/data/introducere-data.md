# Elementul data

Acest element face o legătură a unui element cu datele care sunt citite doar de mașină.

```html
<ul>
  <li>
    <data value="ceva">Text</data>
  </li>
</ul>

<ul>
 <li><data id="x" value="398" data-y="bau" data-c="10">Mini Ketchup</data></li>
 <li><data value="399">Jumbo Ketchup</data></li>
 <li><data value="400">Mega Jumbo Ketchup</data></li>
</ul>
```

Atunci când aceste tag-uri sunt combinate cu atribute ce reprezintă microdate, elementul oferă posibilitatea mașinii să citească valoarea (*machine-readable*), iar userului o valoare (*human-readable*) care să o poată afișa.

Formatul folosit pentru valoarea lui `value` este determinat de vocabularul microformatelor și al microdatelor utilizate. Valoarea atributului `value` trebuie să reflecte conținutul tag-ului.

Majoritatea motoarelor de căutare indexează și microdatele pe care le întâlnesc.

În cazul în care valoarea este o dată calendaristică, se va folosi tag-ul `<time>`.

## Resurse

- [HTML Living standard](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-data-element)
- [<data> | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/data)
