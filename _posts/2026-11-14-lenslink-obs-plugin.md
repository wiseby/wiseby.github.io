---
title: "LensLink, använd din Iphone som webbkamera"
excerpt: "Saknar du en webbkamera? Använd din Iphone ihop med OBS Studio."
date: 2026-11-14
categories:
  - verkstaden
  - artiklar
tags:
  - streaming
  - gaming
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

# Använd din iPhone som webbkamera i OBS med LensLink

LensLink gör det möjligt att använda en iPhone eller iPad som en högkvalitativ kamera direkt i OBS Studio. Anslutningen kan göras via USB eller Wi-Fi.

Det fungerar på både Windows och Linux och kräver ingen separat virtuell webbkamera, RTMP-server eller prenumeration.

## 1. Så fungerar LensLink

LensLink består av två delar:

1. **LensLink-plugin för OBS Studio** – installeras på datorn och lägger till nya videokällor i OBS.
2. **LensLink Camera** – appen som installeras på din iPhone.

När båda delarna är installerade kan OBS kommunicera direkt med telefonen.

Du får tillgång till två nya källor:

- **LensLink Camera:** använder iPhone-kameran som videokälla.
- **LensLink Screen:** speglar iPhone-skärmen och kan även överföra systemljud.

### Funktioner

- Upp till 4K-upplösning och 60 bilder per sekund.
- H.264- och HEVC-video.
- Anslutning via USB eller lokalt Wi-Fi.
- Möjlighet att använda telefonens mikrofon.
- Manuella inställningar för bland annat fokus, exponering och vitbalans.
- Flera telefoner kan anslutas samtidigt.
- Stöd för skärmspegling.

**Rekommendation:** Använd USB när du streamar från en fast plats. Det ger normalt lägre och jämnare fördröjning än Wi-Fi.

## 2. Systemkrav

| Komponent | Krav |
|---|---|
| OBS Studio | Version 32 eller senare |
| iPhone/iPad | iOS/iPadOS 15 eller senare |
| Windows | Windows 10 eller senare |
| Linux | OBS med EGL-stöd och kompatibel VAAPI-drivrutin för hårdvaruavkodning |
| USB på Windows | Apples enhetsdrivrutin via iTunes |
| USB på Linux | `usbmuxd` |

Wi-Fi kräver ingen extra USB-drivrutin, men telefon och dator måste vara anslutna till samma lokala nätverk.

## 3. Installera LensLink på iPhone

1. Öppna App Store på din iPhone.
2. Sök efter **LensLink Camera**.
3. Installera appen.
4. Starta appen och godkänn åtkomst till kameran.
5. Godkänn mikrofonåtkomst om du vill använda telefonens mikrofon.

[LensLink Camera – App Store](https://apps.apple.com/app/id6744560198)

Appen är gratis och uppdateras via App Store.

## 4. Installation på Windows

### Steg 1 – Kontrollera OBS-versionen

Starta OBS och välj:

`Help → About`

Kontrollera att du har version 32 eller senare.

### Steg 2 – Installera pluginen

1. Besök [LensLinks nedladdningssida](https://lenslink.cam/download/).
2. Ladda ner installationsfilen:

   `LensLink-installer-windows-x64.exe`

3. Kör installationsfilen.
4. Följ installationsanvisningarna.
5. Starta om OBS.

Installationsprogrammet placerar pluginen i:

`C:\ProgramData\obs-studio\plugins\lenslink\`

Du behöver normalt inte flytta några filer manuellt.

### Alternativ: Manuell installation

Om du föredrar att installera pluginen manuellt:

1. Ladda ner `lenslink-windows-x64.zip`.
2. Packa upp arkivet i:

   `C:\ProgramData\obs-studio\plugins\`

3. Kontrollera att mappstrukturen innehåller LensLinks pluginfiler.
4. Starta om OBS.

Undvik att blanda gamla och nya installationer. Om du tidigare har installerat en äldre version direkt i OBS-mappen behöver de gamla filerna tas bort enligt LensLinks installationsanvisningar.

### Steg 3 – Installera Apples USB-drivrutin

För att Windows ska kunna kommunicera med iPhone via USB krävs Apples enhetsdrivrutin.

Installera iTunes från Apple eller Microsoft Store om drivrutinen inte redan finns installerad.

Anslut sedan din iPhone och välj **Lita på den här datorn** när frågan visas.

## 5. Installation på Linux

Den här installationen gäller exempelvis Arch Linux, CachyOS och andra distributioner.

### Steg 1 – Installera USB-beroenden

Öppna terminalen och kör:

```bash
sudo pacman -S --needed usbmuxd libimobiledevice
```

Aktivera USB-tjänsten:

```bash
sudo systemctl enable --now usbmuxd
```

För andra Linuxdistributioner installerar du motsvarande paket via distributionens pakethanterare.

### Steg 2 – Kontrollera iPhone-anslutningen

Anslut iPhone med USB-kabel och lås upp telefonen.

Om du får frågan om att lita på datorn väljer du **Lita på**.

Kör sedan:

```bash
idevice_id -l
```

Om anslutningen fungerar visas telefonens enhetsidentifierare.

Om ingen enhet visas bör du kontrollera USB-kabeln, låsa upp telefonen och kontrollera att `usbmuxd` körs:

```bash
systemctl status usbmuxd
```

### Steg 3 – Ladda ner pluginen

Besök:

[LensLink – Downloads](https://lenslink.cam/download/)

Ladda ner:

`lenslink-linux-x86_64.tar.gz`

### Steg 4 – Installera pluginen

För en vanlig OBS-installation installerar du pluginen i din användarmapp.

Skapa pluginmappen om den saknas:

```bash
mkdir -p ~/.config/obs-studio/plugins/
```

Packa upp arkivet:

```bash
tar -xzf ~/Downloads/lenslink-linux-x86_64.tar.gz \
  -C ~/.config/obs-studio/plugins/
```

Kontrollera att filerna har packats upp:

```bash
ls ~/.config/obs-studio/plugins/
```

Starta om OBS efter installationen.

**Observera:** Om du använder Flatpak-versionen av OBS är sökvägen annorlunda:

```bash
~/.var/app/com.obsproject.Studio/config/obs-studio/plugins/
```

För hårdvaruavkodning på Linux använder LensLink VAAPI och OBS måste köra med EGL. Om videon inte visas eller GPU-avkodningen misslyckas behöver du kontrollera din grafikdrivrutin och OBS-loggen.

## 6. Anslut iPhone till OBS

När pluginen är installerad och appen finns på telefonen kan du ansluta.

### USB-anslutning

1. Anslut iPhone till datorn med en USB-datakabel.
2. Lås upp telefonen.
3. Starta LensLink Camera.
4. Välj vilken kamera du vill använda.
5. Välj önskat videoformat och upplösning.
6. Tryck på **Start Camera**.
7. Starta OBS.
8. Gå till panelen **Sources**.
9. Klicka på `+`.
10. Välj **LensLink Camera**.
11. Välj USB som anslutningsmetod.
12. Välj din iPhone om den visas i listan.

Videobilden bör nu visas direkt i OBS.

### Wi-Fi-anslutning

Om du inte vill använda USB:

1. Anslut telefonen och datorn till samma lokala nätverk.
2. Starta LensLink Camera.
3. Öppna anslutningsinformationen i appen.
4. Notera telefonens IP-adress.
5. Lägg till en LensLink Camera-källa i OBS.
6. Välj telefonen i listan eller skriv in IP-adressen manuellt.

Wi-Fi-nätverket måste tillåta kommunikation mellan enheterna. Gästnätverk och vissa företagsnätverk kan blockera detta.

## 7. Använd LensLink i OBS

När kameran är ansluten kan du arbeta med den precis som med andra videokällor.

### Ändra bildstorlek

- Markera LensLink Camera i källistan.
- Dra i de röda hörnen för att ändra storlek.
- Högerklicka på källan och välj Transform för fler alternativ.

### Använd iPhone som mikrofon

LensLink kan även överföra ljud från telefonens mikrofon.

Du kan konfigurera detta i LensLinks källinställningar i OBS. Kontrollera sedan ljudnivån i OBS ljudmixer.

Om du redan använder en separat mikrofon kan det vara bättre att behålla den som primär ljudkälla och använda iPhone enbart för video.

### Använd LensLink Screen

Vill du visa vad som händer på telefonens skärm kan du istället lägga till:

`Sources → + → LensLink Screen`

Detta är användbart för exempelvis:
- Mobilspel.
- Appdemonstrationer.
- Instruktionsfilmer.
- Presentationer av mobilappar.

## 8. Viktigt att känna till

- iPhone måste normalt ha LensLink öppet i förgrunden medan kameran används.
- Om du lämnar appen under en pågående streaming kan videobilden försvinna eftersom iOS begränsar bakgrundsåtkomst till kameran.
- Använd helst USB för längre sändningar.
- Använd ett mobilstativ för att få en stabil bild.
- Se till att telefonen får tillräcklig ström under längre sändningar.
- 4K och 60 fps kräver mer processorkraft och bandbredd än 1080p.

## 9. Felsökning

| Problem | Möjlig lösning |
|---|---|
| LensLink Camera saknas i OBS | Kontrollera OBS-versionen och starta om OBS |
| iPhone visas inte | Kontrollera USB-kabeln och att telefonen är upplåst |
| Windows hittar inte telefonen | Installera eller reparera Apples USB-drivrutin |
| Linux hittar inte telefonen | Kontrollera `usbmuxd` och kör `idevice_id -l` |
| Ingen bild visas | Kontrollera att Start Camera är aktiverat i appen |
| Wi-Fi fungerar inte | Kontrollera att enheterna finns på samma nätverk |
| Bilden hackar | Testa 1080p och 30 fps |
| Linux visar problem med GPU-avkodning | Kontrollera EGL- och VAAPI-stöd samt OBS-loggen |

## 10. Avinstallera LensLink

### Windows

Använd LensLinks avinstallationsfunktion i Windows eller ta bort:

`C:\ProgramData\obs-studio\plugins\lenslink\`

### Linux

Ta bort pluginmappen:

```bash
rm -rf ~/.config/obs-studio/plugins/lenslink
```

Om du vill behålla USB-stödet för andra program behöver du inte avinstallera `usbmuxd` eller `libimobiledevice`.

### iPhone

Avinstallera LensLink Camera precis som vilken annan iOS-app som helst.

---

## Länkar och resurser

- [LensLink – Officiell webbplats](https://lenslink.cam/)
- [LensLink – Nedladdningar](https://lenslink.cam/download/)
- [LensLink – Installationsguide](https://lenslink.cam/docs/install/)
- [LensLink – Anslutning till OBS](https://lenslink.cam/docs/connect/)
- [LensLink – GitHub](https://github.com/MyNamesEMurray/LensLink)
- [LensLink Camera – App Store](https://apps.apple.com/app/id6744560198)

**Sammanfattning:** Installera OBS-pluginen på datorn, installera LensLink Camera på iPhone och anslut via USB eller Wi-Fi. Lägg sedan till LensLink Camera som en videokälla i OBS. Därefter kan du använda telefonen precis som vilken annan kamera som helst i dina scener.