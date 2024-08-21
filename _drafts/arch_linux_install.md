---
layout: post
title: "My Arch Linux Installation"
categories: 'Arch Linux'
---

- Desktop Environment: [Budgie](https://wiki.archlinux.org/title/Budgie)
- Desktop Manager: [Gnome Display Manager (GDM)](https://wiki.archlinux.org/title/GDM) 
- Install bootloader [GRUB](https://wiki.archlinux.org/title/GRUB)
- Install Drivers for Radeon GPU [here](https://wiki.archlinux.org/title/AMDGPU)
- File Manager: [Dolphin](https://wiki.archlinux.org/title/Dolphin)

#### Additional Software:

- Email Client: [Evolution](https://wiki.archlinux.org/title/GNOME/Evolution)
- Steam
- [ProtonGt](https://github.com/DavidoTek/ProtonUp-Qt)
- Spotify
- Focusrite Scarlett drivers

### Bumps on the road

- No USB boot, need to go with the NetBoot approach. Work flawlessly

- Configure network 
  ´´´
    ip link set eno1 up
    ip address add 192.168.0.1/24 broadcast + dev eno1
    ip route add default via 192.168.0.1 dev eno1
  ´´´

  Added ´nameserver 8.8.8.8´ to _/etc/resolve.conf_

  Add a rule for hot-plugging interfaces to enable DHCP auto configuration. Create file __/etc/systemd/network/20-wired.network__ with content: 
  ```
  [Match]
  Name=en* // any pattern here. This pattern works with my interface (enp2s0)

  [Network]
  DHCP=yes
  ```
  
  Enable the systemd-networkd __sudo systemctl enable systemd-networkd__
  Start the systemd-networkd __sudo systemctl start systemd-networkd__

- Installed _netctl_ and optional dependencies _dhclient dhcpd dialog wpa_supplicant_

- Sudo setup. Added user lucas to wheel group and uncommented the line `%wheel ...` via visudo command.

- Installed Xorg server with the following package for my AMD CPU _xf86-video-amdgpu_

- Install GDM, later changed to LightDM

- Install Konsole terminal emulator

- Install Bluetooth packages Blue