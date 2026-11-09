# Projekt: 2D-Spel

## Syfte

Du utvecklar ett eget 2D-spel i spelmotorn Godot och programmerar det i GDScript. Du kombinerar programmering med kreativt skapande: spelmekanik, grafik, ljud och gränssnitt. Du får återskapa ett känt spel eller hitta på ett eget, men du får inte hämta färdig kod från nätet.

Projektet delas med kursen Digitalt Skapande Nivå 1. Den här beskrivningen utgår från vad Programmering nivå 1 kräver.

## Koppling till kursen

**Kriterier i vanliga ord**

- Du visar att du förstår Godots objektorienterade uppbyggnad med noder och scener och hur ett spel körs (kriteriet om programmerbara system, programspråk och programmeringsparadigm).
- Du formulerar och löser programmeringsproblemen i spelet (kriteriet om att formulera och lösa problem).
- Spelet är anpassat till spelaren, till exempel med tydliga menyer och kontroller (kriteriet om anpassning till syfte, användare och tillgänglighet).

**Centralt innehåll:** strukturerad problemlösning, pseudokod och diagramteknik, kontrollstrukturer, felsökning, namngivning och strukturerad kod, gränssnitt mot användaren och samspelet mellan program och hårdvara.

**Kapitel som förbereder**

- [Kapitel 9: Spel och objekt i Godot](../../kapitel/09-spel-och-objekt-i-godot.md)
- [Kapitel 4: Problemlösning, felsökning och god kod](../../kapitel/04-problemlosning-och-felsokning.md)
- [Kapitel 3: JavaScript-grunder](../../kapitel/03-javascript-grunder.md), för kontrollstrukturerna

## Vad du ska göra

- Gå igenom Godots tutorial för ditt första 2D-spel.
- Planera ditt spel i ett dokument med beskrivning, skiss och gärna pseudokod eller flödesschema, och få det godkänt.
- Bygga spelmekanik: rörelse, kollisioner, mål och vinst- eller förlustvillkor.
- Lägga till sprites och animation, startskärm och game over-skärm, ljud och musik, fiender eller samlarföremål samt scenbyten.
- Exportera spelet till en körbar `.exe`-fil och lämna in koden på GitHub.

## Krav och leverabler

Kraven finns i sin helhet i [guiden till projektet](https://github.com/abbjetmus/Godot-2D-Spel). I korthet ska spelet ha:

| Del | Krav |
|---|---|
| Planering | Dokument med beskrivning och skiss, godkänt av läraren |
| Spelmekanik | Rörelse med tangenter eller touch, kollisioner, ett mål och vinst- eller förlustvillkor |
| Grafik | Sprites för spelare, fiender och bakgrund och minst en enkel animation. Tileset är valfritt |
| Gränssnitt | Startskärm med Starta-knapp och game over-skärm. HUD med poäng eller tid är valfritt |
| Ljud | Ljudeffekter för händelser i spelet och bakgrundsmusik |
| Spelelement | Fiender som rör sig, samlarföremål och enkel fysik om det behövs |
| Scener | Byte mellan nivåer eller omstart av spelet |
| Leverans | Körbar fil så att andra kan testa, koden på GitHub |

## Arbetsgång

| Lektion | Innehåll |
|---|---|
| 1 | Projektstart: genomgång av 2D-spelprojektet och kraven. Installera Godot och lär dig noder, scener och ditt första GDScript. |
| 2 | Tutorial Your first 2D game i Godot Docs: skapa spelaren och styr den med tangentbordet. |
| 3 | Fortsätt tutorialen: fiender, signals, HUD och poäng. Gör klart ditt första spel. |
| 4 | Återstart: vi bygger ett enkelt spel tillsammans och repeterar variabler, villkor och kollisioner i GDScript. |
| 5 | Planering: skriv ett dokument med spelidé, skiss och pseudokod eller flödesschema för spelets logik. Få planen godkänd av läraren. |
| 6 | Bygg grundläggande spelmekanik: spelarens rörelse, kollisioner, spelets mål och vinst- eller förlustvillkor. |
| 7 | Grafik: lägg in sprites för spelare, fiender och bakgrund och gör minst en enkel animation. |
| 8 | Användargränssnitt: startskärm med Starta-knapp, game over-skärm och gärna en HUD med poäng eller tid. |
| 9 | Eget arbete och avstämning: visa ditt spel för läraren och bocka av kraven du har klarat. |
| 10 | Spelelement: fiender som rör sig, samlarföremål och enkel fysik som hopp och gravitation. |
| 11 | Ljud: lägg till ljudeffekter för till exempel hopp och kollision samt bakgrundsmusik. |
| 12 | Scen- och nivåhantering: byt mellan nivåer och låt spelaren starta om. |
| 13 | Eget arbete: felsök, kommentera koden och låt en klasskamrat testspela ditt spel. |
| 14 | Färdigställande: åtgärda feedbacken från testspelningen och putsa grafik, ljud och menyer. |
| 15 | Exportera spelet till en `.exe`-fil, pusha koden till GitHub och förbered redovisningen. |
| 16 | Redovisning: visa ditt spel, låt andra testa det och berätta hur du löste spelmekaniken. |

## Bedömning

Du redovisar spelet och låter andra testa det. Bedömningen gäller hur du löser programmeringsproblemen i spelet, hur du använder Godots objektorienterade uppbyggnad med noder och scener, och hur väl spelet är anpassat till spelaren, till exempel med tydliga menyer och kontroller.

## Material

- [Guide till Godot, krav och förmågor](https://github.com/abbjetmus/Godot-2D-Spel)
- [Godot Docs: Your first 2D game](https://docs.godotengine.org/en/stable/getting_started/first_2d_game/index.html)
- [GDScript-tutorials](https://gdscript.com/tutorials/)

## Tips

- Börja med det enklaste spelet som går att vinna och förlora, och bygg sedan vidare.
- Rita ett tillståndsdiagram tidigt. Det avslöjar saker du glömt, som vad som händer efter game over.
- Skriv ner vilken version av Godot du använder. Exempel på nätet för äldre versioner kan använda andra namn, till exempel `KinematicBody2D` där Godot 4 har `CharacterBody2D`.
- Låt någon annan spela i god tid före redovisningen.

[Tillbaka till innehållet](../../README.md)
