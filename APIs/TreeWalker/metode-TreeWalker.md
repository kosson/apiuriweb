# Metode TreeWalker

Această interfață nu importă nicio metodă.
Un nod este vizibile doar dacă există în contextul logic format de `whatToShow` și `filter`. Faptul că nodul este vizibil pe ecran sau nu, este irelevant.

## TreeWalker.parentNode()

Metoda reprezintă primul părinte *vizibil* al documentului, pe care-l returnează. Dacă un astfel de node nu există sau dacă se află dincolo de nodul rădăcină definit la momentul construcției obiectului, va fi returnată valoarea `null`.

## TreeWalker.firstChild()

Nodul curent devine primul copil *vizibil* al nodului curent, returnându-l. Dacă nu există niciun copil, este returnată valoarea `null`, iar poziția este menținută.

## TreeWalker.lastChild()

Nodul curent devine ultimul copil *vizibil* al nodului curent, returnându-l. Dacă nu există niciun copil, este returnată valoarea `null`, iar poziția este menținută.

## TreeWalker.previousSibling()

Mută nodul pe anteriorul sibling (frate pe aceeași ramură), dacă acesta există, pe care-l returnează. Dacă nu există un astfel de nod, este returnată valoarea `null`, iar poziția este menținută.

## TreeWalker.nextSibling()

Mută nodul pe următorul sibling (frate pe aceeași ramură), dacă acesta există, pe care-l returnează. Dacă nu există un astfel de nod, este returnată valoarea `null`, iar poziția este menținută.

## TreeWalker.previousNode()

Mută modul pe nodul anterior *vizibil* găsit, pe care-l returnează. Nodul curent devine cel găsit. Dacă un astfel de node nu există sau dacă se află dincolo de nodul rădăcină definit la momentul construcției obiectului, va fi returnată valoarea `null`.

## TreeWalker.nextNode()

Mută modul pe următorul nod *vizibil* găsit, pe care-l returnează. Nodul curent devine cel găsit. Dacă un astfel de node nu există sau dacă se află dincolo de nodul rădăcină definit la momentul construcției obiectului, va fi returnată valoarea `null`.
