# Kapitel 7: Mikrokontrollern, ESP8266 och C++

> **I det här kapitlet lär du dig**
> - vad en mikrokontroller är och hur den skiljer sig från en dator
> - hur ett program för ESP8266 är uppbyggt
> - vad som skiljer C++ från JavaScript
> - att läsa en sensor och koppla upp mot Wi-Fi
> - att mäta tid utan att stoppa programmet

Din telefon och din dator kör miljontals rader kod från många olika företag. En mikrokontroller gör mycket mindre, men det är du som skriver allt den ska göra. När programmet körs är det ditt program som tänder lysdioden, läser sensorn och skickar värdet ut på nätet. Det är programmering nära hårdvaran.

## Vad är en mikrokontroller?

En **mikrokontroller** är en liten dator på ett enda chip, med processor, minne och in- och utgångar. **ESP8266** är en mikrokontroller med inbyggt Wi-Fi. Den brukar sitta på ett utvecklingskort, ofta kallat **NodeMCU**, som har USB-anslutning och stift du kan koppla komponenter till.

Skillnaderna mot en vanlig dator är stora, och de påverkar hur du skriver kod:

| | Dator | ESP8266 |
|---|---|---|
| Operativsystem | Ja, till exempel Windows | Inget i vanlig mening, ditt program körs direkt |
| Arbetsminne | Flera gigabyte | Några tiotals kilobyte ledigt |
| Lagring | Stora diskar | Begränsat flashminne |
| Skärm | Ja | Nej, du skriver till datorn via Serial Monitor |
| Spänning på stift | Inte aktuellt | 3,3 V, och stiften tål inte högre utan vidare |

Det är de här begränsningarna som [kapitel 1](01-datorn-och-webben.md) pratade om. Eftersom programmet måste rymmas i det lilla minnet väljer du variabeltyper mer noggrant och skickar iväg data i stället för att spara den på kortet.

Du programmerar kortet i **Arduino IDE**, som kompilerar din kod till maskinkod och laddar över den via USB. Stegen för att installera stöd för ESP8266 finns i [ESP8266-guiden](https://github.com/abbindustrigymnasium/programmering1/tree/main/ESP8266).

## Programmets struktur: setup och loop

Ett Arduino-program har alltid två funktioner. `setup()` körs en gång när kortet startar och `loop()` körs om och om igen, så länge kortet har ström.

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);   // Stiftet ska användas som utgång
}

void loop() {
  digitalWrite(LED_BUILTIN, LOW);   // Tänder den inbyggda lysdioden
  delay(500);                       // Väntar 500 millisekunder
  digitalWrite(LED_BUILTIN, HIGH);  // Släcker
  delay(500);
}
```

Att `LOW` tänder lysdioden kan verka bakvänt. På NodeMCU-kortet är den inbyggda lysdioden kopplad så att den lyser när stiftet är lågt. Det är en sådan detalj som bara dokumentationen kan berätta. Lysdioden blinkar en gång per sekund: 500 ms tänd och 500 ms släckt.

## C++ jämfört med JavaScript

Kontrollstrukturerna känner du igen från [kapitel 3](03-javascript-grunder.md). Skillnaderna ligger i typerna och i hur koden körs:

| | JavaScript | C++ |
|---|---|---|
| Typer | Dynamiska: `let t = 21.5;` | Statiska: `float t = 21.5;` |
| Körning | Motorn i webbläsaren | Kompileras till maskinkod i förväg |
| Fel upptäcks | Oftast under körning | Många redan vid kompilering |
| Utskrift | `console.log("hej")` | `Serial.println("hej");` |
| Text | `string` | `String` eller tecken-arrayer |

Vanliga typer är `int` (heltal), `float` (decimaltal), `bool` (sant eller falskt) och `unsigned long` (stora heltal utan tecken). Eftersom typerna är bestämda hittar kompilatorn många fel åt dig. C++ stöder också klasser och objekt, och du kan läsa mer i [C++-mappen](https://github.com/abbindustrigymnasium/programmering1/tree/main/C%2B%2B).

## Läsa en sensor

En **sensor** mäter något i omvärlden. I [Hetaste Laget PROG](../projekt/hetaste-laget/README.md) används AM2320, som mäter temperatur och luftfuktighet och kommunicerar med mikrokontrollern över en buss som heter **I2C**. Ett **bibliotek** är färdig kod som någon annan har skrivit och som du återanvänder.

**Genomgånget exempel.** Programmet läser sensorn var femte sekund utan att blockera `loop()`. Det använder biblioteket AM2320 och samma stift som i Teknik 1-materialet.

```cpp
#include <Wire.h>
#include <AM2320.h>

const unsigned long MATINTERVALL_MS = 5000;

AM2320 sensor;
unsigned long senasteMatning = 0;

void setup() {
  Serial.begin(115200);
  Wire.begin(14, 12);   // SDA på GPIO14, SCL på GPIO12
  delay(2000);          // Ge sensorn tid att starta
}

void loop() {
  unsigned long nu = millis();
  if (nu - senasteMatning >= MATINTERVALL_MS) {
    senasteMatning = nu;
    lasSensor();
  }
}

void lasSensor() {
  if (sensor.measure()) {
    float temperatur = sensor.getTemperature();
    float luftfuktighet = sensor.getHumidity();
    Serial.print("Temperatur: ");
    Serial.print(temperatur);
    Serial.print(" °C, luftfuktighet: ");
    Serial.print(luftfuktighet);
    Serial.println(" %");
  } else {
    Serial.print("Sensorfel, kod: ");
    Serial.println(sensor.getErrorCode());
  }
}
```

Gå igenom koden:

- **`#include`** tar in biblioteken. `Wire` sköter I2C.
- **`const unsigned long`** gör att intervallet har ett namn och inte blir ett magiskt tal.
- **`Serial.begin(115200)`** startar kommunikationen med datorn. Serial Monitor måste vara inställd på samma hastighet, annars ser du bara konstiga tecken.
- **Felhanteringen** är viktig. Sensorn kan misslyckas, och då ska programmet säga det, inte skicka iväg gamla värden.

Stämmer inte din koppling med stiften i koden ändrar du siffrorna i `Wire.begin(...)`. Kopplingen beskrivs i Teknik 1-materialet [Mäta temperatur med AM2320](https://github.com/abbindustrigymnasium/teknik1/tree/main/I%20hetaste%20laget). I kursens repo finns också en övning med [sensorn DHT11](https://github.com/abbindustrigymnasium/programmering1/blob/main/ESP8266/%C3%B6vningar/%C3%B6vning2-luftfuktighet.md). Hör med läraren vilken sensor som gäller för dig.

### Varför inte delay?

`delay(5000)` skulle stoppa programmet i fem sekunder. Under tiden kan det inte reagera på något annat. `millis()` returnerar i stället antalet millisekunder sedan kortet startade, och koden kollar om tillräckligt lång tid har gått.

Räkningen är säker. `millis()` lagras i 32 bitar och börjar om från noll efter 2³² ms, vilket är ungefär 49,7 dygn. Eftersom subtraktionen `nu - senasteMatning` görs med **unsigned long** blir resultatet rätt även över en sådan omstart.

## Koppla upp mot Wi-Fi

```cpp
#include <ESP8266WiFi.h>
#include "secrets.h"    // WIFI_NAMN och WIFI_LOSENORD finns här

void anslutWifi() {
  WiFi.begin(WIFI_NAMN, WIFI_LOSENORD);
  Serial.print("Ansluter");
  while (WiFi.status() != WL_CONNECTED) {
    delay(300);
    Serial.print(".");
  }
  Serial.println();
  Serial.print("IP-adress: ");
  Serial.println(WiFi.localIP());
}
```

Lägg uppgifterna i en separat fil `secrets.h` och skriv in filen i `.gitignore`, enligt [kapitel 6](06-versionshantering.md). Då kan du dela koden utan att dela lösenordet. Anropa `anslutWifi()` från `setup()`.

## Felsökning på hårdvara

När något inte fungerar kan felet sitta i koden, i kopplingen, i kabeln eller i biblioteket. Arbeta systematiskt:

1. Fungerar ett enkelt blink-program? Då är kort och kabel okej.
2. Får du ut något i Serial Monitor? Stämmer hastigheten?
3. Kompileras koden men sensorn svarar inte? Kontrollera kopplingen och att spänningen är 3,3 V.
4. Testa en sak i taget, och ändra bara en sak i taget.

## Begrepp

- **Mikrokontroller:** en liten dator på ett enda chip, gjord för att styra saker
- **ESP8266:** en mikrokontroller med inbyggt Wi-Fi
- **Stift (pin):** en anslutning på kortet som kopplas till komponenter
- **Serial Monitor:** ett fönster i Arduino IDE som visar utskrifter från kortet
- **Sensor:** en komponent som mäter något i omvärlden
- **I2C:** en buss som låter komponenter prata med mikrokontrollern
- **Bibliotek:** färdig kod som du återanvänder
- **Statisk typning:** att typen bestäms när koden skrivs

## Testa dig själv

1. Vad är skillnaden mellan `setup()` och `loop()`?
2. Varför måste du tänka mer på minnet på en ESP8266 än i en webbläsare?
3. Vad är skillnaden mellan `delay` och `millis`?
4. Varför används `unsigned long` för tid?
5. Varför ska Wi-Fi-lösenordet ligga i en separat fil?
6. Vad ska programmet göra om sensorn inte svarar?
7. Hur tar du reda på om ett problem sitter i koden eller i kopplingen?

## Övningar

Övningar finns i [C++-övningarna](https://github.com/abbindustrigymnasium/programmering1/tree/main/C%2B%2B/%C3%B6vningar) och [ESP8266-övningarna](https://github.com/abbindustrigymnasium/programmering1/tree/main/ESP8266/%C3%B6vningar).

**Grund 1.** Gör övningen att blinka en lysdiod på ESP8266.

**Grund 2.** Gör C++-övningarna om variabler, if-satser och loopar.

**Grund 3.** Ett program mäter var femte sekund. Hur många mätningar blir det på ett dygn? Hur många byte blir det om varje mätning tar 50 byte när den sparas?

<details><summary>Svar</summary>Ett dygn har 86 400 sekunder, så det blir 86 400 / 5 = 17 280 mätningar. 17 280 · 50 = 864 000 byte, alltså 864 kB per dygn.</details>

**Vidare 4.** Läs av sensorn och skriv ut temperatur och luftfuktighet i Serial Monitor.

**Vidare 5.** Lägg till en lysdiod som lyser när temperaturen är över ett gränsvärde. Skriv gränsvärdet som en konstant.

**Utmaning 6.** Använd `millis()` för att låta en lysdiod blinka varje sekund samtidigt som sensorn läses var femte sekund, utan `delay` i `loop()`.

## Koppling till projektet

Kapitlet täcker den första delen av [Hetaste Laget PROG](../projekt/hetaste-laget/README.md), från att få en lysdiod att blinka till att läsa sensorn och koppla upp mot Wi-Fi.

## Läs mer

- [ESP8266 Arduino Core: dokumentation](https://arduino-esp8266.readthedocs.io/en/latest/)
- [Arduino: referens för språket](https://docs.arduino.cc/language-reference/)
- [Biblioteket AM2320](https://github.com/hibikiledo/AM2320)
- [C++ från grunden: learncpp.com](https://www.learncpp.com/)

[← Föregående](06-versionshantering.md) | [Innehåll](../README.md) | [Nästa →](08-http-databas-webbapp.md)
