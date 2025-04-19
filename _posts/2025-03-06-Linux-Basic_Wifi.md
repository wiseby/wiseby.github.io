---
layout: post
title: "Setting up initial WIFI"
categories: ["Linux"]
---

# Connecting to WiFi on a Fresh Arch Linux Installation

If you have a fresh Arch Linux installation and need to connect to WiFi **without internet access** using simple Linux tools, follow this guide.

---

## **Step 1: Identify Your Wireless Interface**
First, find your network interface:

```bash
ip link
```

Look for your wireless interface (commonly named `wlan0` or `wlpXsY`).

Bring it up:

```bash
ip link set wlan0 up
```

---

## **Step 2: Scan for Available Networks**
Use `iw` to scan for WiFi networks:

```bash
iw dev wlan0 scan | grep SSID
```

Find your WiFi network's **SSID** from the output.

---

## **Step 3: Connect Using `wpa_supplicant`**
1. Create a configuration file with your WiFi credentials:
   
   ```bash
   wpa_passphrase "Your_SSID" "Your_WiFi_Password" | tee /etc/wpa_supplicant.conf
   ```
   
   This generates a WiFi configuration file with your **SSID** and **encrypted password**.

2. Start `wpa_supplicant`:
   
   ```bash
   wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf
   ```
   
   `-B` runs it in the background.

3. Verify the connection:
   
   ```bash
   iw dev wlan0 link
   ```
   
   If connected, it will show your **SSID**.

---

## **Step 4: Obtain an IP Address**
Now, request an IP address from the router.

1. Using `dhclient`:
   
   ```bash
   dhclient wlan0
   ```
   
2. If `dhclient` is not available, use `dhcpcd`:
   
   ```bash
   dhcpcd wlan0
   ```

---

## **Step 5: Test the Connection**
Check if you received an IP:

```bash
ip addr show wlan0
```

Try to ping Google's public DNS server:

```bash
ping -c 5 8.8.8.8
```

If you see replies, you're successfully connected!

---

## **Making the Connection Persistent**
To automatically connect on boot, enable `wpa_supplicant`:

```bash
systemctl enable wpa_supplicant
```

And restart your system:

```bash
reboot
```

Now, your WiFi should automatically connect when you boot Arch Linux!

---

## **Troubleshooting**
- If WiFi does not connect, check logs:
  ```bash
  journalctl -xe | grep wpa_supplicant
  ```
- If no networks appear in `iw dev wlan0 scan`, ensure your **wireless interface is up**:
  ```bash
  ip link set wlan0 up
  ```

For further debugging, check out the [Arch Linux WiFi Wiki](https://wiki.archlinux.org/title/Wireless_network_configuration).

