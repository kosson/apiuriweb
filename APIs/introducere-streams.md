# Introducere streams

API-urile dedicate stream-urilor permit procesarea în fragmente mici ale datelor. Avantajul folosirii stream-urilor este legat de faptul că nu mai este nevoie să descarci întreaga resursă pentru a o afișa/reda. Poți face acest lucru în timp ce primești fragmentele (*chunks*) resursei.

Concepte de lucru:

- **chunks**;
- stream-uri **Readable**;
- stream-uri **Writeable**;
- stream-uri **Transform**;
- lanțuri de **pipe**-uri;
- **backpressure**;
- **teeing**;

## Chunks

Un *chunk* este o sigură bucată de date ce este scrisă sau citită dintr-un stream. Un *chunk* poate fi de mai multe tipuri. Stream-urile pot conține *chunk*-uri de mai multe tipuri. Un *chunk* nu este cea mai mică unitate de date a unui stream. Un stream de byte poate fi format din *chunk*-uri care conține unități de 16KiB fiecare (`Uint8Array`).

## Stream-uri Readable

Un stream **Readable** (vezi API-ul `ReadableStream`) este o *sursă de date* din care poți citi și este reprezentată în JavaScript de un obiect `ReadableStream`.

## Stream-uri Writable

Aceste stream-uri sunt cele în care poți scrie datele (vezi API-ul `WritableStream`).

## Streamuri Transform

Aceste stream-uri constau dintr-o pereche de două stream-uri (`TransformStream`). Unul este readable și celălalt writable. Acționează scriind date în writable și în același timp le citește din readable.

## Pipe chains

Stream-urile pot fi conectate între ele prin așa-numitele *țevi* - **pipes**. Atfel, poți lega un stream readable cu unui writable folosind o metodă `pipeTo()`. Când este necesar, se poate conecta un stream readable la un stream Transform folosind metoda `pipeThrough()` pe care o pune la dispoziție stream-ul readable. Mai multe stream-uri legate în acest fel realizează ceea ce se numește *pipe chain*.

## Backpressure

În momentul în care se realizează un pipe, acesta va trimite informații despre cât de repede vor trece chunks-urile prin el. În cazul lanțului de pipe-uri un anumit punct nu mai acceptă chunk-uri, acesta va propaga până la sursă un semnal prin care semnalează acest lucru. Acest proces de gestionare a circulației chunk-urilor, se numește *backpressure*.

## Teeing

Unui stream readable i se poate aplica un `T`, folosindu-se metoda `tee()`. Seamănă cu t-urile folosite în relele de comunicații. Acest lucru se face atunci când se va bloca (`lock`) stream-ul, adică atunci când nu va mai fi utilizabil în mod direct. Ceea ce se întâmplă este că vor fi create alte două stream-uri noi readable numite *ramuri* care vor putea fi consumate independent. Închipuiește-ți faptul că unul îl trimiți în browser, iar altul unui worker, de exemplu.

## Resurse

- [Streams—The definitive guide](https://web.dev/streams/)
- [Streams API | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)
