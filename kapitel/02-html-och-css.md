# Kapitel 2: HTML och CSS

> **I det här kapitlet lär du dig**
> - hur en webbsida byggs upp med element och attribut
> - hur du gör formulär, listor och länkar
> - hur du styr utseendet med CSS, selektorer och boxmodellen
> - hur du bygger en layout med Flexbox
> - hur du gör en sida som fler personer kan använda

Varje webbsida du någonsin har besökt består i grunden av två textfiler i samarbete: en som säger vad som finns på sidan och en som säger hur det ska se ut. Du kan skriva båda i vilken textredigerare som helst, och du behöver inget mer än en webbläsare för att se resultatet.

## HTML: sidans struktur

**HTML** står för HyperText Markup Language. Du märker upp innehåll med **element**, som talar om vad varje del är: en rubrik, ett stycke, en bild. Så här ser en komplett sida ut:

```html
<!DOCTYPE html>
<html lang="sv">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Min första sida</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>Temperatur i klassrummet</h1>
    <p>Just nu är det <strong>21 grader</strong>.</p>
    <img src="termometer.png" alt="En termometer som visar 21 grader">
    <ul>
      <li>Mätt med en digital sensor</li>
      <li>Uppdateras varje minut</li>
    </ul>
    <a href="historik.html">Se tidigare mätningar</a>
  </body>
</html>
```

Gå igenom koden uppifrån och ned:

- `<!DOCTYPE html>` talar om att det är modern HTML.
- `<head>` innehåller information *om* sidan, som titeln och länken till stilmallen. Inget av det visas på själva sidan.
- `<body>` innehåller det som syns.
- Ett **element** består oftast av en starttagg, innehåll och en sluttagg, till exempel `<p>text</p>`. Vissa element, som `<img>`, har inget innehåll och ingen sluttagg.
- Ett **attribut** ger ett element extra information. `href` säger vart en länk går och `src` säger vilken bild som ska visas.

Element är antingen **blockelement**, som `<p>` och `<div>`, som tar upp hela raden, eller **inline-element**, som `<a>` och `<strong>`, som ligger i textflödet. Attributen `class` och `id` ger element namn så att du kan peka ut dem senare. Ett `id` får bara finnas en gång på en sida, medan samma `class` kan användas på många element.

### Formulär

Formulär låter användaren skriva in data. Varje fält ska ha en etikett, kopplad med `for` och `id`:

```html
<form>
  <label for="namn">Ditt namn</label>
  <input id="namn" type="text" required>

  <label for="alder">Ålder</label>
  <input id="alder" type="number" min="0" max="120">

  <button type="submit">Skicka</button>
</form>
```

Tack vare `type="number"` får användaren en sifferinmatning på mobilen, och `required` gör att webbläsaren säger ifrån om fältet är tomt.

### Sökvägar

När du länkar till en annan fil skriver du en **sökväg**. `bilder/hund.png` betyder "mappen bilder i samma mapp som den här filen", och `../index.html` betyder "gå upp en mapp". Ett vanligt fel är att skriva en sökväg från din egen dator, som `C:/Users/...`, vilket slutar fungera så fort sidan flyttas.

## CSS: sidans utseende

**CSS** står för Cascading Style Sheets. En CSS-regel består av en **selektor** som väljer element och **deklarationer** som säger vad som ska ändras:

```css
h1 {
  color: darkblue;
  font-size: 2rem;
}

.varning {
  background-color: #ffe5e5;
  padding: 12px;
}

#status {
  font-weight: bold;
}
```

Selektorn `h1` väljer alla `<h1>`, `.varning` väljer element med `class="varning"` och `#status` väljer elementet med `id="status"`. CSS kan läggas i ett attribut, i `<style>` eller i en egen fil. Använd en egen fil, så kan flera sidor dela samma utseende och koden hålls ren.

Om flera regler gäller samma element avgör **specificiteten**: `id` väger tyngre än `class`, som väger tyngre än elementnamn. Vid lika tyngd vinner regeln som kommer sist. Det är därifrån ordet *cascading* kommer.

### Boxmodellen

Varje element är en låda. Innifrån och ut består lådan av innehåll, **padding** (utrymme innanför ramen), **border** (ramen) och **margin** (utrymme utanför ramen).

**Genomräknat exempel.** Hur mycket plats tar den här lådan i bredd?

```css
.kort {
  width: 200px;
  padding: 20px;
  border: 2px solid gray;
  margin: 10px;
}
```

Med standardinställningen gäller `width` bara innehållet. Padding, ram och marginal finns på båda sidor:

| Del | Beräkning | Bredd |
|---|---|---|
| Innehåll | | 200 px |
| Padding | 2 · 20 | 40 px |
| Ram | 2 · 2 | 4 px |
| Synlig låda | 200 + 40 + 4 | 244 px |
| Marginal | 2 · 10 | 20 px |
| **Plats på sidan** | 244 + 20 | **264 px** |

Lägger du till `box-sizing: border-box` räknas padding och ram in i `width`, och lådan blir 200 px bred. Många utvecklare sätter det på alla element, eftersom det gör layouten lättare att räkna på.

### Layout med Flexbox

**Flexbox** är ett layoutsystem som ställer element i rad eller kolumn och fördelar utrymmet mellan dem.

```css
.meny {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

@media (max-width: 600px) {
  .meny {
    flex-direction: column;
  }
}
```

`display: flex` på föräldern gör att barnen hamnar i en rad. `justify-content` fördelar dem längs raden och `align-items` placerar dem på tvären. Blocket med `@media` är en **mediafråga**: reglerna gäller bara på smala skärmar, här blir menyn en kolumn. Det kallas **responsiv** design och betyder att sidan anpassar sig efter skärmen.

## Tillgänglighet från början

**Tillgänglighet** betyder att en sida går att använda även om du ser dåligt, inte kan använda mus eller använder en skärmläsare, ett program som läser upp innehållet. Det här är en del av kursens krav på att dina program ska vara anpassade till användaren.

- Skriv en `alt`-text på bilder som bär information.
- Koppla `<label>` till varje fält.
- Använd rubriker i rätt ordning, `<h1>` följt av `<h2>`, i stället för att bara välja text som ser stor ut.
- Använd element efter vad de betyder. En `<button>` går att nå med tangentbordet, en `<div>` med klick-händelse gör det inte.
- Se till att text och bakgrund har tillräcklig kontrast och att färg inte är det enda som bär information.

Prova själv: stäng av musen och försök använda din sida bara med tabbtangenten.

## Begrepp

- **Element:** en del av en HTML-sida, oftast med start- och sluttagg
- **Attribut:** extra information om ett element, som `href` eller `alt`
- **Selektor:** den del av en CSS-regel som väljer vilka element som påverkas
- **Specificitet:** reglerna som avgör vilken CSS-regel som vinner
- **Boxmodellen:** att varje element består av innehåll, padding, ram och marginal
- **Flexbox:** ett CSS-system för layout i rad eller kolumn
- **Responsiv design:** att sidan anpassar sig efter skärmens storlek
- **Tillgänglighet:** att fler människor, även med funktionsnedsättning, kan använda sidan

## Testa dig själv

1. Vad är skillnaden mellan `<head>` och `<body>`?
2. Vad är skillnaden mellan `class` och `id`?
3. Varför ska en bild ha ett `alt`-attribut?
4. Varför är en relativ sökväg bättre än en sökväg från din egen dator?
5. Vilken regel vinner om både `p { color: red; }` och `.text { color: blue; }` gäller samma stycke, och varför?
6. Vad händer med bredden på en låda när du lägger till `box-sizing: border-box`?
7. Vad är en mediafråga bra för?

## Övningar

**Grund 1.** Gör [HTML-övningarna 1 till 3](https://github.com/abbindustrigymnasium/programmering1/tree/main/HTML/%C3%96vningar) och [CSS-övningarna 1 och 2](https://github.com/abbindustrigymnasium/programmering1/tree/main/CSS/%C3%96vningar).

**Grund 2.** En låda har `width: 300px`, `padding: 10px`, `border: 5px` och `margin: 15px`. Hur mycket plats tar den i bredd utan `box-sizing: border-box`?

<details><summary>Svar</summary>300 + 2 · 10 + 2 · 5 + 2 · 15 = 360 px</details>

**Vidare 3.** Gör CSS-övningarna 3 till 5 och bygg en egen sida med minst två undersidor. Testa den i mobilläge i utvecklarverktygen.

**Vidare 4.** Gå igenom din sida med listan i avsnittet om tillgänglighet och rätta det du hittar. Skriv ner vad du ändrade.

**Utmaning 5.** Gör om menyn på din sida med Flexbox så att den blir en kolumn på smala skärmar. Lägg till tangentbordsfokus som syns tydligt med `:focus-visible`.

## Koppling till projektet

Det här kapitlet motsvarar de första två delarna av [Programmeringsintroduktion](../projekt/programmeringsintroduktion/README.md). Du tränar på det som kommer på provet och du bygger grunden till webbappen i [Hetaste Laget PROG](../projekt/hetaste-laget/README.md).

Kursens genomgångar med länkar till varje delområde finns i mapparna [HTML](https://github.com/abbindustrigymnasium/programmering1/tree/main/HTML) och [CSS](https://github.com/abbindustrigymnasium/programmering1/tree/main/CSS). Till webbappen senare i kursen kan du använda [Bootstrap](https://github.com/abbindustrigymnasium/programmering1/tree/main/Bootstrap).

## Läs mer

- [MDN: Lär dig HTML](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content)
- [MDN: CSS-grunder](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics)
- [W3C: Introduktion till webbtillgänglighet](https://www.w3.org/WAI/fundamentals/accessibility-intro/)

[← Föregående](01-datorn-och-webben.md) | [Innehåll](../README.md) | [Nästa →](03-javascript-grunder.md)
