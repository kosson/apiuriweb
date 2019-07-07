# MediaDevices.getUserMedia(constraints)

Această metodă este folosită pentru a produce un `MediaStream` și poate fi apelată din obiectul de tip Singleton `navigator.mediaDevices.getUserMedia(c)`.

Apelarea metodei va conduce la apariția pe ecranul clientului a unui mesaj prin care i se cere permisiunea pentru folosirea dispozitivelor media. Ca urmare a acordului utilizatorului, se va crea un obiect `MediaStream` ce va conține track-uri pentru fiecare media care emite și a primit acordul.

Metoda returnează un `Promise`, a cărui rezolvare este chiar obiectul `MediaStream`. Stream-ul rezultat poate fi convertit în URL folosind metoda `createObjectURL`, ceea ce permite afișarea acestuia în browser dacă avem un tag `<video>`.

```javascript
navigator.mediaDevices.getUserMedia(constraints)
.then(function(stream) {
  /* folosește stream-ul la ceva */
})
.catch(function(err) {
  /* afișează eroarea */
});
```

Poți împacheta și într-o funcție `async`.

```javascript
async function getMedia(pc) {
  let stream = null;
  try {
    stream = await navigator.mediaDevices.getUserMedia(constraints);
    /* folosește stream-ul la ceva */
  } catch(err) {
    /* afișează eroarea */
  }
}
```

În cazul în care browserul nu găsește track-urile media, va returna o eroare `NotFoundError`.

## Parametrul ce definește limitele

Metoda `getUserMedia` poate primi un obiect de tip `MediaTrackConstraints`, care specifică tipurile de media împreună cu cerințele specifice fiecărui tip al acestora.

Acest obiect are doi membri: `audio` și `video`.

De exemplu, următoarea cerință specifică necesitatea ambelor track-uri:

```javascript
{ audio: true, video: true }
```

Dacă unul din trackuri este indisponibil, va fi emisă o eroare `NotFoundError`.
Un alt scenariu poate implica ca doar unul din track-uri să fie necesar.

```javascript
const video  = document.getElementById('video');
const button = document.getElementById('button');
button.addEventListener('click', event => {
  const constraints = {
    video: true,
    audio: false
  };
  navigator.mediaDevices
    .getUserMedia(constraints)
    .then(stream => {
      video.srcObject = stream; // necesită existența unui <video>
    })
    .catch(error => {
      console.error(error);
    });
});
```

### Caracteristici

În cazul unui track video poți specifica în obiectul limitărilor dimensiunile la care se vor face capturile de la cameră.

```javascript
{
  audio: true,
  video: { width: 1280, height: 720 }
}
```

#### Rezoluția

În cazul specificării rezoluției, dacă aceasta nu poate fi onorată de către device, promisiunea va fi rejected cu o eroare `OverconstrainedError`.

Pot fi definite chiar plaje de valori.

```javascript
{
  video: {
    width: {
      min: 1280,
      ideal: 1920,
      max: 2560,
    },
    height: {
      min: 720,
      ideal: 1080,
      max: 1440
    }
  }
}
```

#### Selectarea camerei

În cazul în care dorești să precizezi care va fi camera ce va trimite date unui anumit track video, există patru opțiuni posibile: `user`, `environment`, `left` și `right`.

În cazul dispozitivelor mobile, putem specifica care dintre camere pot fi folosite. Următorul exemplu de setare va indica o preferință pentru frontcamera, dacă este disponibilă.

```javascript
{
  audio: true,
  video: {
    facingMode: "user"
  }
}
```

Pentru a *întări* o anumită preferință, se va face opțiunea specificând-o prin cuvântul cheie `exact`.

```javascript
{
  audio: true,
  video: {
    facingMode: { exact: "environment" }
  }
}
```

Tot ca indicație precisă, poți specifica un `deviceId` după ce în prealabil ai făcut o identificare și o alegere din ceea ce ai găsit cu `mediaDevices.enumerateDevices()`.

```javascript
{
  audio: true,
  video: {
    { deviceId: Id-ulPreferat }
  }
}
```

Poți întări opțiunea pentru a limita strict și în cazul id-ului dispozitivului.

```javascript
{
  audio: true,
  video: {
    { exact: id-ulexactAlCamerei }
  }
}
```

#### Expunerea propriului desktop

Acest lucru este posibil dacă se alege drept opțiune pentru video cea specifică browserului cu care se va lucra. Pentru Firefox vom avea `mediaSource: 'screen'`.

```javascript
{
  audio: true,
  video: {
    mediaSource: 'screen'
  }
}
```

În cazul Chrome avem:

```javascript
{
  audio: true,
  video: {
    mandatory: {
      chromeMediaSource: 'desktop'
    }
  }
}
```

## Referințe

- [URL.createObjectURL(), MDN](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL)
- [Front and Rear Camera Access with JavaScript's getUserMedia()](https://scotch.io/tutorials/front-and-rear-camera-access-with-javascripts-getusermedia)
- [Choosing cameras in JavaScript with the mediaDevices API](https://www.twilio.com/blog/2018/04/choosing-cameras-javascript-mediadevices-api.html)
- [Add screen sharing to your Twilio Video application](https://www.twilio.com/blog/2018/01/screen-sharing-twilio-video.html)
- [Camera and Video Control with HTML5, David Walsh](https://davidwalsh.name/browser-camera)
- [Take Photos and Control Camera Settings](https://developers.google.com/web/updates/2016/12/imagecapture)
- [Capturing Audio & Video in HTML5](https://www.html5rocks.com/en/tutorials/getusermedia/intro/)
