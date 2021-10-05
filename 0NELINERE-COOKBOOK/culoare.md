## Generează o culoare hexazecimală aleatorie

```javascript
const hexColor = () => "#" + Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, '0');
```

## Detectează modul dark

```javascript
const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
```
