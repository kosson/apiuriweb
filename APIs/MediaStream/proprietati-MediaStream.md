# Proprietăți MediaStream

Această interfață moșteneste de la `EventTarget`.

## MediaStream.active

Este o valoare care returnează `true` în cazul în care `MediaStream` este activ.

## MediaStream.id

Este un identificator unic (UUID) pentru obiect.

## Evenimente

### MediaStream.onaddtrack

Este un `EventHandler` - `addtrack` care declanșează execuția în momentul în care un obiect `MediaStreamTrack` este adăugat.

### MediaStream.onremovetrack

Este un `EventHandler` - `removetrack` care declanșează execuția în momentul în care un obiect `MediaStreamTrack` este eliminat.
