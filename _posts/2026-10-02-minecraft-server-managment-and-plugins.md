---
title: "Installera och hantera Multiverse-Core, LuckPerms och RCON"
excerpt: "Detta är en guide om hur du hanterar din server och plugins"
date: 2026-09-30
categories:
  - verkstaden
  - artiklar
tags:
  - server
  - gaming
  - minecraft
  - paper
  - multiverse
  - luckperms
  - rcon
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

# Installera och hantera Multiverse-Core, LuckPerms och RCON

Den här guiden beskriver hur jag satte upp en liten Paper-baserad Minecraft-server på Ubuntu Server med flera världar, behörigheter och fjärradministration.

Servern körs som en `systemd`-tjänst och administreras från en annan dator med RCON-klienten `mcrcon`.

Målet är en enkel server för en mindre grupp spelare med bland annat:

- en Survival-värld
- en gemensam Creative-värld
- möjlighet att skapa tillfälliga Event-världar
- LuckPerms för spelarbehörigheter
- Multiverse-Core för världshantering
- RCON för administration utan att behöva vara inne i spelet

> Kommandona nedan utgår från en Paper-server på Ubuntu Server. Byt sökvägar och tjänstenamn om din installation använder andra namn.

---

## Förutsättningar

Jag utgår från att Paper redan är installerat och körs som en systemd-tjänst, exempelvis:

```bash
sudo systemctl status minecraft
```

Serverns filer ligger exempelvis i:

```text
/home/minecraft/server/
```

Pluginen placeras då i:

```text
/home/minecraft/server/plugins/
```

---

# Multiverse-Core

## Varför Multiverse?

Paper använder normalt en huvudvärld, men Multiverse-Core gör det möjligt att ha flera världar laddade samtidigt.

I den här servern används följande struktur:

```text
world      -> Survival
creative   -> gemensam Creative-värld
event      -> tillfällig Event-värld
```

Det betyder att man inte behöver byta `level-name` i `server.properties` för att byta mellan världarna. Alla världarna kan finnas samtidigt och spelare kan teleporteras mellan dem.

## Installera Multiverse-Core

Ladda ner en Multiverse-Core-version som stöder den Minecraft/Paper-version servern kör.

Placera `.jar`-filen i:

```text
/home/minecraft/server/plugins/
```

Kontrollera:

```bash
ls -l /home/minecraft/server/plugins/
```

Starta sedan om servern:

```bash
sudo systemctl restart minecraft
```

Kontrollera tjänsten:

```bash
sudo systemctl status minecraft
```

Och från Minecraft-konsolen/RCON:

```text
plugins
```

Multiverse-Core ska visas bland de laddade pluginen.

Aktuell dokumentation finns hos [Multiverse](https://mvplugins.org/).

---

## Visa världarna

```text
mv list
```

Det visar de världar som Multiverse känner till.

---

## Skapa Creative-världen

En vanlig Overworld kan skapas med:

```text
mv create creative normal
```

Teleportera sedan dit:

```text
mv tp creative
```

Tillbaka till Survival:

```text
mv tp world
```

---

## Ställ in Creative-världen

Sätt Creative som spelläge för världen:

```text
mv modify set gamemode creative creative
```

Vi ville också förhindra att eld sprids i Creative-världen. I den aktuella Minecraft-versionen används inte längre den äldre `doFireTick`-gamerulen för detta ändamål.

Vi använde därför:

```text
mv gamerule set fire_spread_radius_around_player 0 creative
```

För att hindra exempelvis creepers och endermen från att påverka byggen:

```text
mv gamerule set mobGriefing false creative
```

`fire_damage` är separat från eldsspridning och kan därför lämnas aktiverad om man fortfarande vill att eld ska kunna skada spelare.

---

## Skapa en Event-värld

När en Event-värld behövs kan den skapas på samma sätt:

```text
mv create event normal
```

Teleportera dit:

```text
mv tp event
```

Det gör att Event-världen kan finnas parallellt med Survival och Creative.

---

## Teleportera en annan spelare

När kommandot körs från serverkonsolen eller RCON behöver spelarnamnet anges:

```text
mv tp PlayerName creative
```

Exempel:

```text
mv tp Alice creative
```

Detta är särskilt användbart när servern administreras på distans.

---

# LuckPerms

## Varför LuckPerms?

LuckPerms används för att bestämma vilka kommandon olika spelare får använda.

I stället för att göra alla spelare till OP kan man skapa grupper, till exempel:

```text
admin
player
```

Administratörer kan då ha full kontroll medan vanliga spelare bara får de funktioner som behövs.

Det är särskilt viktigt för Multiverse. En vanlig spelare bör exempelvis kunna teleportera mellan tillåtna världar utan att kunna skapa eller ta bort världar.

Officiell dokumentation finns på [LuckPerms](https://luckperms.net/) och [LuckPerms Wiki](https://luckperms.net/wiki/).

---

## Installera LuckPerms

Ladda ner rätt Bukkit/Paper-version av LuckPerms och placera `.jar`-filen i:

```text
/home/minecraft/server/plugins/
```

Kontrollera:

```bash
ls -l /home/minecraft/server/plugins/
```

Starta om servern:

```bash
sudo systemctl restart minecraft
```

Kontrollera att LuckPerms laddades:

```text
plugins
```

På den här servern visades pluginet som `LuckPerms`/`luck-terms` i plugin-listan under felsökningen. Det viktiga är att LuckPerms faktiskt är laddat som plugin.

---

## En viktig skillnad: OP och LuckPerms

OP och LuckPerms är inte samma sak.

OP ger mycket omfattande administratörsbehörigheter. LuckPerms används för mer detaljerad kontroll.

Tanken för den här servern är därför:

- administratören behåller OP/admin-behörigheter
- vanliga spelare läggs i `player`-gruppen
- permissions läggs på gruppen i stället för på varje spelare separat

Det gör det mycket enklare att ändra reglerna senare.

---

## Skapa spelargruppen

Skapa gruppen:

```text
lp creategroup player
```

Visa grupperna:

```text
lp listgroups
```

---

## Lägg till spelare i gruppen

För varje spelare används:

```text
lp user PlayerName parent add player
```

Exempel:

```text
lp user Alice parent add player
lp user Bob parent add player
lp user Charlie parent add player
```

På servern finns sex spelare som ska kunna läggas till på detta sätt.

Fördelen är att permissions sedan kan ändras för hela `player`-gruppen i stället för för sex separata konton.

---

## Visa gruppens permissions

För att se vilka permissions som finns på gruppen:

```text
lp group player permission info
```

Information om en specifik spelare:

```text
lp user PlayerName info
```

Kontrollera en specifik permission:

```text
lp check PlayerName PERMISSION_NODE
```

LuckPerms har även ett verbose-läge som kan användas när man behöver se vilken permission ett kommando faktiskt kontrollerar:

```text
lp verbose on
```

Stäng av igen efter felsökning:

```text
lp verbose off
```

---

## Multiverse-permissions

Vilka Multiverse-permissions som behövs beror på exakt vilken Multiverse-version som är installerad och vilka funktioner spelarna ska få använda.

Grundprincipen är att lägga permissionen på gruppen:

```text
lp group player permission set PERMISSION_NODE true
```

Använd Multiverses aktuella permissions-dokumentation för den exakta noden för den funktion som ska tillåtas.

Målet för den här servern är att vanliga spelare ska kunna använda de nödvändiga teleportfunktionerna men inte få administrativa rättigheter som att skapa eller ta bort världar.

---

# RCON och mcrcon

## Varför RCON?

Eftersom Paper-servern körs som en `systemd`-tjänst har man inte en vanlig interaktiv Minecraft-konsol i terminalen.

`systemctl` används för att hantera själva tjänsten:

```bash
sudo systemctl start minecraft
sudo systemctl stop minecraft
sudo systemctl restart minecraft
sudo systemctl status minecraft
```

RCON används i stället för Minecraft-kommandon:

```text
mv list
mv tp PlayerName creative
lp user PlayerName info
list
say Hej!
```

Det gör det möjligt att administrera servern utan att vara inne i Minecraft.

---

## Konfigurera RCON på Paper-servern

Öppna serverns `server.properties` och kontrollera att RCON är aktiverat:

```properties
enable-rcon=true
rcon.port=25575
rcon.password=ETT_LÅNGT_UNIKT_LÖSENORD
```

Port `25575` är ett vanligt RCON-portnummer.

Om RCON-klienten bara ska köras lokalt på servern behöver RCON inte exponeras mot nätverket.

Om RCON ska användas från en annan dator måste porten vara nåbar från den datorn. Öppna inte RCON mot Internet utan att först ha tänkt igenom brandvägg och åtkomst noggrant.

Starta om Paper efter ändringen:

```bash
sudo systemctl restart minecraft
```

---

# Installera mcrcon på administratörsdatorn

Projektet vi använde är [mcrcon](https://github.com/Tiiffi/mcrcon), en enkel RCON-klient för Minecraft.

På en Linux-dator kan man använda en färdig release från projektets GitHub-sida.

Exempel på installationsflöde:

```bash
cd /tmp
wget https://github.com/Tiiffi/mcrcon/releases/download/v0.7.2/mcrcon-0.7.2-linux-x86-64-static.zip
sudo apt install unzip
unzip mcrcon-0.7.2-linux-x86-64-static.zip
sudo install -m 755 mcrcon /usr/local/bin/mcrcon
```

Kontrollera installationen:

```bash
mcrcon -v
```

> Versionsnumret ovan är ett exempel från installationen. Kontrollera mcrcons aktuella releasesida innan du använder en specifik nedladdnings-URL.

---

## Anslut med mcrcon

Om du kör `mcrcon` direkt på Minecraft-servern:

```bash
mcrcon -H 127.0.0.1 -P 25575 -p 'DITT_RCON_LÖSENORD'
```

Från en annan dator använder du Minecraft-serverns IP-adress:

```bash
mcrcon -H SERVER_IP -P 25575 -p 'DITT_RCON_LÖSENORD'
```

Exempel:

```bash
mcrcon -H 192.168.1.50 -P 25575 -p 'DITT_RCON_LÖSENORD'
```

När du är inne i RCON kan du skriva Minecraft-kommandon direkt.

Skriv normalt **inte** `/` framför kommandona.

Använd alltså:

```text
list
```

inte:

```text
/list
```

---

## Testa RCON

Börja med ett vanligt Paper/Bukkit-kommando:

```text
list
```

Det bör visa hur många spelare som är anslutna.

Testa sedan:

```text
plugins
```

Det visar vilka plugin som är laddade.

Ett enkelt testmeddelande kan skickas med:

```text
say RCON fungerar!
```

Meddelandet ska synas i Minecraft och i serverloggen.

---

## Kör ett enda kommando

mcrcon kan också köra ett kommando utan att öppna en interaktiv session:

```bash
mcrcon -H 192.168.1.50 -P 25575 -p 'DITT_RCON_LÖSENORD' "list"
```

Exempel:

```bash
mcrcon -H 192.168.1.50 -P 25575 -p 'DITT_RCON_LÖSENORD' "say Servern startas om snart!"
```

Det är praktiskt för enkla skript och administrativa rutiner.

---

# Vanliga administrativa kommandon

## Server

Visa anslutna spelare:

```text
list
```

Visa aktiva plugin:

```text
plugins
```

Visa Paper/Minecraft-version:

```text
version
```

Skicka ett meddelande:

```text
say Servern startas om om fem minuter.
```

Stoppa servern:

```text
stop
```

Var försiktig med `stop` eftersom det faktiskt stänger Minecraft-servern.

---

## Multiverse

Visa världarna:

```text
mv list
```

Teleportera dig själv:

```text
mv tp creative
```

Teleportera en spelare från konsolen:

```text
mv tp PlayerName creative
```

Skapa en värld:

```text
mv create event normal
```

---

## LuckPerms

Visa grupper:

```text
lp listgroups
```

Skapa spelargruppen:

```text
lp creategroup player
```

Lägg till en spelare:

```text
lp user PlayerName parent add player
```

Visa en spelares information:

```text
lp user PlayerName info
```

Visa gruppens permissions:

```text
lp group player permission info
```

Kontrollera en permission:

```text
lp check PlayerName PERMISSION_NODE
```

---

# Om RCON-kommandon inte ger någon output

Under installationen/felsökningen uppstod ett problem där `lp`-kommandon inte gav någon synlig output via RCON.

När detta händer är det viktigt att först kontrollera om RCON över huvud taget kör kommandona. Börja med:

```text
list
```

och:

```text
say RCON_TEST
```

Om dessa fungerar men `lp` inte ger någon output är problemet sannolikt specifikt för LuckPerms-kommandot eller command-sendern.

Kontrollera även att LuckPerms verkligen är laddat:

```text
plugins
```

På Ubuntu-servern kan Paper-loggen följas med:

```bash
sudo journalctl -u minecraft -f
```

Det går också att kontrollera de senaste raderna:

```bash
sudo journalctl -u minecraft -n 50 --no-pager
```

Om ett test med:

```text
say RCON_TEST
```

inte syns i loggen bör RCON undersökas innan man ändrar LuckPerms-konfigurationen.

---

# Systemd och serverlogg

Paper-servern hanteras av systemd.

Starta:

```bash
sudo systemctl start minecraft
```

Stoppa:

```bash
sudo systemctl stop minecraft
```

Starta om:

```bash
sudo systemctl restart minecraft
```

Visa status:

```bash
sudo systemctl status minecraft
```

Följ loggen i realtid:

```bash
sudo journalctl -u minecraft -f
```

Det här är användbart om ett plugin inte laddas eller om servern får fel vid uppstart.

---

# Rekommenderad enkel struktur

Den färdiga servern kan hållas ganska enkel:

```text
Paper
├── world       -> Survival
├── creative    -> Gemensam Creative
└── event       -> Tillfälliga event
```

Behörigheter:

```text
LuckPerms
├── admin       -> serveradministratörer
└── player      -> vanliga spelare
```

Och administration:

```text
systemctl
└── start / stop / restart / status

mcrcon
└── Minecraft-kommandon
    ├── Multiverse
    ├── LuckPerms
    ├── spelare
    └── meddelanden
```

Det ger en enkel uppdelning mellan själva serverprocessen, världshanteringen, spelarbehörigheterna och fjärradministrationen.

---

# Nästa steg

När den grundläggande servern fungerar kan fler funktioner läggas till utan att ändra grundstrukturen.

Ett exempel är personliga byggplatser i Creative-världen. Eftersom flera barn kan använda samma Minecraft-konto går det inte att tekniskt identifiera vilket barn som spelar. En enkel lösning är därför att skapa förutbestämda, "hemliga" byggplatser och använda teleportkommandon som:

```text
/space alice
/space bob
/space charlie
```

Detta är en enkel teleportlösning och inte ett riktigt skyddssystem. Om man senare behöver verkligt byggskydd kan ett separat permissions- eller region/claim-system användas.
