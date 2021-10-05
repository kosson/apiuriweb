## Curăță toate cookie-urile

```javascript
const clearCookies = () => document.cookie
  .split(';')
  .forEach((c) =>(document.cookie = c.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date().toUTCString()};path=/`)));

// sau

const clearCookies = document.cookie.split(';').forEach(cookie => document.cookie = cookie.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date(0).toUTCString()};path=/`));
```

## Convertește cookie la obiect

```javascript
const cookies = document.cookie.split(';').map((item) => item.split('=')).reduce((acc, [k, v]) => (acc[k.trim().replace('"', '')] = v) && acc, {});
```

## Resurse

- [HTML DOM](https://htmldom.dev/)
