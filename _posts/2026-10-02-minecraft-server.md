---
title: "Gör en egen Minecraft server"
excerpt: "En enkel guide för dig som vill driva din egna Minecraft server hemma"
categories:
  - verkstaden
  - artiklar
tags:
  - server
  - gaming
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

I denna artikeln kommer vi gå igenom både hårdvara och mjukvara för att köra en egen Minecraft Server över ditt lokala nätverk (LAN).

## Operativsystem

Här kommer vi köra med välprövade Ubuntu Server 26.04 LTS. Denna Linux distro kommer funka perfekt för ändamålet och installera utan problem på den flesta hårdvaran där ute. 

Ladda ner den senaste version gratis [här](https://ubuntu.com/download/server)

Jag använder ett program som heter Rufus för att skriva ISO filen till ett usb-minne.

Man kan också använda kommandot 'dd':

`sudo dd if=/home/wiseby/Downloads/ubuntu-26.04.1-live-server-amd64.iso of=/dev/sda bs=4M status=progress`

Nästa steg blir att få igång SSH så att vi kan configurera servern utan att ha 
tillgång till den fysiska datorn. [Se denna artikeln för att komma igång med SSH]({% post_url 2026-10-02-initial-ssh-setup-on-server %})

---

### Håll Ubuntu uppdaterat

Manuellt:

```bash
sudo apt update
sudo apt upgrade
```

Installera automatiska säkerhetsuppdateringar:

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure unattended-upgrades
```

### Konfigurera routern

För fjärråtkomst via SSH behöver routern vidarebefordra SSH-porten till servern.

Exempel:

```text
Internet
   │
   │ TCP 22
   ↓
Router
   │
   │ TCP 22
   ↓
Ubuntu-server
```

Använd en DHCP-reservation eller annan fast LAN-adress för servern.

### Slutlig säkerhetsnivå

En bra grundkonfiguration är:

```text
✓ SSH-nyckel används
✓ SSH-lösenord är avstängt
✓ root kan inte logga in via SSH
✓ UFW är aktiverat
✓ Endast nödvändiga portar är öppna
✓ Ubuntu hålls uppdaterat
✓ Servern har en fast LAN-adress
✓ Routern vidarebefordrar endast nödvändiga tjänster
```

---

## Minecraft (Paper) Installation

För vår server så använder vi Paper som är en Minecraft Java Edition Server som tillför bättre prestanda och stabilitet.

Läs mer om projectet [Paper MC](https://docs.papermc.io/)

### 1. Uppdatera Ubuntu

```bash
sudo apt update
sudo apt upgrade
```

### 2. Installera Java

Paper 26.1+ kräver Java 25.

Installera Java 25:

```bash
sudo apt install openjdk-25-jdk
```

Kontrollera versionen:

```bash
java -version
```

Utdata ska visa Java 25.

### 3. Skapa en separat Minecraft-användare

```bash
sudo adduser minecraft
```

Det skapar:

```text
/home/minecraft
```

Minecraft-servern ska köras som användaren `minecraft`, inte som `root` eller ditt vanliga användarkonto.

### 4. Skapa serverkatalogen

Om hemkatalogen inte redan finns:

```bash
sudo mkdir -p /home/minecraft
sudo chown minecraft:minecraft /home/minecraft
```

Byt till Minecraft-användaren:

```bash
sudo -u minecraft -i
```

Gå sedan till serverkatalogen:

```bash
cd /home/minecraft
```

### 5. Ladda ner Paper

Ladda ner önskad Paper-version från PaperMC och placera JAR-filen i:

```text
/home/minecraft
```

Det är praktiskt att döpa den till:

```text
paper.jar
```

Katalogen kommer så småningom ungefär att se ut så här:

```text
/home/minecraft/
├── paper.jar
├── server.properties
├── eula.txt
├── world/
├── world_nether/
├── world_the_end/
└── plugins/
```

### 6. Starta Paper manuellt första gången

Från `/home/minecraft`:

```bash
java -Xms2G -Xmx4G -jar paper.jar --nogui
```

Anpassa minnesmängden efter serverns RAM.

Första starten kommer att stoppa och kräva att Minecraft EULA accepteras.

Redigera:

```bash
nano eula.txt
```

Ändra:

```text
eula=false
```

till:

```text
eula=true
```

Starta sedan servern igen.

### 7. Konfigurera servern

Redigera:

```bash
nano server.properties
```

Exempel:

```text
server-port=25565
motd=Vår Minecraft-server
```

Vi håller servern så nära vanilla som möjligt och lägger bara till Paper-plugins när de behövs.

### 8. Stoppa servern

Från Minecraft-konsolen:

```text
stop
```

Använd inte bara `kill` eller stäng av datorn medan servern körs, eftersom Minecraft behöver möjlighet att spara världen korrekt.

### 9. Sätt ägare och rättigheter

Har man kört servern med den nya minecraft användaren så ska alla rättigheter vara korrekta redan, hoppa då vidare till nästa kapitel.

Om serverfilerna tidigare ägdes av en annan användare:

```bash
sudo chown -R minecraft:minecraft /home/minecraft
```

Sätt normala rättigheter på kataloger:

```bash
sudo find /home/minecraft -type d -exec chmod 755 {} \;
```

Sätt normala rättigheter på filer:

```bash
sudo find /home/minecraft -type f -exec chmod 644 {} \;
```

Använd **inte**:

```bash
chmod -R 777
```

Om servern innehåller körbara shell-skript:

```bash
sudo find /home/minecraft -type f -name "*.sh" -exec chmod 755 {} \;
```

### 10. Skapa en systemd-tjänst

Skapa:

```bash
sudo nano /etc/systemd/system/minecraft.service
```

Använd:

```ini
[Unit]
Description=Minecraft Paper Server
After=network.target

[Service]
User=minecraft
WorkingDirectory=/home/minecraft
ExecStart=/usr/bin/java -Xms2G -Xmx4G -jar paper.jar --nogui
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Se till att filens namn är korrekt och motsvarar den du laddade ner. Oftast kommer den med ett namn som innehåller information om vilken version det var. Uppdatera då `ExecStart` så att rätt fil körs.

Ändra `-Xms` och `-Xmx` om det behövs för serverns RAM.

### 11. Ladda och starta tjänsten

```bash
sudo systemctl daemon-reload
```

Aktivera automatisk start:

```bash
sudo systemctl enable minecraft
```

Starta:

```bash
sudo systemctl start minecraft
```

Kontrollera:

```bash
sudo systemctl status minecraft
```

### 12. Visa Minecraft-loggen

Följ loggen:

```bash
sudo journalctl -u minecraft -f
```

Visa de senaste 50 raderna:

```bash
sudo journalctl -u minecraft -n 50 --no-pager
```

Om tjänsten inte startar är detta ett av de första kommandona att använda.

### 13. Vanliga systemd-kommandon

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

Status:

```bash
sudo systemctl status minecraft
```

Inaktivera automatisk start:

```bash
sudo systemctl disable minecraft
```

### 14. Installera plugins

Stoppa servern:

```bash
sudo systemctl stop minecraft
```

Placera plugin-JAR-filer i:

```text
/home/minecraft/plugins/
```

Det enklaste sättet att hämta ner plugins är att högerklicka på länken/knappen för att ladda ner pluginet och bara kopiera länken och sedan använda wget i _plugins_ mappen på servern:

```bash
# Laddar ner pluginet Multiverse Portal
wget https://hangarcdn.papermc.io/plugins/Multiverse/Multiverse-Portals/versions/5.3.0/PAPER/multiverse-portals-5.3.0.jar
```

Se till att de ägs av Minecraft-användaren:

```bash
sudo chown minecraft:minecraft /home/minecraft/plugins/*.jar
```

Starta servern igen:

```bash
sudo systemctl start minecraft
```

För vår server har vi bland annat använt:

* Multiverse-Core
* LuckPerms

Ge vanliga spelare så få administrativa rättigheter som möjligt. Undvik att ge dem OP om det inte behövs.

### 15. Brandvägg

Installera UFW:

```bash
sudo apt install ufw
```

Tillåt Minecraft:

```bash
sudo ufw allow 25565/tcp
```

Aktivera brandväggen:

```bash
sudo ufw enable
```

Kontrollera:

```bash
sudo ufw status verbose
```

Öppna bara portar som faktiskt behövs.

### 16. Router

Ge Ubuntu-servern en fast LAN-adress, helst genom en DHCP-reservation i routern.

Om Minecraft ska vara tillgängligt från Internet behöver routern vidarebefordra:

```text
Internet TCP/UDP 25565
        ↓
Ubuntu-server:25565
```


## Konfiguration

Jag använde en laptop som server och jag behövde då se till att den inte 
somnade så fort jag stängde locket.

Jag gjorde följande förändring i _/etc/systemd/logind.conf_:

```
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

Starta om logind:

`sudo systemctl restart systemd.logind`

