# CSSStyleDeclaration

Aceasta este o interfață care oferă un obiect care este un bloc declarativ pentru CSS prin intermediul căreia poți obține informație despre metode și proprietăți legate de stiluri.

Acest obiect poate fi expus folosind trei API-uri diferite:

- `HTMLElement.style` care privește stilurile setate inline;
- prin intermediul API-ului CSSStyleSheet;
- prin Window.getComputedStyle() care expune obiectul `CSSStyleDeclaration` ca o interfață read-only.
