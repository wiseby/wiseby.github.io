---
title: "Konfigurera SSH på ny server"
excerpt: "Du har fått fart på din server, nu behöver du säker tillgång över SSH, let's go!"
categories:
  - verkstaden
  - artiklar
tags:
  - server
  - ssh
locale: sv-SE
toc: true
toc_label: "Innehåll"
toc_icon: "list"
toc_sticky: true
---

Du har precis installerat och kopplat in din nya server på nätverket. Under installationen hade du kanske en skärm och tangentbord, men nu ska den sitta "headless" på nätverket. Nu kommer SSH in i bilden som gör det möjligt att koppla upp sig direkt mot servers terminal.

SSH står för "Secure Shell". Detta är ett kommunicationsprotokoll som idag är en del av i stort sett all kommunication över internet idag. På servern så är en så kallad SSH agent installerad som lyssnar på port 22. Vi kan då använda en SSH klient från våran dator för att koppla samman dessa för att utföra alla möjliga uppgifter på server.

Den simplaste uppkopplingen sker med hjälp av användarnamn och lösenord, detta är vad vi initiellt kommer att använda men byta ut mot en säkrare metod med så kallade nycklar.

Såhär startar du en tunnel men användarnamn och lösenord:

`ssh wiseby@192.168.1.123`

Du kommer att få frågan om att ange ditt lösenord.

### Ubuntu-server — Säker konfigurering av SSH

Målet är att kunna administrera servern via SSH från Internet utan att använda lösenordsinloggning.

**Viktigt:** Stäng inte av lösenordsinloggningen förrän SSH-inloggning med nyckel fungerar. Behåll din nuvarande SSH-session öppen medan du testar.

#### 1. Installera OpenSSH Server

På Ubuntu-servern:

```bash
sudo apt update
sudo apt install openssh-server
```

Kontrollera att tjänsten kör:

```bash
sudo systemctl status ssh
```

#### 2. Skapa en SSH-nyckel på klienten

På datorn som du använder för att administrera servern:

```bash
ssh-keygen -t ed25519
```

Acceptera standardplatsen:

```text
~/.ssh/id_ed25519
```

Använd gärna ett lösenord/passphrase för själva SSH-nyckeln.

Kontrollera:

```bash
ls -l ~/.ssh/id_ed25519*
```

Du bör ha:

```text
id_ed25519
id_ed25519.pub
```

`id_ed25519` är den privata nyckeln och ska aldrig kopieras till servern eller delas med någon.

#### 3. Kopiera den publika nyckeln till servern

Från klienten:

```bash
ssh-copy-id användarnamn@server-ip
```

Ange det nuvarande kontolösenordet när du blir tillfrågad.

Nyckeln läggs då till i:

```text
~/.ssh/authorized_keys
```

#### 4. Testa SSH med nyckeln

Öppna en **ny terminal** på klienten.

Stäng inte den befintliga SSH-sessionen.

Anslut:

```bash
ssh användarnamn@server-ip
```

Du ska nu kunna logga in med SSH-nyckeln.

Du kan uttryckligen testa public-key-autentisering:

```bash
ssh -o PreferredAuthentications=publickey användarnamn@server-ip
```

Gå inte vidare förrän detta fungerar.

#### 5. Kontrollera SSH-konfigurationen

På servern:

```bash
sudo sshd -t
```

Ingen output betyder att konfigurationen är syntaktiskt korrekt.

Kontrollera de befintliga inställningarna:

```bash
sudo grep -R "PasswordAuthentication\|KbdInteractiveAuthentication\|PubkeyAuthentication\|PermitRootLogin" /etc/ssh/sshd_config /etc/ssh/sshd_config.d/
```

Ubuntu kan ha ytterligare SSH-konfiguration i:

```text
/etc/ssh/sshd_config.d/
```

#### 6. Stäng av lösenordsinloggning

Skapa en separat konfigurationsfil:

```bash
sudo nano /etc/ssh/sshd_config.d/99-hardening.conf
```

Lägg in:

```text
PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
PermitRootLogin no
```

Det ger:

```text
SSH-nyckel       → tillåten
SSH-lösenord     → avstängt
root-inloggning  → avstängd
```

#### 7. Kontrollera konfigurationen

Innan SSH startas om:

```bash
sudo sshd -t
```

Om du får ett felmeddelande ska du **inte** starta om SSH förrän felet är åtgärdat.

#### 8. Starta om SSH

```bash
sudo systemctl restart ssh
```

Behåll fortfarande den gamla SSH-sessionen öppen.

Från den andra terminalen:

```bash
ssh användarnamn@server-ip
```

Kontrollera att du fortfarande kan logga in.

Först när detta fungerar kan du stänga den gamla sessionen.

#### 9. Konfigurera brandväggen

Installera UFW:

```bash
sudo apt install ufw
```

Tillåt SSH:

```bash
sudo ufw allow 22/tcp
```

Aktivera:

```bash
sudo ufw enable
```

Kontrollera:

```bash
sudo ufw status verbose
```

#### 10. Valfritt: byt extern SSH-port

Det är möjligt att använda exempelvis port `2222` istället för `22`.

Det är dock **inte en ersättning för SSH-nycklar eller brandvägg**.

Ändra exempelvis:

```text
Port 2222
```

Tillåt den nya porten i UFW:

```bash
sudo ufw allow 2222/tcp
```

Testa från en annan terminal:

```bash
ssh -p 2222 användarnamn@server-ip
```

Ta först därefter bort den gamla regeln:

```bash
sudo ufw delete allow 22/tcp
```

Om du gör detta måste även routerns port forwarding ändras.

#### 11. Kontrollera vilka tjänster som lyssnar

```bash
sudo ss -tulpn
```

Var särskilt uppmärksam på tjänster som lyssnar på:

```text
0.0.0.0
[::]
```

Du bör kunna identifiera varje tjänst som är nätverksåtkomlig.

#### 12. Konfigurera routern

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

#### 13. Kontrollera CGNAT

Eftersom servern använder en 5G-anslutning är detta särskilt viktigt.

Om operatören placerar anslutningen bakom CGNAT fungerar normalt inte vanlig port forwarding för inkommande SSH.

Alternativ kan då vara:

* Tailscale
* WireGuard via en server med publik IP
* VPN
* Offentlig IPv4-adress från operatören

#### 14. Slutlig säkerhetsnivå

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
✓ CGNAT är kontrollerat
```



