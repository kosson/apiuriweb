## Obține textul selectat

```javascript
const getSelectedText = () => window.getSelection().toString();
```

## Elimină tot codul HTML din pagină

```javascript
const stripHtml = html => (new DOMParser().parseFromString(html, 'text/html')).body.textContent || '';
```

## Resurse

- [HTML DOM](https://htmldom.dev/)
