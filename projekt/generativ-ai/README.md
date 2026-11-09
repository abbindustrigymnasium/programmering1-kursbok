# Projekt: Generativ AI

## Syfte

Generativ AI, som ChatGPT och Copilot, kan skapa text, bilder och kod. I det här projektet lär du dig hur stora språkmodeller fungerar, hur du skriver bra prompter och vilka begränsningar AI har. Sedan använder du det du kan i JavaScript för att själv bygga en app som anropar en AI-modell via ett API.

## Koppling till kursen

**Kriterier i vanliga ord**

- Du formulerar och löser ett problem i koden (kriteriet om att formulera och lösa problem).
- Appen är anpassad till sitt syfte och till dem som ska använda den (kriteriet om anpassning till syfte, användare och tillgänglighet).

**Centralt innehåll:** programmering i textbaserat språk, skapande av program som löser en uppgift, undantagshantering, gränssnitt mot användaren och sociala aspekter av hur programmering används.

**Kapitel som förbereder**

- [Kapitel 10: Generativ AI, etik och samhälle](../../kapitel/10-generativ-ai-och-etik.md)
- [Kapitel 8: HTTP, databaser och webbappar](../../kapitel/08-http-databas-webbapp.md)
- [Kapitel 5: DOM och användargränssnitt](../../kapitel/05-dom-och-granssnitt.md)

## Vad du ska göra

- Lära dig grunderna: vad en LLM är, prompter, tokens, hallucinationer och bias.
- Öva promptteknik och jämföra hur olika prompter påverkar svaret.
- Köra och bygga vidare på lärarens exempel där en webbsida anropar en språkmodell från JavaScript.
- Planera och bygga en egen AI-app som löser ett verkligt eller kreativt problem, till exempel en studiehjälp, en chatbot för ett ämne eller ett quizspel.
- Presentera och demonstrera din app för klassen.

## Krav och leverabler

- Appen anropar en AI-modell via ett API och är byggd med JavaScript.
- Appen löser ett verkligt eller kreativt problem.
- Du skriver en kort plan: vilket problem appen löser, för vem och vilka funktioner den ska ha.
- Koden är kommenterad och pushad till GitHub.
- Du presenterar och demonstrerar appen för klassen.

## Arbetsgång

| Lektion | Innehåll |
|---|---|
| 1 | Introduktion: vad är AI och generativ AI och hur fungerar stora språkmodeller? Testa olika AI-verktyg och diskutera vad de kan användas till. |
| 2 | Promptteknik: skriv tydliga och stegvisa prompter och jämför resultaten. Diskutera hallucinationer, bias och källkritik. |
| 3 | Din första AI-app: kör lärarens exempel där en webbsida anropar en språkmodell via API från JavaScript. |
| 4 | Bygg vidare på exemplet: en chatt med systemprompt och konversationshistorik som visas på sidan. |
| 5 | Promptteknik i kod och strukturerad output (JSON) enligt lektion 3 och 4 i Generative AI with JavaScript. |
| 6 | Översikt över RAG och tool calling (lektion 5 och 6) som inspiration. Spåna idéer till ditt eget projekt. |
| 7 | Välj projektidé och skriv en kort plan: vilket problem appen löser, för vem och vilka funktioner den ska ha. Stäm av med läraren. |
| 8 | Eget projekt: bygg grundfunktionen med anropet till AI-modellen och ett enkelt gränssnitt. |
| 9 | Eget projekt: fortsätt bygga funktionerna. Avstämning med läraren. |
| 10 | Eget projekt: förbättra gränssnittet och låt en klasskamrat testa appen. |
| 11 | Färdigställ projektet: åtgärda feedback, felsök, kommentera koden och pusha till GitHub. |
| 12 | Gör klart appen och förbered presentationen: demo och förklaring av hur appen använder AI. |
| 13 | Redovisning: presentera och demonstrera din AI-app för klassen. |

## Bedömning

Bedömningen bygger på ditt eget projekt och din presentation: hur du formulerar och löser problemet i koden, och hur väl appen är anpassad till sitt syfte och till dem som ska använda den.

## Material

- [Kursmaterial om generativ AI](https://github.com/abbjetmus/Generative-AI-Hitachigymnasiet)
- [Presentation](https://github.com/abbjetmus/Generative-AI-Hitachigymnasiet/blob/main/Generativ-AI-Presentation.pptx)
- [Generative AI with JavaScript](https://github.com/abbjetmus/generative-ai-with-javascript)
- [Lektionerna i Generative AI with JavaScript](https://github.com/abbjetmus/generative-ai-with-javascript/tree/main/lessons)

## Tips

- Börja med en app som bara gör ett anrop och visar svaret. Bygg sedan vidare.
- Testa vad som händer när modellen svarar något oväntat eller när anropet misslyckas.
- Håll API-nyckeln borta från GitHub och från kod som körs i webbläsaren.
- Fundera på vem appen kan missleda om modellen gissar fel, och visa användaren att svaret kommer från en AI.

[Tillbaka till innehållet](../../README.md)
