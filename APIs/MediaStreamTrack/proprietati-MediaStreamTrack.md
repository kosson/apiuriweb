# Proprietăți MediaStream

## MediaStreamTrack.enabled

Dacă track-ul a fost activat, valoarea va fi `true`.

## MediaStreamTrack.id

Este un identificator (GUID) creat de browser pentru un track.

## MediaStreamTrack.kind

Indică tipul track-ului: `audio` sau `video`. Această proprietate poate fi folosită într-un scenariu care necesită un inventar al dispozitivelor existente.

```javascript
const video = document.getElementById('video');
const button = document.getElementById('button');
const select = document.getElementById('select');

function gotDevices(mediaDevices) {
  select.innerHTML = '';
  select.appendChild(document.createElement('option'));
  let count = 1;
  mediaDevices.forEach(mediaDevice => {
    if (mediaDevice.kind === 'videoinput') {
      const option = document.createElement('option');
      option.value = mediaDevice.deviceId;
      const label = mediaDevice.label || `Camera ${count++}`;
      const textNode = document.createTextNode(label);
      option.appendChild(textNode);
      select.appendChild(option);
    }
  });
}
navigator.mediaDevices.enumerateDevices().then(gotDevices);
```

## MediaStreamTrack.label

Este un string care identifică sursa track-ului: `internal microphone`.

## MediaStreamTrack.muted

Indică prin Boolean dacă track-ul nu mai este disponibil din diferite motive.

## MediaStreamTrack.readyState

Returnează o valoare care indică starea în care se află track-ul.

- `"live"` indicând faptul că un input este conectat
- `"ended"` care indică că input-ul nu mai oferă date și nu va mai da nici mai departe.

## Referințe

- [Choosing cameras in JavaScript with the mediaDevices API](https://www.twilio.com/blog/2018/04/choosing-cameras-javascript-mediadevices-api.html)
