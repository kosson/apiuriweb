# Event handlers - gestionari de evenimente

Atunci când apare un eveniment (un click, o atingere, o anumită tastă apăsată), în cazul în care este în intenția programatorului să ofere o reacție, va „programa” executarea codului asociat folosind o funcție cu rol de callback.

În relația codului JavaScript cu DOM-ul, evenimentele sunt gestionate prin așa-numiții „event handlers” - **gestionari de evenimente** în limba română, dacă dorești.

## Spune standardul

Unele obiecte pot primi „semnale” (`events`), care trebuie gestionate. Aceste „semnale” (`events`) sunt „ascultate” de *receptorii de evenimente* (`event listeners`), fără ca aceste evenimente (semnale), să fie capturate/reținute de obiectele cărora le sunt destinate.

## Definirea receptorilor în HTML

Un „gestionar de evenimente” (`event handler`) are un nume ușor de deosebit pentru că începe cu `on`, fiind urmat de numele explicit al evenimentului. Pentru că este mai ușor de scris și înțeles, vom numi *gestionarii de evenimente* în textele documentației **receptori**. Această denumire simplificată va conduce la înțelegerea mecanismelor mai târziu când vom diseca un eveniment.

### Definirea codului ca valoare a atributului

Cea mai directă metodă de a executa cod JavaScript ca urmare a apariției unui eveniment, este să definești codul ca valoare a atributului *on*nume_eveniment.

```html
<input type="button" value="Declanșează!!!" onclick="console.log('sunt răspunsul')"/>
```

Un *receptor* are una dintre valorile: `null`, o funcție callback sau chiar o secvență de cod brută, necompilată. Fii foarte atent(ă) să folosești HTML escaped charcters pentru semnele de punctuație care au însemnătate pentru codul HTML. Ceea ce se petrece în bucătăria acestui mod de a defini receptorii este că întreg atributul este *ambalat* într-o funcție de către motorul browserului. În codul funcției va fi disponibil un identificator numit `event`, care este o legătură către obiectul eveniment însuși.

```html
<input type="button" value="Declanșează!!!" onclick="console.log(event.type)"/>
```

Acest lucru este foarte util pentru că îți oferă acces la acest obiect fără ca tu să-l definești sau să-l obții dintr-o listă de argumente. Ba mai mult, ai acces chiar la obiectul care reprezintă elementul țintit prin legătura pe care o oferă `this`.

```html
<input type="button" value="Declanșează!!!" onclick="console.log(this.value)"/>
```

Ambalarea codului executat se face în spate cu setarea legăturilor către mediile lexicale ale obiectului global și la obiectul ce reprezintă ținta.

```javascript
function () {
  with(document){
    with(this){
      // executarea coduluid definit ca receptor
    }
  }
}
```

În cazul în care elementul vizat este parte a unui formular, se va face o legătură și către elementul părinte, care este `form`.

```javascript
function () {
  with(document){
    with(this.form){
      with(this){
        // executarea coduluid definit ca receptor
      }
    }
  }
}
```

Această structură de rezolvare a mediilor lexicale permite adresarea directă în cazul formularelor a identificatorilor definiți prin atributul `name`.

```html
<form>
  <input type="text" name="nume" value="">
  <input type="button" onclick="console.log(nume.value)">
</form>
```

### Apelarea unu callback definit anterior

În cazul în care codul *receptorului* este deja definit în pagină sau încărcat dintr-un fișier JavaScript, poate fi menționat apelul către funcție.

```html
<script>function facCeva () { console.log('sunt răspunsul'); }</script>
<input type="button" value="Declanșează!!!" onclick="facCeva()"/>
```

Codul JavaScript executat de funcția apelată are acces la orice există în global scope. Acest aspect este important pentru cazul în care sunt folosite modulele.

## Înregistrarea evenimentelor

Receptorii sunt definiți în câteva moduri:

-   un mod comun tuturor *receptorilor* este cel din poziția de atribut al elementului DOM vizat. Numele atributului IDL este chiar numele evenimentului (`onclick`, `onclose`);
-   folosirea proprietății corespondente a obiectului elementului vizat: `window.onload = function () {};` - definit prin DOM 0;
-   identificator al unei funcții JavaScript `onclick="facCeva()"`;
-   folosirea metodei interne `addEventListener()` pentru atribuirea programatică a unui *receptor*.

Un exemplu foarte simplu ar fi cel pe care practica îl indică ca fiind o cerință la momentul în care începi să scrii cod pentru client. Verifici dacă pagina s-a încărcat prin faimoasa secvență:

```javascript
window.onload = function () {}; // la încărcarea paginii execută funcția
// DOM-ul este pregătit și pe deplin încărcat
```

Și o variantă mai dezvoltată:

```javascript
function onReady (){
  console.log('Totul s-a încărcat');
};
window.onload = onReady;
```

Acest mod de atașare a receptorilor a fost definit de specificațiile DOM 0 și a fost în intenție tratarea evenimentului la faza de bubbling. Acest mod atașează receptorul ca metodă a obiectului țintă.

```javascript
let element = document.getElementById("ceva");
element.onclick = function () {
  console.log(this.id); // "ceva"
};
```

Pentru a elimina receptorii atașați astfel (DOM 0), se va seta la valoarea `null` proprietatea: `element.onclick = null;`.

Se pot atașa funcții direct unor proprietăți, dar această practică poate conduce la erori, suprascrieri de eveniment, ș.a.m.d. Cel mai bine este să se folosească metoda `addEventListener()` oferită de specificațiie DOM 2:

```javascript
// poți atașa direct
document.body.onclick = function () {};

// sau prin utilizarea metodei dedicate addEventListener
document.body.addEventListener("click", () => {
  var elemCentral = document.getElementById("central");
  oFunctieCareFaceCeva(elemCentral, "S-a dat click");
}, false);
```

Atenția la definirea callback-ului. Este indicată folosirea unui arrow function pentru a păstra legătura la obiectul țintă. În exemplul de mai sus, a fost setat cel de-al treilea parametru la valoarea `false` pentru ca apelarea callback-ului să se facă la faza de bubbling. Folosind `addEventListener` poți atașa mai mulți receptori unui element.

Pentru a elimina receptorii, trebuie să ai un identificator către aceștia. Urmând această necesitate, funcțiile care vor juca rolul de callback trebuie definite separat pentru a putea fi referite atunci când se face atribuirea, dar și eliminarea.

```javascript
let element = document.selectElementById("ceva");
let facCeva = () => {
  console.log("this.id");
}
element.addEventListener("click", facCeva, false);
element.removeEventListener("click", facCeva, false);
```

## Probleme care apar

### Receptor încărcat după eveniment

Pentru a te asigura de faptul că eistă un mecanism care să prevină situațiile în care pagina s-a încărcat, dar codul *receptorului* nu, cel mai bine este ca apelul să fie introdus în `try {} catch(err) {}`.

```html
<input type="button" value="Declanșează!!!" onclick="try { facCeva(); } catch(err) {}"/>
```

În exemplul de mai sus, dacă butonul este acționat înaintea încărcării codului funcției, nu va fi produsă o eroare, iar browserul va gestiona starea de eroare.

### Dubla modificare

În cazul în care survin modificări ale codului *receptorului* va trebui ca acestea să fie făcute în codul sursă JavaScript, dar și în codul HTML, după caz. Alternativa este atribuirea *receptorului* folosind `addEventListener`.

```javascript
let element = document.getElementById("tinta");
element.onclick = function() {
  console.log("Salut!");
};
```

## Resurse

[Event handlers](https://html.spec.whatwg.org/multipage/webappapis.html#event-handlers)
