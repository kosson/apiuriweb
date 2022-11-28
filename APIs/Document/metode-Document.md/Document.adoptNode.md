# Document.adoptNode()

Această metodă trasferă nodul unui alt document în cel specificat de aceasta. Modul în care lucrează este că nodul *adoptat* cu întregul său arbore este scos din documentul original, dacă există unul fiind setat `ownerDocument` la cel curent. Nodul va putea fi inserat în documentul cu care se operează.

Metoda are un singur paramentru, iar valoarea acestuia este nodul care trebuie extras din documentul sursă.

Valoarea returnată este chiar nodul care a fost inserat cu noul său context.
