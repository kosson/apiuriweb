## Detectează când s-a făcut scroll la întreaga pagină

```javascript
const scrolledToBottom = () => document.documentElement.clientHeight + window.scrollY >= document.documentElement.scrollHeight;
```

## Scroll la începutul paginii

```javascript
const toTop = () => window.scrollTo(0, 0);
```
