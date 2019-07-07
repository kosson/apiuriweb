# Metode MediaStreamTrack

## MediaStreamTrack.applyConstraints()

Permite unei aplicații să specifice valorile acceptate pentru proprietățile obiectului `MediaStreamTrack`.

## MediaStreamTrack.clone()

Returnează o clonă a obiectului `MediaStreamTrack`.

## MediaStreamTrack.getCapabilities()

Returnează o listă de proprietăți care au putut sau pot fi modificate pentru obiectul `MediaStreamTrack`.

## MediaStreamTrack.getConstraints()

Returnează un obiect `MediaTrackConstraints` ce conține setul curent de posibile modificări pentru respectivul track. Valorile sunt cele care au fost setate folosind metoda `applyConstraints()` de la un moment anterior.

## MediaStreamTrack.getSettings()

Returnează un obiect `MediaTrackSettings` care oferă valorile curente.

## MediaStreamTrack.stop()

Oprește din rulare sursa care este asociată track-ului. Starea track-ului este setată la `ended`.

În următorul exemplu, este luat un stream a cărui track-uri sunt oprite rând pe rând.

```javascript
const video  = document.getElementById('video');
const button = document.getElementById('button');
const select = document.getElementById('select');
let streamul;

function opresteTrackurile(stream) {
  stream.getTracks().forEach(track => {
    track.stop();
  });
}

button.addEventListener('click', event => {
  if (typeof streamul !== 'undefined') {
    opresteTrackurile(streamul);
  }
  const videoConstraints = {};
  if (select.value === '') {
    videoConstraints.facingMode = 'environment';
  } else {
    videoConstraints.deviceId = { exact: select.value };
  }
  const constraints = {
    video: videoConstraints,
    audio: false
  };

  navigator.mediaDevices
    .getUserMedia(constraints)
    .then(stream => {
      streamul = stream;
      video.srcObject = stream;
      return navigator.mediaDevices.enumerateDevices();
    })
    .then(gotDevices)
    .catch(error => {
      console.error(error);
    });
});
```

## Referințe

- [Let's light a torch and explore MediaStreamTrack's capabilities](https://www.oberhofer.co/mediastreamtrack-and-its-capabilities/)
