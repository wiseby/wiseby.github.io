---
layout: post
title: "3D Printing - En Introduktion"
categories: ["3D-Printing"]
---

## Intro?



## Tekniken bakom den tredje dimensionen

Tekniken jag kommer att beskriva heter "FDM" (Fused Deposition Modeling) eller också "FFF" (Fused Filament Fabrication). Som namnen kanske avslöjar så beskriver de en process där man fogar samman material i form utav så kallat filament. Jag brukar dra liknelsen med en limpistol där du trycker in limstavar i ena änden och pressar ut det igenom det varma munstycket för att sedan applicera detta på ytan som ska limmas. 

_Bild på extruder som kör ut plast här_

_Bild på limpistol?_

Föreställ dig att du med nogrann precision kan applicera limpistolens extruderade material i en kontrollerad rörelse i många fina lager, där har du en 3D-Skrivare i enkla drag.

Skrivare av denna typ kommer i många olika former, men dom flesta följer dessa grundläggande principer. Skrivarens munstycke rör sig över en yta där den disponerar ett givet material enligt instruktioner från en dator. För varje lager rör sig sedan munstycket uppåt för att sakta och säkert bygga upp objektet ifrån plattan. 

Detta tillvägagånssättet kallas för additiv tillverkning då modellen byggs upp ifrån ingenting istället för motpartens subtraktiva tillverkning där vi istället skär bort material för att få den slutgiltiga formen. Detta har många fördelar då det går åt mindre material för att skriva ut något i en 3D-skrivare än att fräsa bort materialet i en maskin ifrån ett större stycke material.

_bild på en pågående utskrift_

## Skrivarens delar

I denna sektionen kommer vi att gå igenom några utav skrivarens beståndsdelar för att få en större förståelse om hur allt hänger ihop.

#### __Hotend__

En hotend är det värme-element som smälter tillsatsmaterialet som ska appliceras på utskriften. Plasten matas in i form utav en tråd som går igenom ett värme-block där ett munstycke sitter monterat. Detta munstycke har i uppgift att stoppa tråden tills dess att den har värmts upp och fått rätt konsistens för att tryckas ut i en mindre storlek. Diametern som tråden kommer ut i beror helt på vilken typ utav munstycke man har utrustat skrivaren med. De vanligaste storlekarna sträcker sig ifrån 0.2mm - 0.8mm, men givetvis finns det undantag. Branchstandarden har länge varit 0.4mm. In kommer då plast som är 1.75mm och ut kommer en sträng som är 0.4mm som ett exempel.

![bild på extruder utan fläktar och tillbehör monterade](/assets/images/printing/hotend-assembly-1.jpg "hotend assembly")

Hotenden består i sin tur utav ett gäng komponenter. Om vi börjar nerifrån så är det följande:

- Munstycke (Noozle), stoppar filamentet/smältan och tvingar materialet att reduseras i diameter för att få hög precision på appliceringen på utskriften.

_Närbild av munstycket_

- Värmeblock, detta block har i uppgift att leverera värme till munstycket och smältzonen. Här sitter det en värmepatron och en termistor för att reglera temperaturen.

![Närbild utav värmeblocket/termistor/patron](/assets/images/printing/heater-block-2.jpg "heater block")

- Värmesköld/kylning, detta större parti har i uppgift att fort transportera bort värmen som söker sig uppåt från värmeblocket. Det är viktigt att inte få filamentet/plasten att värmas upp innan den når värmeblocket för att kunna hjälpa till att trycka på plasten och inte fastna.

- Alternativt en anslutning av slang för matning från extrudern.

Runt hotenden sitter det också vanligtvis två fläktar. En för att ständigt trycka luft igenom värmeskölden och en för att blåsa på den nyligen extruderade plasten som kommer ut genom munstycket.

### Extruder

En extruder är den mekanik som förser munstycket med filament. Dom två vanligaste varianterna är "Bowden" och "Direct-Drive" extruders. 

En Bowden extruder sitter inte direkt i anslutning till hotenden utan en bit ifrån och oftast fast monterad på icke rörliga komponenter. Filamentet matas då genom en slang hela vägen till hotenden. Fördelen med denna konstruktion är att dom rörliga delarna blir lättare och kan färdas med högre hastighet och acceleration. Nackdelen är att spänningen och friktionen i slangen leder till sämre kontroll över filamentets flöde.

![Bild på bowden extruder samt vägen till hotend](/assets/images/printing/ender3-extruder-1.jpg "extruder")

En Direct-Drive extruder som namnet avslöjar sitter direkt monterad ovanför hotenden. Detta resulterar till att man har mycket kort sträcka för filamentet att färdas och även i en rak riktning så att man har mycket god förmåga att kontrollera flödet. Nackdelen är då tyngden man tillför då en motor väger en del. I många fall så kan vikten mer än fördubblas, detta resulterar i sämre prestanda när hastighet och acceleration ökar. Dessa skrivare har en rejälare konstruktion för att kunna hantera den extra vikten.

### Utskriftsytan

Bädden som modellen kommer skrivas ut på är en mycket viktig del i skrivaren. Den är oftast uppvärmd och det yttersta skicktet kan variera i material beroende på vad man skriver ut. Anledningen till en varm byggyta är då plasten fäster bättre om den inte kyls ner under en viss temperatur. Ytan kan var av glas, fjäderstålplåt med slät eller texturerad PEI behandling, G10 fiber-skiva och många fler. Till dessa kan man dessutom använda diverse tillsatser för att få utskrifterna att fästa ännu bättre.

![Bild på all byggytor jag har, och även limm/sprayer](/assets/images/printing/printbeds-adhesion-2.jpg "extruder")

![Prusa Mini byggytor](/assets/images/printing/printbeds-mini-3.jpg "mini buildplates")

### Motorer/axlar

Det som ger alla axlarna liv är så kallade stegmotorer. Dessa motorer skiljer sig ifrån dom vi normalt ser i vår hemelektronik, dom flyttar sig i steg/hack för att sedan hålla en stadig position. Detta medför en hög precision vid förflyttning. Antalet motorer varierar mellan olika modeller av skrivare, men en Creality Ender3 har totalt 4 stycken, vardera axel X, Y och Z har en motor var och så sitter det även en för extrudern. Vissa skrivare har dubbla motorer för Z-axeln (motorn som driver höjden) för att ge en stadigare och starkare rörelse.

![kollage med alla motorer på en ender3](/assets/images/printing/motors.jpg "printer motors")

### Display/Användargränsnitt

En skärm finns på de flesta skrivare idag för att man ska kunna utföra alla funktioner som krävs för att starta en utskrift. Standarden för att navigera är ett hjul man snurrar och klickar med. Skärmarna kan skilja sig en del och sträcker sig ifrån simplare monochroma varianter som på äldre Creality skrivare och flerfärgade displayer som på en Prusa Mini+ där man till och med kan se en förhandsvisning av modellen man skriver ut. Går man upp några prisklasser så har dessa ibland touch-skärm.

![Bild på Ender3 display](/assets/images/printing/ender3-display-1.jpg "printer motors")

![Bild på Mini+ display](/assets/images/printing/mini-display-1.jpg "printer motors")

### Materialen

Med en 3D-Skrivare kan man skriva ut föremål med en stor mängd av material, för att bara nämna några så är dom populäraste PLA, PETG, FLEX, HIPS och ABS. Det är viktigt att tänka till när man ska välja material då olika filament har olika egenskaper. Är fokus en fin yta? Ska den tåla högre temperaturer? Kommer den utsättas för högre belastning?

Filament finns i olika diametrar 1,75mm och 3mm där den först nämnda är vanligast.

Det är en hel djungel full med filament idag så dom flesta materialen har en uppsjö med olika tillverkare och färger.

## Processen, steg för steg

Vill du veta hur hela processen går till så kan du läsa vidare här (lämk till nästa artikel)