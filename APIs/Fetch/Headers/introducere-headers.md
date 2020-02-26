# Headers

Acest obiect este unul asemănător celor de tip `Map`. Un obiect `Header` au un *header list*, care este inițial goală. Atenție, acest obiect în al său *header list* nu poate avea decât o singură înregistrare `Set-Cookie`. Pentru a face o cerere pentru care ai nevoie să setezi un header, acesta poate fi pasat ca membru în obiectul de configurare a lui `fetch`.

```javascript
let dateExterne = fetch(UrlProtejat, {
    headers: {
        Authentication: 'unToken'
    }
});
```

Există un set de headere care nu pot fi setate:

- `Accept-Charset`, `Accept-Encoding`
- `Access-Control-Request-Headers`
- `Access-Control-Request-Method`
- `Connection`
- `Content-Length`
- `Cookie`, `Cookie2`
- `Date`
- `DNT`
- `Expect`
- `Host`
- `Keep-Alive`
- `Origin`
- `Referer`
- `TE`
- `Trailer`
- `Transfer-Encoding`
- `Upgrade`
- `Via`
- `Proxy-*`
- `Sec-*`
