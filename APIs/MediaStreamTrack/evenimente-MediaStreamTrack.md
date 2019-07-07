# Evenimente

Aceste evenimente pot primi funcții cu rol de listener folosind `addEventListener` sau cu `onnumeeveniment`.

## ended

Este un eveniment care apare atunci când sursa își încetează emisia către respectivul track. Este momentul în care valoarea `readyState` este modificată în `ended`.

## mute

Este emis atunci când valoarea proprietății `muted` este setată la `true`. Acest lucru înseamnă că respectivul track nu va mai oferi date, fiind întrerupt temporar. Aceste evenimente pot apărea atunci când sunt probleme cu rețeaua sau cu cel care emite datele.

## unmute

Este emis atunci când datele sunt din nou disponibile.

## isolationchange

Este emis atunci când proprietatea `isolated` suferă o modificare din motiv de acces a documentului la un anumit track.

## overconstrained

Este emis atunci când constrângerile specifice unui track fac ca un track să fie incompatibil ceea ce-l face inutilizabil.

## Resurse

- [4.3 MediaStreamTrack, Media Capture and Streams, W3C](https://w3c.github.io/mediacapture-main/#mediastreamtrack)
- [https://w3c.github.io/webrtc-pc/#isolated-track, WebRTC 1.0: Real-time Communication Between Browsers, W3C](https://w3c.github.io/webrtc-pc/#isolated-track)
