# Modelul după care se fac formatările vizuale

*Visual formatting model* descrie cum ar trebui să fie preluat arborele documentului pentru a fi procesat și afișat în medii care permit acest lucru.

În acest model, fiecare element din arborele documentului generează zero sau mai multe casete (în lb. engleză *boxes*) conform lui *box model* - modelul de creare a casetelor.

Afișarea casetelor este guvernată de următoarele constrângeri:
- dimensiunile casetei și tipul acestora;
- schema de poziționare (*normal flow*, *float*, și *absolute positioning*);
- relațiile dintre elementele din arborele documentului;
- informație externă (dimensiunea viewport-ului, dimensiunile intrinsece ale imaginilor, etc.).

În mediul de afișare continuu *viewport*-ul este zona care în care se face afișarea în cadrul broserului. Agenții utilizatorului pot modifica layout-ul paginii atunci când dimensiunea viewport-ului se modifică. Acesta este cazul în care redimensionezi fereastra browserului sau când orientarea se modifică în cazul unui dispozitiv portabil.

## Generarea casetelor

Generarea casetelor - *gox generation* este partea modelului de formatare vizuală care creează casete în baza elementelor documentului. Tipul cutiilor generate depinde de valoarea proprietății `display`.

## Resurse

- [Visual formatting model](https://developer.mozilla.org/en-US/docs/Web/CSS/Visual_formatting_model)
