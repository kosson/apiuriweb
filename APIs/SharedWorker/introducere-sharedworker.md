# Introducere SharedWorker

Aceasta este o interfață ce reprezintă un tip special de worker care poate fi accesat din diferite contexte de navigare. Acestea pot fi ferestre de navigare diferite, iframes sau chiar alți workeri.

Interfața este diferită de a workerilor dedicați și au un global scope diferit - `SharedWorkerGlobalScope`.

SharedWorker moștenește de la `EventTarget`.

Pentru a crea un `SharedWorker` se va folosi constructorul.

```javascript
var myWorker = new SharedWorker('worker.js');
```

## Resurse

- [SharedWorker | MDN](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker)
- [Basic shared worker example | MDN](https://github.com/mdn/simple-shared-worker)
