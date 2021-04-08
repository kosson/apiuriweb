# USVString

Un `USVString` este o secvență de [valori scalare Unicode](https://www.unicode.org/glossary/#unicode_scalar_value) (*oricare codepoint Unicode, mai puțin high-surogate și low-surogate*). Această definiție diferă de cea a `DOMString` sau a unui `String` de JavaScript în sensul că va reprezenta mereu o secvență validă care este pretabilă căutării de text. Celelalte (`DOMString` și `String`) pot conține surrogate code points.

Tipul `USVString` este găsit mai mult în API-urile care lucrează intensiv cu procesarea de texte. Restul API-urilor folosesc `DOMString`.

Atunci când `USVString` este prelucrat de JavaScript, va fi transformat în primitive `String` (codare UTF-16).
