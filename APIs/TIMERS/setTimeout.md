# setTimeout()

Este o metodă a obiectului `window`, care execută o funcție după ce timpul menționat în al doilea parametru introdus a expirat.

În loc de o funcție care va fi invocată, poate primi și cod JavaScript, care va fi compilat și executat la scurgerea timpului. Această practică nu este recomandată, fiind încadrată la riscuri.

Metoda returnează un identificator, care poate fi folosit pentru a întrerupe scurgerea timpului menționat.

```javascript
let id = setTimeout(function () {
    return 'ceva';
}, 3000);
console.log(id); // 1
```

## Debouncing și trottling

Aceste tehnici sunt folosite pentru a limita numărul de evenimente declanșate. În exemplul de mai jos, declanșarea evenimentelor se amână conform valorii pasate în al doilea parametru.

```javascript
let aduDate = () => {
  console.log("Aduc date de la API...");
};

function debounce (fn, timeout = 300) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(this, args);
    }, timeout);
  };
};

let apelIntarziat = debounce(() => aduDate(), 2000);
apelIntarziat();
```

### Ignorarea altor evenimente care ar putea surveni

Există cazuri în care este nevoie să previi apăsarea unui buton de două ori, de exemplu.

```javascript
function debounce_frame (fn, timeout = 300) {
  let timer;
  return (...args) => {
    // în cazul în care nu a fost setat un timer pentru funcție
    if (!timer) {
      fn.apply(this, args); // execută funcția
    }
    clearTimeout(timer); // curăță timerul

    // setează un timer care va reseta timer la undefined după o perioadă de timp
    timer = setTimeout(() => {
      timer = undefined;
    }, timeout);

    // după ce se scurge timpul de întârziere, timer va fi setat la undefined ceea ce permite execuția încă o dată
  };
}; 
```