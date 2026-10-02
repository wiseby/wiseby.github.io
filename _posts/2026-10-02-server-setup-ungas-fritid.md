---
title: "Uppsättning av Ungas Fritids Minecraft Server"
excerpt: "För att kunna återskapa samma miljö som vi har på Ungas Fritids server"
date: 2026-09-02
categories:
  - verkstaden
  - artiklar
tags:
  - server
  - gaming
  - minecraft
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---


# Minecraft – världar, gamerules och portaler

Den här guiden beskriver vår grundläggande serverstruktur med **Paper**, **Multiverse-Core**, **Multiverse-Portals** och **LuckPerms**.

## 1. Världar

Vi använder fyra världar:

| Värld      | Syfte                           | Spelläge    |
| ---------- | ------------------------------- | ----------- |
| `hub`      | Central lobby och världsväljare | Adventure   |
| `survival` | Vanligt Minecraft               | Survival    |
| `creative` | Fritt byggande                  | Creative    |
| `event`    | Tillfälliga gruppevent          | Efter behov |

Skapa världarna med Multiverse-Core:

```text
/mv create hub normal
/mv create survival normal
/mv create creative normal
/mv create event normal
```

## 2. Spelläge per värld

Ställ in spelläget:

```text
/mv modify set gamemode adventure hub
/mv modify set gamemode survival survival
/mv modify set gamemode creative creative
```

`event` lämnas efter behov.

Tanken är att spelarna **inte själva ska behöva byta gamemode**. Världen bestämmer spelläget.

---

## 3. Creative-världen

Vi vill att spelarna ska kunna bygga fritt utan att mobbar förstör deras byggen.

```text
/mv gamerule set mob_griefing false creative
/mv gamerule set keep_inventory true creative
```

Kontrollera tillgängliga gamerules på serverversionen med:

```text
/mv gamerule list creative
```

Undvik att kopiera gamla gamerule-namn från äldre Minecraft-guider eftersom namnen har ändrats i nyare versioner.

---

## 4. Hub

Hubben fungerar som en skyddad central plats.

Spelare ska kunna:

* gå runt
* använda portaler
* välja värld
* inte kunna bygga eller förstöra

Därför används:

```text
/mv modify set gamemode adventure hub
```

Bygg exempelvis ett litet torg med tre portaler:

```text
              [ CREATIVE ]

        ┌─────────────────────┐
        │                     │
        │        HUB          │
        │                     │
        │ [SURVIVAL] [EVENT]  │
        │                     │
        └─────────────────────┘
```

---

## 5. Portaler

Portalerna skapas med **Multiverse-Portals**.

Hämta portalverktyget:

```text
/mvp wand
```

Markera portalens område:

1. Vänsterklicka första hörnet.
2. Högerklicka motsatt hörn.

Skapa sedan portalen.

### Survival

```text
/mvp create survivalportal w:survival
```

### Creative

```text
/mvp create creativeportal w:creative
```

### Event

```text
/mvp create eventportal w:event
```

Spelaren går sedan helt enkelt genom portalen och hamnar i respektive värld.

Portalen behöver inte vara en vanlig Nether-portal. Bygg själva portalen precis som du vill, exempelvis med sten, quartz, glas eller andra block.

---

## 6. Tillbaka till hubben

Spelarna bör ha ett enkelt sätt att komma tillbaka till hubben:

```text
/hub
```

Det kan senare kopplas till ett lämpligt kommando/plugin så att spelarna slipper använda Multiverse-kommandon.

Administratören kan alltid använda:

```text
/mvtp hub
```

för att teleportera sig till hubben.

---

## 7. LuckPerms

Vanliga spelare ska kunna använda portalerna men **inte administrera Multiverse**.

Portalbehörigheterna är exempelvis:

```text
multiverse.portal.access.survivalportal
multiverse.portal.access.creativeportal
multiverse.portal.access.eventportal
```

Ge dessa rättigheter till spelargruppen via LuckPerms.

Administratören behåller Multiverse- och serveradministrationsrättigheter.

---

## 8. Rekommenderad struktur

Den färdiga servern fungerar då ungefär så här:

```text
                         SERVER
                            │
                           HUB
                       Adventure
                            │
              ┌─────────────┼─────────────┐
              │             │             │
          Survival       Creative        Event
          Survival       Creative       valfritt
```

Spelarnas normala arbetsflöde:

```text
Anslut
  ↓
Hub
  ↓
Välj portal
  ↓
Spela
  ↓
/hub
  ↓
Hub igen
```

Det gör servern enkel för spelarna samtidigt som administrationen fortfarande sker via Multiverse och LuckPerms.

---

## 9. Nätverksport

Minecraft-serverns standardport är:

```text
25565/TCP
```

Om servern endast används på det lokala nätverket behöver ingen port öppnas mot Internet.

Klienterna ansluter då exempelvis med:

```text
192.168.x.x:25565
```

Om serverns port ändras måste `server.properties` uppdateras:

```properties
server-port=25565
```

---

## 10. Hub som startpunkt

Vi använder `hub` som serverns centrala lobby, men **inte** som `level-name` i `server.properties`. Multiverse-Core hanterar istället vart spelare skickas när de ansluter.

### Skicka spelare till hubben vid anslutning

Med Multiverse-Core 5.8.1:

```text
/mv config enable-join-destination true
/mv config join-destination hub
```

Det gör att spelaren skickas till `hub` varje gång de ansluter till servern.

Första-spawn kan också styras separat:

```text
/mv config first-spawn-override true
/mv config first-spawn-location hub
```

### Sätt hubbens spawn

Gå till den plats där spelarna ska komma in i hubben och kör:

```text
/mv setspawn
```

Hubben bör vara i **Adventure**:

```text
/mv modify set gamemode adventure hub
```

---

## 11. `/hub`-kommando

Vi använder `commands.yml` för att skapa ett enkelt alias.

Öppna serverns:

```text
commands.yml
```

Lägg till:

```yaml
aliases:
  hub:
    - "mvtp hub"
```

Starta sedan om servern.

Spelare kan nu använda:

```text
/hub
```

för att komma tillbaka till hubben.

Det innebär att spelarna inte behöver känna till Multiverse-kommandona.

---

## 12. LuckPerms för `/hub`

Om vanliga spelare inte kan använda `/hub`, ge spelargruppen rättighet att teleportera:

```text
/lp group default permission set multiverse.teleport.self.w true
```

Om servern använder destinationsspecifika teleportbehörigheter:

```text
/lp group default permission set multiverse.teleport.self.w.hub true
```

Testa gärna med en spelare som **inte är OP**.

---

## Färdig struktur

Servern fungerar nu enligt följande:

```text
                       ANSLUT
                          │
                          ▼
                    ┌───────────┐
                    │    HUB    │
                    │ Adventure │
                    └─────┬─────┘
                          │
              ┌───────────┼───────────┐
              ▼           ▼           ▼
          Survival     Creative      Event
          Survival     Creative     valfritt
              │           │           │
              └───────────┼───────────┘
                          │
                       /hub
```
