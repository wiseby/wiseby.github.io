---
title: "3D-Printing, grundkurs för körkort"
excerpt: "En kurs i hanteringen av 3D-Skrivare"
date: 2026-10-19
categories:
  - verkstaden
  - artiklar
tags:
  - 3d-printing
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

## Mål och syfte

I denna kurs kommer vi att gå igenom de grundläggande komponenterna som gör utskrift av 3D modeller möjligt i en så kallad FDM-skrivare. Efter genomförd kurs kommer deltagarna att ha kunskapen att hantera skrivaren på ett korrekt och säkert sätt. Denna kursen är obligatorisk att genomföra för att man ska kunna ta ett körkort för att kunna nyttja skrivaren utan ledare/instruktör.

Kursens syfte är att bygga en grund och öka förståelsen av skrivaren

Målet är att få den teoretiska grund för att gå vidare till den praktiska delen i att ta ett körkort för skrivaren.

## Innehåll

Vi kommer bland annat att..
- gå igenom de fysiska komponenterna som utgör en FDM-skrivare
- lära oss om vilka begränsningar som finns
- starta utskrifter och de grundläggande momenten för att ställa in skrivaren
- 

## Skrivarens konstruktion

En 3D-Skrivare är precis vad det låter som, den tillåter utskrift i tre dimensioner. Till skillnad från en traditionell pappersskrivare som enbart skriver i två dimensioner. I denna kurs kommer vi att gå igenom en variant av 3d-skrivare som använder tekniken Fuse Deposition Modeling (FDM). Detta innebär att den tillsätter material (Additiv Tillverkning) för att skapa ett fysiskt objekt. Motsattsen (Subtraktiv Tillverkning) utgår ifrån ett större ämne där material plockas bort.

Jag brukar dra liknelsen med en limpistol där man kan limma i flera lager för att bygga upp något på höjden. Föreställ dig också att man kan montera limpistolen i en ram som tillåter exakta rörelser i bredd, djup och höjd, där har du hela grundprincipen på hur en 3d-skrivare fungerar.

I denna kursen kommer vi att utgå från en Bambulab P2S med AMS.

### De fysiska grund-komponenterna

Grundkomponenter:

- Hotend (Den varma delen med munstycke)
- Extruder (Extruderare som matar plasten)
- Heatbed (Värmebädd)
- X-axel (rör munstycket i X-axel med stegmotor)
- Y-axel (rör munstycket i Y-axel med stegmotor)
- Z-axel (rör bädden up och ner)

Extra utrustning:

- Multimaterial-station (hanterar rullarna med plast och byter automatiskt vid behov)
- Filament torkar

En Bambulab P2S är en så kallad Core-XY skrivare, detta vill säga att X och Y axlarna sitter ihop på ett unikt sätt för att kunna jobba med högre hastigheter och accelerationer. Den har en direkt-driven extruder som sitter ihop med den varma delen (hotend) i ett kompakt "huvud" som rör sig över utskriftsytan, detta är vår "limpistol".

![Bambulab P2S Extruder Head](/assets/images/printing/bambu_p2s_extruder.jpg "Bambulab P2S Extruder Head")

Bädden sitter ihop och rör sig i höjd (Z axel) och är uppvärmd för att förbättra vidhäftningen av plasten som läggs där på. Den översta ytan är en tunnare, flexibel stålskiva som ska vara lätt att ta ur skrivaren. Denna kommer med lite olika behandlingar beroende på vilken plast man använder. I detta grundutförande så är den av typen PEI med rugglig struktur. Detta ska göra att utskrifterna sitter bra när temperaturen är lite högre, men är lätt att få bort när den svalnar.

![Bambulab P2S Värmebädd](/assets/images/printing/bambu_p2s_heatbed.jpg "Bambulab P2S Värmebädd")

Displayen har touch navigering och används för att:

- Se status för pågående utskrift
- Kontrollera och förbereda
- Manuellt köra funktioner
- Starta ny utskrift

![Bambulab P2S Display](/assets/images/printing/bambu_p2s_display.jpg "Bambulab P2S Display")

