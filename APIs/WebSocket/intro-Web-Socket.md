# WebSocket

Aceasta este o tehnologie de comunicare bidirecțională interactivă între un broser și un server.

Interfețele pe care acest API le pune la dispoziție:
- `WebSocket`,
- `CloseEvent`,
- `MessageEvent`.

Pentru a crea un socker web simplu se va folosi constructorul.

```javascript
const socket = new WebSocket("ws://ceva.ro");
```

## Resurse

- [The WebSocket Protocol](https://datatracker.ietf.org/doc/html/rfc6455)
- [The WebSocket API (WebSockets) | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
- [WebSocket | javascript.info](https://javascript.info/websocket)
- [How JavaScript works: Deep dive into WebSockets and HTTP/2 with SSE + how to pick the right path | Alexander Zlatkov | Nov 1, 2017](https://blog.sessionstack.com/how-javascript-works-deep-dive-into-websockets-and-http-2-with-sse-how-to-pick-the-right-path-584e6b8e3bf7)
