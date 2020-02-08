# Elemente custom

Aceste elemente sunt create de programator, care spre deosebire de tagurile HTML cu care suntem obișnuiți deja, au o liniuță precum în `<nou-element>`.

Elementele custom pot avea propria semnatică. Realizarea de elemente particularizate, de fapt implică realizarea unei adevărate componente de pagină web.

De exemplu, să presupunem că dorim ca de fiecare dată când introducem un nou element `<ceva-nou>`, să fie afișat un paragraf de text.

```html
<ceva-nou></ceva-nou>
```

Acest nou element are nevoie de cod în JavaScript pentru a produce efectul necesar. În acest sens, se va face o extindere a interfeței `HTMLElement`.

## Resurse

- [An Introduction to Web Components | css-tricks.com](https://css-tricks.com/an-introduction-to-web-components/)
- [4.13 Custom elements | HTML Living standard](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements)
