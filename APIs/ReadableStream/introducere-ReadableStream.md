# API-ul `ReadableStream`

## Constructor `ReadableStream()`

Creează și returnează un obiect de tip `ReadableStream` care nu este altceva decât un stream de byte data.

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
