---
title: "Windows Explorer startar inte"
excerpt: ""
categories:
  - verkstaden
  - artiklar
tags:
  - windows
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

# Windows 11 – svart skrivbord efter inloggning

## Symptom

Efter uppstart av Windows 10:

* Windows startade normalt och inloggningsskärmen fungerade.
* Efter inloggning var skrivbordet helt svart.
* Muspekaren syntes och gick att flytta.
* Aktivitetsfältet och övrig navigering saknades.
* Windows-tangenten fungerade inte.
* **Aktivitetshanteraren** gick fortfarande att öppna med `Ctrl + Shift + Esc`.
* Datorn verkade i övrigt fungera normalt.
* Datorn körde **Windows 10 22H2** och verkade inte ha använts på länge.

## Felsökning

Eftersom Aktivitetshanteraren fortfarande fungerade gick det att starta program manuellt via **Kör ny aktivitet**.

Det första som testades var att starta Windows Explorer:

```text
explorer.exe
```

Eftersom problemet kvarstod kördes Windows systemfilsgranskare från en administrativ kommandotolk:

```cmd
sfc /scannow
```

## Lösning

Under tiden som `sfc /scannow` kördes började skrivbordet och Windows navigering plötsligt fungera igen.

Det tyder på att problemet kan ha varit relaterat till skadade eller inkonsekventa systemfiler som SFC kunde reparera.

Skanningen fick köras färdigt.

## Bra att känna till

Om Windows Explorer inte fungerar men Aktivitetshanteraren fortfarande går att öppna kan man använda **Kör ny aktivitet** för att starta:

```text
explorer.exe
```

eller öppna en administrativ kommandotolk och köra:

```cmd
sfc /scannow
```

Windows Update kan också öppnas direkt med:

```text
ms-settings:windowsupdate
```

## Slutsats

Datorn kunde starta Windows och användaren kunde logga in, men Windows-skalet fungerade inte korrekt. Eftersom Aktivitetshanteraren fortfarande var tillgänglig gick det att felsöka problemet utan att behöva starta om till återställningsläge eller installera om Windows.

I det här fallet började skrivbordet fungera igen medan `sfc /scannow` kördes, vilket pekar på att problemet sannolikt var relaterat till Windows systemfiler.

### Kommando som löste problemet

```cmd
sfc /scannow
```
