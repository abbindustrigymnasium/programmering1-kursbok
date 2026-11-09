# Kapitel 10: Generativ AI, etik och samhälle

> **I det här kapitlet lär du dig**
> - hur en stor språkmodell fungerar i stora drag
> - att skriva tydliga prompter och förstå vad AI inte kan
> - att anropa en språkmodell från JavaScript på ett säkert sätt
> - att diskutera sociala och etiska frågor kring programmering
> - att använda AI som hjälp utan att sluta tänka själv

Du kan fråga en chatbot nästan vad som helst och få ett välformulerat svar på några sekunder. Men hur fungerar det egentligen, och kan du lita på svaret? Som programmerare behöver du kunna båda sidor: att bygga med verktygen och att se vad de kan ställa till med.

## Vad är generativ AI?

**Generativ AI** är system som kan skapa nytt innehåll, till exempel text, bilder eller kod. Skillnaden mot ett vanligt program är stor. Du har inte skrivit reglerna själv; i stället har systemet tränats på mycket stora mängder data och lärt sig mönster.

En **stor språkmodell** (LLM, large language model) förutsäger vilken text som sannolikt kommer härnäst. Modellen arbetar inte med hela ord utan med **tokens**, ordbitar. När du ställer en fråga väljer modellen en token i taget och bygger på så sätt upp svaret. Det betyder att den är väldigt bra på att skriva något som *låter* rätt, vilket inte är samma sak som att det *är* rätt.

Därav de viktigaste begränsningarna:

| Begränsning | Vad det betyder | Vad du gör åt det |
|---|---|---|
| **Hallucination** | Modellen hittar på fakta eller källor som låter trovärdiga | Kontrollera mot pålitliga källor |
| **Kunskapsgräns** | Modellen kan sakna information om det som hänt nyligen | Ge den aktuell information, eller kontrollera själv |
| **Bias** | Modellen återger fördomar som finns i träningsdatan | Var uppmärksam och granska resultatet |
| **Begränsad indata** | Det finns en gräns för hur mycket text modellen kan hantera samtidigt | Dela upp och sammanfatta |

## Promptteknik

En **prompt** är instruktionen du ger modellen. Att jämföra är det bästa sättet att lära sig:

| Svag prompt | Bättre prompt |
|---|---|
| Förklara loopar. | Du är lärare i programmering. Förklara `for`-loopar i JavaScript för en nybörjare på gymnasiet. Använd ett exempel med en array och högst fem meningar. |
| Skriv kod för en temperatur. | Skriv en JavaScript-funktion som tar en temperatur och ett gränsvärde och returnerar `true` om temperaturen är högre. Skriv också tre testfall. |

Tydliga prompter säger **vem** modellen ska vara, **vad** den ska göra, ger **sammanhang** och beskriver **formatet** på svaret. Gör det i steg om uppgiften är stor, och be om förklaringar. Du är ansvarig för det du lämnar in, så förstår du inte koden ska du inte använda den.

## Anropa en språkmodell från JavaScript

En språkmodell nås oftast genom ett HTTP-API, alltså på samma sätt som i [kapitel 8](08-http-databas-webbapp.md). Ett anrop skickar en lista med meddelanden med olika **roller**: `system` för övergripande instruktioner, `user` för det användaren skriver och `assistant` för modellens tidigare svar. Modellen minns inget mellan anrop, så i en chatt måste du skicka hela historiken varje gång.

Många tjänster följer ungefär samma format. Så här kan ett anrop se ut i Node.js, med inställningarna i **miljövariabler** så att de inte hamnar i koden:

```js
const ADRESS = process.env.AI_ADRESS;
const NYCKEL = process.env.AI_NYCKEL;
const MODELL = process.env.AI_MODELL;

async function fragaModellen(meddelanden) {
  const svar = await fetch(`${ADRESS}/chat/completions`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${NYCKEL}`,
    },
    body: JSON.stringify({ model: MODELL, messages: meddelanden }),
  });

  if (!svar.ok) {
    throw new Error(`API-fel: status ${svar.status}`);
  }

  const data = await svar.json();
  return data.choices[0].message.content;
}

const historik = [
  { role: "system", content: "Du är en vänlig studiehjälp som svarar kort på svenska." },
  { role: "user", content: "Vad är en loop?" },
];

try {
  const text = await fragaModellen(historik);
  historik.push({ role: "assistant", content: text });
  console.log(text);
} catch (fel) {
  console.log("Något gick fel:", fel.message);
}
```

Spara filen som `chatt.mjs` och kör den med `node chatt.mjs`. Filändelsen `.mjs` behövs för att `await` ska få stå utanför en funktion. Vad adress, nyckel och modellnamn ska vara beror på tjänsten du använder, och det får du från kursens material.

**Nyckeln är en hemlighet.** Kod som körs i webbläsaren är synlig för alla som besöker sidan, så en nyckel där är röjd. I en riktig app låter du därför en liten server göra anropet och håller nyckeln där. Lägg aldrig en nyckel i kod du pushar till GitHub, och behandla den som röjd om det ändå händer, enligt [kapitel 6](06-versionshantering.md).

Vill du ha svar som ett program kan använda ber du modellen om **strukturerad output** i JSON. Eftersom modellen ibland ändå svarar med något annat måste du använda `JSON.parse` inom `try` och `catch`.

Två tekniker till, som kursmaterialet tar upp, är **RAG**, där du låter modellen läsa dina egna dokument, och **tool calling**, där modellen kan be ditt program att köra en funktion.

## Programmering och samhälle

Program påverkar verkliga människor, ofta utan att de märker det. De avgör vilka nyheter du ser, vem som kallas till intervju och vilka som får lån. Den som bygger systemet har gjort många val på vägen, och de valen är inte neutrala.

**Genus.** Ett system tränat på historisk data lär sig även historiska fördomar. Forskningsprojektet [Gender Shades](http://gendershades.org/) visade att flera kommersiella system för ansiktsanalys fungerade sämre för kvinnor med mörk hud än för män med ljus hud. Fundera också på hur ett formulär frågar om kön och vilka röster och namn som är förval.

**Kultur och språk.** Hanterar din app namn med å, ä och ö eller med bokstäver från andra alfabet? Fungerar den på andra språk än engelska? En språkmodell är ofta bäst på det språk den tränats mest på.

**Socioekonomisk bakgrund.** Alla har inte den senaste telefonen, snabbt nät eller råd med en betaltjänst. Om bara de med tid och pengar kan använda en tjänst förstärks skillnader. Den som har haft tillgång till dator och kurser hemma har dessutom lättare att komma in i programmering, vilket påverkar vilka som bygger systemen.

**Tillgänglighet.** En sida som inte går att använda med skärmläsare utestänger människor. Därför finns också krav och standarder, till exempel [WCAG](https://www.w3.org/WAI/standards-guidelines/wcag/).

**Integritet.** Sparar du personuppgifter måste du ha en anledning och skydda dem. [GDPR](https://www.imy.se/verksamhet/dataskydd/det-har-galler-enligt-gdpr/) gäller i hela EU. Skicka aldrig andras personuppgifter till en AI-tjänst utan att tänka igenom var de hamnar.

**Att använda AI som hjälp.** Det är lätt att låta en modell skriva all kod. Men om du inte förstår den kan du inte felsöka den eller ta ansvar för den. Använd AI för att få förklaringar, inte för att slippa tänka, och följ skolans regler för hjälpmedel.

### Etisk analys steg för steg

När du ställs inför ett svårt val kan du fråga dig:

1. **Vilka berörs** av programmet, även de som inte själva använder det?
2. **Vad kan gå fel**, och vem drabbas i så fall?
3. **Vilka alternativ finns?** Kanske går det att samla in mindre data eller att låta en människa fatta beslutet.
4. **Vad skulle du tycka** om du var den som drabbades?

Organisationen ACM har skrivit en [etisk kod](https://www.acm.org/code-of-ethics) för yrkesverksamma, som går igenom liknande frågor mer utförligt.

## Begrepp

- **Generativ AI:** system som skapar nytt innehåll
- **LLM:** en stor språkmodell som förutsäger nästa token
- **Token:** en ordbit som modellen arbetar med
- **Prompt:** instruktionen du ger modellen
- **Hallucination:** när modellen hittar på något som låter sant
- **Bias:** snedvridning som kommer från data eller från hur systemet har byggts
- **Miljövariabel:** en inställning som läses från systemet i stället för koden
- **Personuppgift:** information som kan knytas till en levande person

## Testa dig själv

1. Varför kan en språkmodell ge ett felaktigt svar som ändå låter rätt?
2. Vad är skillnaden mellan rollerna `system`, `user` och `assistant`?
3. Varför måste en chatt skicka hela historiken vid varje anrop?
4. Varför får API-nyckeln inte ligga i kod som körs i webbläsaren?
5. Ge ett exempel på hur ett program kan missgynna en grupp människor.
6. Vilka frågor kan du ställa för att analysera en etisk fråga?
7. När är det rimligt att använda AI som hjälp i en programmeringsuppgift, och när är det inte det?

## Koppling till projektet

Kapitlet förbereder [Generativ AI](../projekt/generativ-ai/README.md), där du bygger och presenterar en egen AI-app. Delen om samhälle hör ihop med [Etik](../projekt/etik/README.md) och med kursens syfte om sociala aspekter av programmering.

## Läs mer

- [Kursens material om generativ AI](https://github.com/abbjetmus/Generative-AI-Hitachigymnasiet)
- [Generative AI with JavaScript: lektioner](https://github.com/abbjetmus/generative-ai-with-javascript/tree/main/lessons)
- [Gender Shades](http://gendershades.org/)
- [IMY: Det här gäller enligt GDPR](https://www.imy.se/verksamhet/dataskydd/det-har-galler-enligt-gdpr/)
- [ACM Code of Ethics](https://www.acm.org/code-of-ethics)

[← Föregående](09-spel-och-objekt-i-godot.md) | [Innehåll](../README.md)
