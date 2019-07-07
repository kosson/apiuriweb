# Metode MediaDevices

## enumerateDevices()

Folosind metoda obții un array al dispozitivelor media prezente în sistem.

```javascript
const getCameraSelection = async () => {
  const devices = await navigator.mediaDevices.enumerateDevices();
  const videoDevices = devices.filter(device => device.kind === 'videoinput');
  const options = videoDevices.map(videoDevice => {
    return `<option value="${videoDevice.deviceId}">${videoDevice.label}</option>`;
  });
  cameraOptions.innerHTML = options.join('');
};
```

## getSupportedConstraints()

## getDisplayMedia()

## getUserMedia()
