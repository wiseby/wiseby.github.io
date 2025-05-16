---
layout: post
title: "Self-Hosted Email Server"
categories: ["Linux"]
---

# Self-Hosted Email Server on Ubuntu + Loopia DNS Configuration

## Required Tools and Services

| Service      | Purpose                         |
|--------------|---------------------------------|
| Postfix      | SMTP server (sending/receiving) |
| Dovecot      | IMAP server (receiving/fetching)|
| OpenSSL      | TLS for secure communication    |
| SpamAssassin | Spam filtering (optional)       |
| ClamAV       | Antivirus (optional)            |
| OpenDKIM     | DKIM signing                    |
| Fail2ban     | Brute force protection          |
| Certbot      | Let's Encrypt SSL               |

---

## Server Installation (Ubuntu 22.04+)

### 1. Update & Install Base Packages
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install postfix dovecot-core dovecot-imapd mailutils \
     opendkim opendkim-tools spamassassin clamav certbot \
     python3-certbot-nginx ufw fail2ban
```

### 2. Configure Postfix
During install, choose:
- "Internet Site"
- System mail name: `yourdomain.com`

Basic config: `/etc/postfix/main.cf`
```bash
sudo nano /etc/postfix/main.cf
```
Set:
```
myhostname = mail.yourdomain.com
mydomain = yourdomain.com
myorigin = /etc/mailname
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
home_mailbox = Maildir/
smtpd_tls_cert_file=/etc/letsencrypt/live/mail.yourdomain.com/fullchain.pem
smtpd_tls_key_file=/etc/letsencrypt/live/mail.yourdomain.com/privkey.pem
smtpd_use_tls=yes
smtpd_tls_auth_only = yes
```

### 3. Configure Dovecot (IMAP)
Edit `/etc/dovecot/conf.d/10-mail.conf`
```conf
mail_location = maildir:~/Maildir
```

Enable plain login with SSL (10-auth.conf):
```conf
disable_plaintext_auth = yes
auth_mechanisms = plain login
```

SSL certs (10-ssl.conf):
```conf
ssl = required
ssl_cert = </etc/letsencrypt/live/mail.yourdomain.com/fullchain.pem
ssl_key = </etc/letsencrypt/live/mail.yourdomain.com/privkey.pem
```

### 4. Setup Maildir for existing users
```bash
sudo mkdir -p /home/username/Maildir
sudo chown -R username:username /home/username/Maildir
```

### 5. TLS Certificates via Let's Encrypt
If port 80 is in use, stop the web server temporarily:
```bash
sudo systemctl stop nginx  # or apache2, depending on your setup
sudo certbot certonly --standalone -d mail.yourdomain.com
sudo systemctl start nginx
```

Renewal test:
```bash
sudo certbot renew --dry-run
```

### 6. Open Required Ports (UFW)
```bash
sudo ufw allow 22
sudo ufw allow 25,465,587/tcp
sudo ufw allow 993/tcp
sudo ufw enable
```

---

## Configure DNS on Loopia.se

### 1. A Record
| Type | Host | Value              |
|------|------|--------------------|
| A    | mail | YOUR.SERVER.IP.HERE|

### 2. MX Record
| Type | Host        | Priority | Value               |
|------|-------------|----------|---------------------|
| MX   | yourdomain.com | 10       | mail.yourdomain.com |

### 3. SPF (TXT)
| Type | Host | Value                                    |
|------|------|------------------------------------------|
| TXT  | @    | "v=spf1 ip4:YOUR.SERVER.IP.HERE -all"    |

### 4. DKIM (after OpenDKIM setup)
| Type | Host                          | Value                                |
|------|-------------------------------|--------------------------------------|
| TXT  | `default._domainkey`          | `v=DKIM1; k=rsa; p=YOURPUBLICKEY`    |

### 5. DMARC
| Type | Host   | Value                                               |
|------|--------|-----------------------------------------------------|
| TXT  | _dmarc | "v=DMARC1; p=none; rua=mailto:you@yourdomain.com"  |

### 6. PTR Record (Reverse DNS)
- If you use Hetzner Cloud, set reverse DNS in the **Cloud Console > Floating IPs** or by opening a support request.
- Set your server's IP PTR record to `mail.yourdomain.com`.

---

## Mail Migration (optional)

To move mail from your old provider:
```bash
sudo apt install imapsync
imapsync \
  --host1 old.mailserver.com --user1 you@yourdomain.com --password1 'oldpass' \
  --host2 localhost         --user2 you@yourdomain.com --password2 'newpass'
```

**Or with Thunderbird**:
1. Add both accounts in Thunderbird (old and new).
2. Drag-and-drop emails between inboxes.
3. (Optional) Backup mailboxes locally using `ImportExportTools NG` add-on.

---

## Virtual Mailboxes with Custom Passwords

Instead of using system users, configure Dovecot to authenticate using a password file.

Edit `/etc/dovecot/conf.d/auth-passwdfile.conf.ext`:
```conf
passdb {
  driver = passwd-file
  args = scheme=CRYPT username_format=%u /etc/dovecot/users
}

userdb {
  driver = static
  args = uid=1000 gid=1000 home=/home/wiseby
}
```

Create `/etc/dovecot/users`:
```bash
lucas.wiseby@yourdomain.com:{CRYPT}$6$... (hashed password)
```
Generate a secure hash:
```bash
doveadm pw -s CRYPT
```

Set permissions:
```bash
sudo chown root:dovecot /etc/dovecot/users
sudo chmod 640 /etc/dovecot/users
```

Restart Dovecot:
```bash
sudo systemctl restart dovecot
```

Test login:
```bash
sudo doveadm auth test lucas.wiseby@yourdomain.com 'yourpassword'
```

---

## Final Notes

- Use [https://mail-tester.com](https://mail-tester.com) to test your config.
- Monitor logs: `/var/log/mail.log`, `/var/log/mail.err`
- Test from an email client like Thunderbird.

---

## Security Tips

- Enable Fail2ban to block brute-force attempts.
- Regularly update packages and rotate your TLS certs.
- Back up your Maildir and Postfix configs regularly.
