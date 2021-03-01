# API-ul `ReadableStream`

Un stream **Readable** (vezi API-ul `ReadableStream`) este o *sursă de date* din care poți citi și este reprezentată în JavaScript de un obiect `ReadableStream`.

Sursele de date pot fi de două tipuri:

- *push*, care împing continuu date atunci când ai acces la sursă (video, evenimente trimise de server sau WebSockets);
- *pull*, care cer în mod explicit să faci o cerere de date atunci când te conectezi la sursă (`fetch` și `XMLHttpRequest`).

Datele sunt citite în `chunks`. Spunem despre chunk-urile unui stream că sunt *enqueued*, ceea ce înseamnă că sunt ordonate într-o coadă gata de a fi citită. Strategia de organizare a acestei cozi (*queuing strategy*) este un obiect care determină cum va fi semnalat `backpressure`-ul în funcție de starea cozii interne. Strategia de organizare a cozii atribuie dimensiunea fiecărui chunk și compară dimensiunea tuturor chunk-urilor din coadă cu un număr specificat numit *high water mark*.

Chunk-urile dintr-un stream sunt citite de un *reader*. Acesta accesează câte un chunk pe rând, fiind permise operațiuni asupra lui. Acest reader însoțit de cod ce reprezintă o anumit logică de procesare, împreună se numesc *consumator*. Dor un singur reader poate citi stream-ul. Atunci când acesta începe să citească stream-ul spunem că devine *active reader* care este *locked* pe stream. Dacă dorești ca alt reader să preia citirea stream-ului, atunci va trebui să procedezi la ceea ce numim *release*. Totuți poți proceda și la o procedură de teeing.

Fiecare stream readable are câte un controller atașat, care controlează curgerea stream-ului.

## Constructor `ReadableStream()`

Creează și returnează un obiect de tip `ReadableStream` care nu este altceva decât un stream de date byte. Acest contructor are un argument opțional `underlyingSource`, care reprezintă obiectul a cărui metode și proprietăți vor defini cum se va comporta instanța streamului construit.

## Proprietăți

### `ReadableStream.locked`

Este o proprietate read-only care indică dacă stream-ul este blocat de un reader sau nu.

## Metode

### `ReadableStream.cancel()`

### `ReadableStream.getReader()`

### `ReadableStream.pipeThrough()`

### `ReadableStream.pipeTo()`

### `ReadableStream.tee()`

## Exemplu

În exemplul dat de MDN este creat un `Response` cu scopul de a face streaming fragmentelor HTML aduse dintr-o altă sursă în browser. Este demonstrat ce se poate face cu `ReadableStream` în combinație cu `Uint8Array`.

```javascript
fetch("https://www.example.org/").then((response) => {
  const reader = response.body.getReader();
  const stream = new ReadableStream({
    start(controller) {
      // The following function handles each data chunk
      function push() {
        // "done" is a Boolean and value a "Uint8Array"
        reader.read().then(({ done, value }) => {
          // Is there no more data to read?
          if (done) {
            // Tell the browser that we have finished sending data
            controller.close();
            return;
          }

          // Get the data and send it to the browser via the controller
          controller.enqueue(value);
          push();
        });
      };

      push();
    }
  });

  return new Response(stream, { headers: { "Content-Type": "text/html" } });
});
```
