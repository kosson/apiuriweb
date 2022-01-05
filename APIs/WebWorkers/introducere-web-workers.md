# Web Workers

Acesta este un mecanism pe care browserul îl pune la dispoziție pentru a rula programe JavaScript într-un thread separat de cel al aplicației web din pagină. Acest lucru permite executarea unor operațiuni care necesită o prelucrare dedicată care să beneficieze de resurse separate.

Scopul este de a face aplicațiile *smooth* (*fluente*) și *responsive* (*receptive*, *care reacționează*).

Web workerii sunt utili atunci când ai de adus date de la server sau atunci când ai de computat o imagine a unui sistem dinamic care necesită resurse suplimentare ori pur și simplu faci un autosave.

Pentru a crea un worker tot ce este nevoie este instanțierea sa pasându-i fișierul ce conține codul ce va fi executat.

```javascript
const worker = new Worker("aduDatele.js");
```

În acest moment s-a creat un fir de execuție dedicat. Acest fir va comunica numai cu programul care l-a inițiat. Workerii pot instanția la rândul lor alți workeri.

Un worker poate fi utilizat în comun de mai multe programe. Acești workeri sunt numiți workeri partajați (*shared workers*).

```javascript
const worker = new SharedWorker("aduDatele.js");
```

## Contextul de execuție

Web workerii nu se execută în conextul global cum are fi `window`. Contextul de execuție al acestora se numește `DedicatedWorkerGlobalScope`.

Folosind WebWorkerii nu poți manipula DOM-ul sau proprietăți ale obiectului `window` pentru că pur și simplu, worker-ul nu are acces la acesta.

## Metode ale WebWorkerilor

Metodele obiectelor intanțiate sunt `postMessage`, `onmessage`, și `onerror`. Acestea sunt folosite pentru a comunica cu programul care a instanțiat workerul.

## Referințe

- [Web Workers API, MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)
- [The State Of Web Workers In 2021 | Surma | jun 30, 2021](https://www.smashingmagazine.com/2021/06/web-workers-2021/)
