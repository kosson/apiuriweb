# Metode MediaStream

## MediaStream.addTrack()

Face o copie a obiectului `MediaStreamTrack` care apare ca argument al metodei. În cazul în care se încearcă adăugarea aceluiași track, nimic nu se va petrece.

## MediaStream.clone()

Returnează o clonă a obiectului `MediaStream`. Această clonă va avea o valoare proprie la `id`.

## MediaStream.getAudioTracks()

Returnează o listă de track-uri existentă în obiectul `MediaStream`, care au atributul `kind` setat la valoarea `"audio"`.

## MediaStream.getTrackById()

Returnează track-ul al cărui id a fost pasat drept parametru. Dacă id-ul nu există sau nu a fost oferit vreun parametru, valoarea returnată este `null`. Dacă mai multe track-uri au același id, va fi returnat doar primul.

## MediaStream.getTracks()

Returnează o listă cu obiecte `MediaStreamTrack` care există în obiectul `MediaStream` indiferent de valoarea atributului `kind`.

## MediaStream.getVideoTracks()

Returnează o listă de track-uri existentă în obiectul `MediaStream`, care au atributul `kind` setat la valoarea `"video"`.
