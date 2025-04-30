---
layout: post
title: "Setup Factorio Server"
categories: ["Linux"]
---

## Factorio Headless Server Setup on Linux (Systemd)

### 1. Create a User for the Server

```bash
sudo useradd -m -r -s /bin/bash factorio
```

This creates a non-login system user named `factorio`.

---

### 2. Set Up Directory and Download Server

```bash
sudo mkdir -p /opt/factorio
sudo chown factorio:factorio /opt/factorio
cd /opt/factorio
```

Download the latest headless server from Factorio’s website:

```bash
wget https://www.factorio.com/get-download/latest/headless/linux64 -O factorio_headless.tar.xz
```

Or upload form you computer to server:

```bash
scp factorio.x.y.tar.xy <user>@<server ip or hostname>:.
```

Extract it:

```bash
tar -xvf factorio_headless.tar.xz
rm factorio_headless.tar.xz
```

This extracts into a directory like `factorio`. You can rename it or keep it as is:
```bash
mv factorio/* . && rmdir factorio
```

---

### 3. Run the Server Once to Generate Files

Switch to the `factorio` user and run the server once to create default files:

```bash
sudo -u factorio /opt/factorio/bin/x64/factorio --create /opt/factorio/saves/base-game.zip
```

This creates a basic save file.

---

### 4. Configure the Server

Edit `/opt/factorio/data/server-settings.json` to adjust name, description, visibility, etc.

You can also copy the example:
```bash
cp /opt/factorio/data/server-settings.example.json /opt/factorio/data/server-settings.json
```

Edit it with:
```bash
sudo -u factorio nano /opt/factorio/data/server-settings.json
```

If you do not own the "Space Age" DLC or want's to create a vanilla factorio server you need to create a mod-list.json file with the following content to disable DLC specific mods:
```json
  "mods": 
  [
    
    {
      "name": "base",
      "enabled": true
    },
    
    {
      "name": "elevated-rails",
      "enabled": false
    },
    
    {
      "name": "quality",
      "enabled": false
    },
    
    {
      "name": "space-age",
      "enabled": false
    }
  ]
}

```

---

### 5. Create the Start Script

Create a simple script to launch the server:

```bash
sudo nano /opt/factorio/start-base
```

Paste this in:

```bash
#!/bin/bash
cd /opt/factorio
exec ./bin/x64/factorio \
  --start-server ./saves/base-game.zip \
  --server-settings ./data/server-settings.json
```

Then make it executable:

```bash
sudo chmod +x /opt/factorio/start-base
```

---

### 6. Create a systemd Service

Create the service file:

```bash
sudo nano /etc/systemd/system/factorio.service
```

Paste the following:

```ini
[Unit]
Description=Factorio Headless Server
After=network.target

[Service]
User=factorio
Group=factorio
WorkingDirectory=/opt/factorio
ExecStart=/opt/factorio/start-base
Restart=on-failure
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

---

### 7. Enable and Start the Service

Reload systemd and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable factorio
sudo systemctl start factorio
```

---

### 8. Check Logs and Status

To check the status:

```bash
sudo systemctl status factorio
```

To follow the server logs:

```bash
journalctl -u factorio -f -o cat
```

---

### 9. Optional Cleanup

Delete the downloaded archive (if you haven’t already):
```bash
rm /opt/factorio_headless.tar.xz
```
