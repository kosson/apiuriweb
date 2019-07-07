# MediaStream

Această interfață reprezintă un stream de conținut media. Un stream constă din câteva track-uri, fie acestea video sau audio.
Fiecare track este o instanță a interfeței `MediaStreamTrack`, adică câte un obiect, fiecare dintre acestea reprezentând track-uri audio sau video. Fiecare `MediaStreamTrack` poate avea mai multe canale.

Obiectele `MediaStream` au o singură intrare și o singură ieșire. Un astfel de obiect creat folosind metoda `getUserMedia()` este numit **local** pentru că accesează camera și microfonul mașinii locale. Stream-urile care nu sunt locale sunt cele care au ca origine rețeaua și sunt obținute prin API-ul WebRTC `RTCPeerConnection` sau prin Web Audio API `MediaStreamAudioSourceNode`.

Ceea ce produce un `MediaStream` poate fi *consumat* prin folosirea elementelor media `<audio>` sau `<video>`.

Constructorul `MediaStream()` creează și returnează un obiect. Folosind contructorul poți crea un stream gol, unul bazat pe altul sau unul care să conțină o listă de track-uri.

## Referințe

- [MediaStream, MDN](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)
