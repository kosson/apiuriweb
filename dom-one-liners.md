# Expresii eficiente pe o singură linie

## Detectează când s-a făcut scroll la întreaga pagină

```javascript
const scrolledToBottom = () => document.documentElement.clientHeight + window.scrollY >= document.documentElement.scrollHeight;
```

## Scroll la începutul paginii

```javascript
const toTop = () => window.scrollTo(0, 0);
```

## Toggle display pentru elemente

```javascript
const toggle = element => element.style.display = (element.style.display === "none" ? "block" : "none");
```

## Generează o culoare hexazecimală aleatorie

```javascript
const hexColor = () => "#" + Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, '0');
```

## Șterge toate cookie-urile

```javascript
const clearCookies = document.cookie.split(';').forEach(cookie => document.cookie = cookie.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date(0).toUTCString()};path=/`));
```

## Elimină tot codul HTML din pagină

```javascript
const stripHtml = html => (new DOMParser().parseFromString(html, 'text/html')).body.textContent || '';
```

## Detectează modul dark

```javascript
const isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
```
