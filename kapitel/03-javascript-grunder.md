# Kapitel 3: JavaScript-grunder

> **I det här kapitlet lär du dig**
> - att spara data i variabler och använda datatyper
> - att fatta beslut med villkor
> - att upprepa kod med loopar
> - att dela upp kod i funktioner
> - att hålla ordning på data med objekt och arrayer

HTML och CSS kan beskriva en sida, men de kan inte fatta beslut. Med JavaScript kan sidan räkna, jämföra och reagera. Det är också ett riktigt programspråk, och det du lär dig här gäller nästan ordagrant i C++ och GDScript senare i kursen.

Du kan köra exemplen i webbläsarens konsol (F12) eller lägga dem i en fil som du länkar in med `<script src="...">`. `console.log()` skriver ut ett värde i konsolen.

## Variabler och datatyper

En **variabel** är ett namngivet ställe i minnet. Du skapar den med `let` om värdet kan ändras och med `const` om det inte ska ändras.

```js
const namn = "Sara";
let antalMatningar = 0;
antalMatningar = antalMatningar + 1;

console.log(namn, antalMatningar); // Sara 1
```

De **datatyper** du använder mest är `number` (tal), `string` (text), `boolean` (`true` eller `false`), `undefined` (inget värde ännu) och `object`. Eftersom JavaScript är **dynamiskt typat** bestäms typen av värdet, inte av variabeln. Det är bekvämt, men kan också ställa till det:

```js
console.log(5 + 3);     // 8
console.log("5" + 3);   // "53", texten slås ihop
console.log("5" * 2);   // 10, texten görs om till tal
console.log(7 % 3);     // 1, resten vid division
```

Operatorn `%` kallas **modulo** och ger resten vid division. Den är användbar för att till exempel se om ett tal är jämnt.

Jämför alltid med `===` och `!==`. De kontrollerar både värde och typ, medan `==` försöker göra om typerna först och ger överraskande resultat, som att `0 == ""` är sant.

## Villkor

Med `if` väljer programmet väg beroende på ett villkor. Ett villkor är ett uttryck som blir `true` eller `false`.

```js
const temperatur = 26;
let meddelande;

if (temperatur > 25) {
  meddelande = "För varmt";
} else if (temperatur < 18) {
  meddelande = "För kallt";
} else {
  meddelande = "Lagom";
}

console.log(meddelande); // För varmt
```

Du kan kombinera villkor med `&&` (och), `||` (eller) och `!` (inte). `switch` passar när du jämför en variabel med flera bestämda värden.

## Loopar

En **loop** upprepar kod. `for` passar när du vet hur många varv det ska bli, `while` när du upprepar tills något händer.

**Genomgånget exempel.** Vi vill räkna medeltemperaturen och hitta det högsta värdet i en lista:

```js
const matningar = [18, 21, 25, 19];
let summa = 0;
let hogst = matningar[0];

for (let i = 0; i < matningar.length; i++) {
  summa = summa + matningar[i];
  if (matningar[i] > hogst) {
    hogst = matningar[i];
  }
}

const medel = summa / matningar.length;
console.log(medel, hogst); // 20.75 25
```

Att följa variablerna varv för varv kallas **spårning**. Gör det på papper när koden inte fungerar:

| Varv | `i` | `matningar[i]` | `summa` efter | `hogst` efter |
|---|---|---|---|---|
| 1 | 0 | 18 | 18 | 18 |
| 2 | 1 | 21 | 39 | 21 |
| 3 | 2 | 25 | 64 | 25 |
| 4 | 3 | 19 | 83 | 25 |

Sedan blir medelvärdet 83 / 4 = 20,75. Index börjar på 0, så sista giltiga index är `length - 1`. Därför står det `i < matningar.length` och inte `<=`.

## Funktioner

En **funktion** är ett namngivet stycke kod som kan köras många gånger. Den tar emot **parametrar** och kan lämna tillbaka ett **returvärde**.

```js
function medelvarde(lista) {
  let summa = 0;
  for (const tal of lista) {
    summa += tal;
  }
  return summa / lista.length;
}

const arDetVarmt = (temperatur, grans) => temperatur > grans;

console.log(medelvarde([18, 21, 25, 19]));  // 20.75
console.log(arDetVarmt(26, 25));            // true
```

Den andra funktionen är skriven som en **arrow-funktion**, ett kortare skrivsätt. Med funktioner kan du dela upp ett stort problem i små delar som är lätta att testa var för sig.

## Objekt och arrayer

En **array** är en ordnad lista. Ett **objekt** samlar värden under namn.

```js
const matning = {
  temperatur: 21.5,
  luftfuktighet: 40,
  rum: "A12",
};

console.log(matning.temperatur); // 21.5
matning.rum = "A14";

const historik = [
  { temperatur: 20, rum: "A12" },
  { temperatur: 26, rum: "A14" },
  { temperatur: 23, rum: "A12" },
];

const varma = historik.filter((m) => m.temperatur > 22);
console.log(varma.length); // 2
```

`filter` är en arrayfunktion som tar emot en arrow-funktion och returnerar de element där den blir sann. Arrayer och objekt tillsammans kan beskriva nästan all data, och det är just så data skickas mellan din ESP8266, databasen och webbappen senare i kursen.

## Från JavaScript till andra språk

Kontrollstrukturerna ser nästan likadana ut i de språk du möter senare, vilket gör det lätt att byta språk när du förstår grunden:

| Struktur | JavaScript | C++ | GDScript |
|---|---|---|---|
| Variabel | `let x = 5;` | `int x = 5;` | `var x = 5` |
| Villkor | `if (x > 3) { }` | `if (x > 3) { }` | `if x > 3:` |
| Loop | `for (let i = 0; i < 3; i++) { }` | `for (int i = 0; i < 3; i++) { }` | `for i in range(3):` |
| Funktion | `function f(a) { }` | `int f(int a) { }` | `func f(a):` |

Den största skillnaden är att C++ är **statiskt typat**: du måste bestämma typen när du deklarerar variabeln, och det kontrolleras redan vid kompileringen.

## Begrepp

- **Variabel:** ett namngivet ställe där ett värde sparas
- **Datatyp:** vilken sorts värde något är, till exempel tal eller text
- **Kontrollstruktur:** kod som styr ordningen programmet körs i, som villkor och loopar
- **Modulo:** operatorn `%`, som ger resten vid division
- **Funktion, parameter och returvärde:** ett namngivet kodstycke, det den får in och det den lämnar tillbaka
- **Array:** en ordnad lista av värden
- **Objekt:** en samling namngivna värden
- **Spårning:** att följa variablernas värden steg för steg

## Testa dig själv

1. När ska du använda `const` och när ska du använda `let`?
2. Varför blir `"5" + 3` något annat än `"5" * 2`?
3. Varför är `===` säkrare än `==`?
4. Vad händer om du skriver `i <= matningar.length` i loopen ovan?
5. Vad är skillnaden mellan en parameter och ett returvärde?
6. Vad är skillnaden mellan en array och ett objekt? Ge ett exempel på när du använder vardera.
7. Vad menas med att C++ är statiskt typat?

## Övningar

Övningarna finns i kursens repo: [JavaScript-övningar](https://github.com/abbindustrigymnasium/programmering1/tree/main/Javascript/%C3%B6vningar). Genomgångar och länkar till varje område hittar du i mappen [Javascript](https://github.com/abbindustrigymnasium/programmering1/tree/main/Javascript).

**Grund 1.** Gör avsnitten Variabler, Datatyper, Operatorer, Jämförelser, If-satser, Loopar och Switch-satsen i övningsmappen.

**Grund 2.** Vad skriver koden ut? Tänk först, kör sedan.

```js
let x = 10;
x = x % 4;
console.log(x * 3);
```

<details><summary>Svar</summary>10 % 4 = 2 och 2 · 3 = 6, så koden skriver ut 6.</details>

**Grund 3.** Skriv en loop som summerar talen från 1 till 10.

<details><summary>Svar</summary>Summan blir 55.</details>

**Vidare 4.** Gör avsnitten Funktioner, Objekt, Listor och Arrow functions i övningsmappen.

**Vidare 5.** Skriv en funktion som tar emot en array med temperaturer och ett gränsvärde och returnerar hur många värden som ligger över gränsvärdet.

**Utmaning 6.** Gör avsnittet Array filter med arrow functions. Skriv en funktion som tar emot `historik` från exemplet och returnerar medeltemperaturen för ett valt rum. Testa din funktion med ett rum som inte finns. Vad händer, och hur vill du att det ska fungera?

## Koppling till projektet

Kapitlet täcker JavaScript-delen av [Programmeringsintroduktion](../projekt/programmeringsintroduktion/README.md), som avslutas med prov. Samma grunder använder du sedan i varje annat projekt i kursen.

## Läs mer

- [MDN: JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [javascript.info](https://javascript.info/)

[← Föregående](02-html-och-css.md) | [Innehåll](../README.md) | [Nästa →](04-problemlosning-och-felsokning.md)
