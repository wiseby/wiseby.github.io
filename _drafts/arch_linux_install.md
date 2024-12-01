---
layout: post
title: "My Arch Linux Installation"
categories: 'Arch Linux'
---

- Desktop Environment: [Budgie](https://wiki.archlinux.org/title/Budgie)
  Finally ended up with the full KDE Plasma desktop
- Desktop Manager: [Gnome Display Manager (GDM)](https://wiki.archlinux.org/title/GDM) 
  Finally used [SDDM](https://wiki.archlinux.org/title/SDDM) (Simple Desktop Display Manager)
- Install bootloader [GRUB](https://wiki.archlinux.org/title/GRUB)
- Install Drivers for Radeon GPU [here](https://wiki.archlinux.org/title/AMDGPU)
- File Manager: [Dolphin](https://wiki.archlinux.org/title/Dolphin)

#### Additional Software:

- Email Client: Thunderbird
- Steam
- [ProtonUpQt](https://github.com/DavidoTek/ProtonUp-Qt)
- Spotify
- Focusrite Scarlett drivers (Work right out the box)

### Bumps on the road

- No USB boot, needed to go with the NetBoot approach. Work flawlessly

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

- Install GDM later switched to LightDM when I had issues with the Desktop Envswitcher not showing up.

- Install Konsole terminal emulator

- Install Bluetooth packages Blue

### Nvidia drivers

I tried to follow the arch-wiki page but I couldn't get it to work. After some searching I figured that I had issues with loading the modules to the kernel.

- Installed a custom kerner (linux-zen, which should be the one with optimized graphics available [The Zen Kernel](https://github.com/zen-kernel/zen-kernel/wiki/FAQ))

- Then I could install and follow the guide from the [wiki](https://wiki.archlinux.org/title/NVIDIA) to install the nvidia-dkms package.

After installation of the drivers I rebooted my PC and thought that everything was all good. I tried a couple of games, viewed the nvidia-settings and it ran really good with the new drivers. Later I noticed some issues with KDE itself. Some icons where not showing, windows where not rendering, fonts where pixelated, etc. All issures related to the KDE environment. I started digging and found some threads that matched the issues on Reddit and arch-forums.

I found this [gist](https://gist.github.com/lbrame/1678c00213c2bd069c0a59f8733e0ee6) and the creator had done a similar install of arch as me. Some packages wasa outdated and merged into something else, and not all sections didn't apply to me.

From the time of writing it fixed all my issues.

### KDE Plasma

I had trouble with some packages when using Budgie and I was in need of a more full fledged desktop environment. I also use my steam deck many times and it runs KDE Plasma as well, so the choice was simple. Installed it with little hazzle and I was very happy with the result. 

Some packages didn't come along with KDE package and had to be installed seperatly:

- Dolphin File Manager
- Ark Archive Ectractor/Zip tool
- Network Manager

Many of the programs that you want for a day-to-day basis has a package tailored for the KDE Desktop Environment and works seamlessly. Check out this [Application List](https://apps.kde.org/)

#### Install snapd (trying to use Fusion360)

- Install and configure [AppArmor](https://wiki.archlinux.org/title/AppArmor#Installation)
- Add the kernel parameters in the _/etc/default/grub_ file and run _sudo grub-mkconfig -o /boot/grub/grub.cfg_ command to enable it on reboot.
- Enable the services
  - sudo systemctl enable apparmor.service
  - sudo systemctl enable snapd.apparmor.service
  - sudo systemctl enable --now snapd.socket
  - verify basic confinement by installing and running the _hello-world_ snap with _hello-world.evil_

I also installed the snap-store with sudo 

#### Install Fusion360

installed it using the following script on github (here)[]

### Things I should change in the future

For now everything is working relly well and Im happy with my new system. I would want to change a couple of things to make it perfect.

- I dont like the look of the Display-Manager which is LightDM for the moment. Know I'm using SDDM and it's beautifull :D
- How to handle networks, started with commandline tools like _netctl_ but installed _NetworkManager_ to work better with KDE widgets and settings, I need to clean that up a bit.
- KDE-Plasma Wayland breaks from time to time when I upgrade the system so I have to fall back on X11. Issues can be random reboots, display stuttering among others. Sometimes it just works and I keep trying to use Wayland.

## Troubleshooting Section:

Here is a list of issues I stumbled apon when using archlinux. A reminder to myself and others, maybe you could find the answer for something thats troubling you as well.

### Random reboots

One day when I was doing some research on the web, my system reboots after about 20 minutes of use. There was no high load for the system. The only application I started was the Steam Client, Discord and Firefow Web Browser.
I tried to identify the issues in every log I could find without any clarity. Then I checked what type of session I was using for the Desktop Environment and it was Wayland. I changed it to X11 and know, no more reboots. Maybe I'll switch back to wayland when there is a new update awailable for either KDE-Plasa or maybe the kernel itself. I could perhaps switch to the more stable linux-kernel to see if that is the issue, but for now I'm using the X11 version.

