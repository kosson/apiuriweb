# Introducere ImageCapture

Este o interfață care permite capturarea de imagini de la o cameră, adică de la un `MediaStreamTrack`. Interfața moșteneste de la `EventTarget`.

## Proprietăți

### ImageCapture.track

Returnează o referință către obiectul `MediaStreamTrack` pasat constructorului.

## Metode

### ImageCapture.takePhoto()

Ia un instantaneu din obiectul `MediaStreamTrack` și returnează o promisiune care rezolvată oferă un `Blob` cu datele de imagine.

### ImageCapture.getPhotoCapabilities()

Metoda returnează o promisiune care odată rezolvată, oferă un obiect `PhotoCapabilities`.

### ImageCapture.getPhotoSettings()

Returnează o promisiune care se rezovă prin aducerea unui obiect `PhotoSettings` ce conține informații despre configurația fotografiei.

### ImageCapture.grabFrame()

Face un instantaneu din track-ul video și returnează un `ImageBitmap`.

## Resurse

- [ImageCapture](https://developer.mozilla.org/en-US/docs/Web/API/ImageCapture)
- [PhotoCapabilities, MSN](https://developer.mozilla.org/en-US/docs/Web/API/PhotoCapabilities)
- [Image Capture / Grab Frame - Take Photo Sample](https://googlechrome.github.io/samples/image-capture/grab-frame-take-photo.html)
