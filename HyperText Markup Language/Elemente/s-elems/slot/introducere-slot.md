# Elementul slot

Acest element împreună cu `template` face parte din suita de tehnologii numită *Web components*. Elementul `slot` este folosit pentru a rezerva un loc într-o componentă web. Acest loc va primi propria structură de markup. Acest lucru permite introducerea de structuri arborescente DOM pentru a le prezenta într-un singur document unificator.

Are o singură proprietate `name` care indică numele slotului.

Un exemplu de folosire ar fi o structură care declară sloturile ce vor primi date definite în componenta dedicată.

```html
<div class="carte">
  <div class="coperta">
    <slot name="coperta"></slot>
  </div>
  <slot name="titlu"></slot>
  <slot name="autor"></slot>
</div>
```

Creăm componenta similar codului următor.

```html
<carte-data>
  <img src"cuore.jpg" slot="coperta">
  <span slot="titlu">Cuore</span>
  <span slot="autor">Edmondo De Amicis</span>
</carte-data>
```

Structura pe care o obții la final este.

```html
<div class="carte">
  <div class="coperta">
    <slot name="coperta">
      <img src"cuore.jpg" slot="coperta">
    </slot>
  </div>
  <slot name="titlu">
    <span slot="titlu">Cuore</span>
  </slot>
  <slot name="autor">
    <span slot="autor">Edmondo De Amicis</span>
  </slot>
</div>
```

## Referințe

- [slot | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/slot)
- [Web components | MDN](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
