# Projekt: Hetaste Laget PROG

## Syfte

I hetaste laget är ett IoT-projekt, Internet of Things, som du gör tillsammans med kursen Teknik 1. Du bygger en uppkopplad termometer: en ESP8266 läser temperatur och luftfuktighet från en AM2320-sensor, skickar värdena via HTTP till en databas, och du visar dem i en egen webbapp. I programmeringsdelen ansvarar du för koden hela vägen från sensor till skärm.

## Koppling till kursen

**Kriterier i vanliga ord**

- Du visar att du förstår hur mikrokontrollern, webbappen och databasen hänger ihop, och vad som skiljer språken du använder åt (kriteriet om programmerbara system, programspråk och programmeringsparadigm).
- Du formulerar och löser de programmeringsproblem som dyker upp längs vägen (kriteriet om att formulera och lösa problem).
- Du skapar ett gränssnitt som är användbart och tydligt för den som ska läsa av temperaturen (kriteriet om anpassning till syfte, användare och tillgänglighet).

**Centralt innehåll:** samspelet mellan program, exekveringsmiljö, operativsystem och hårdvara, programmering i flera språk, verktyg för programutveckling, felsökning, undantagshantering, god struktur och gränssnitt mot användaren.

**Kapitel som förbereder**

- [Kapitel 7: Mikrokontrollern, ESP8266 och C++](../../kapitel/07-esp8266-och-cpp.md)
- [Kapitel 8: HTTP, databaser och webbappar](../../kapitel/08-http-databas-webbapp.md)
- [Kapitel 6: Versionshantering med Git och GitHub](../../kapitel/06-versionshantering.md)
- [Kapitel 5: DOM och användargränssnitt](../../kapitel/05-dom-och-granssnitt.md)

## Vad du ska göra

- Programmera ESP8266 i C++ i Arduino IDE så att den läser sensorn och kopplar upp sig mot Wi-Fi.
- Skicka mätvärdena till en databas eller ett API över HTTP.
- Bygga en webbapp, med Vue eller HTML, CSS och JavaScript, som hämtar och presenterar värdena.
- Låta användaren ändra minst en parameter i gränssnittet, till exempel ett gränsvärde eller mätintervall.
- Kommentera din kod och versionshantera den på GitHub.

## Krav och leverabler

- Ett fungerande system från sensor till skärm, som du visar upp.
- Din kommenterade kod, inlämnad via GitHub.
- En webbapp där användaren kan ändra minst en parameter.

## Arbetsgång

| Lektion | Innehåll |
|---|---|
| 1 | Projektstart: genomgång av I hetaste laget och målbilden. Installera Arduino IDE med ESP8266-stöd och få en lysdiod att blinka. |
| 2 | C++ för Arduino: setup, loop, variabler och funktioner. Koppla in AM2320 och skriv ut temperatur och luftfuktighet i Serial Monitor. |
| 3 | HTTP och API:er: hur en förfrågan fungerar, fetch och async/await i JavaScript. Gör övningarna i mappen HTTP och APIer. |
| 4 | Koppla upp ESP8266 mot Wi-Fi och skicka mätvärden till databasen. Testa hela flödet med exemplet i projektmappen. |
| 5 | Bygg webbappen: hämta temperaturvärdena från databasen och visa dem på sidan (Vue eller HTML/CSS/JavaScript med Bootstrap). |
| 6 | Eget arbete: låt användaren ändra en parameter i gränssnittet, till exempel gränsvärde eller mätintervall. Avstämning med läraren. |
| 7 | Eget arbete: presentera värdena tydligare, till exempel med historik eller diagram, och förbättra design och användbarhet. |
| 8 | Avstämning: visa hur långt du kommit, kommentera koden, pusha till GitHub och skriv ner vad som återstår. |
| 9–14 | Innehållet i de här lektionerna är inte fastställt i planeringen. Läraren meddelar vad som gäller. |
| 15 | Färdigställande: testa hela systemet från sensor till skärm och förbered redovisningen av programmeringsdelen. |

## Bedömning

Du visar upp ett fungerande system och lämnar in din kommenterade kod. Bedömningen gäller hur du löser problemen längs vägen, hur väl du förstår hur mikrokontrollern, webbappen och databasen hänger ihop och skillnaden mellan språken du använder, samt hur användbart och tydligt gränssnittet är för den som ska läsa av temperaturen.

## Material

- [Kursens repo på GitHub](https://github.com/abbindustrigymnasium/programmering1)
- [Projekt Temperatursensor](https://github.com/abbindustrigymnasium/programmering1/tree/main/Projekt-Temperatur-Sensor), med exempelkod och [övningar med Firebase](https://github.com/abbindustrigymnasium/programmering1/tree/main/Projekt-Temperatur-Sensor/Exempel/%C3%96vningar)
- [ESP8266-guide och övningar](https://github.com/abbindustrigymnasium/programmering1/tree/main/ESP8266)
- [C++: genomgång och övningar](https://github.com/abbindustrigymnasium/programmering1/tree/main/C%2B%2B)
- [HTTP och API:er: genomgång och övningar](https://github.com/abbindustrigymnasium/programmering1/tree/main/HTTP%20och%20APIer)
- [Vue](https://github.com/abbindustrigymnasium/programmering1/tree/main/Vue) och [Bootstrap](https://github.com/abbindustrigymnasium/programmering1/tree/main/Bootstrap)
- [Teknik 1: I hetaste laget](https://github.com/abbindustrigymnasium/teknik1/tree/main/I%20hetaste%20laget), med instruktionen för AM2320

## Tips

- Bygg i små delar: läs sensorn, skicka ett påhittat värde till databasen och hämta det till webbappen. Koppla ihop delarna först när var och en fungerar.
- Behåll Wi-Fi-lösenord och nycklar i en fil som står i `.gitignore`.
- Ha databasens konsol öppen medan du arbetar, så ser du om värdena kommer fram.
- Tänk på vad gränssnittet ska visa om sensorn slutat skicka. En gammal temperatur får inte se ut som en ny.

[Tillbaka till innehållet](../../README.md)
