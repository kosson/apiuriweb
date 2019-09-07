# ImageBitmap

Această interfață reprezintă o imagine bitmap care poate fi afișată într-un element `<canvas>`. Această imagine poate fi generată sau constituită din mai multe surse folosindu-se metoda factory `createImageBitmap()`.

Această interfață poate fi folosită și pentru a oferi posibilitatea de a introduce texturi în WebGL.

## Proprietăți

### `ImageBitmap.height`

Este un *unsigned long* care reprezintă înălțimea în pixeli CSS.

### `ImageBitmap.width`

Este un *unsigned long* care reprezintă lățimea în pixeli CSS.

## Metode

### `ImageBitmap.close()`

Șterge toate resursele grafice asociate cu un `ImageBitmap`.
