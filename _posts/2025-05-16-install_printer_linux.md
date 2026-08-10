---
layout: post
title: "Installing a printer in linux"
categories: ["linux"]
---

### Install dependencies

Instructions can be found on [archlinux wiki (cups)](https://wiki.archlinux.org/title/CUPS/Printer-specific_problemshttps://wiki.archlinux.org/title/CUPS)

Drivers for specific printers can be found [here](https://wiki.archlinux.org/title/CUPS/Printer-specific_problems)

For my printer (Canon PIXMA TS3151) I needed the [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2) package.

`sudo pacman -S cups cnijfilter2`

If thats not available, install with yay:

`yay cnijfilter2`

Start and enable cups service:

`sudo systemctl enable cups.service`
`sudo systemctl start cups.service`

Use the lpadmin tool to add your printer through airprint everywhere. Use your specific ip address for your printer.

`lpadmin -p AirPrint -E -v "ipp://192.168.0.21/ipp/print" -m everywhere`

Or you can add a printer connected over usb:

```
sudo lpadmin -p CanonPrinter \
        -v 'cnijbe2://Canon/?port=usb&serial=426FDE' \
        -P /usr/share/cups/model/canone3100.ppd \
        -E
```

the -P argument is the ppd file that matches the model of your printer.

#### Scanner Support

My printer also has a scanner built in, to make use of it, follow below guide.

Install SANE (Scanner Access Now Easy) packages:

`sudo pacman -S sane sane-airscan`

KDE Plasma has a good GUI Application for scanning:

`sudo pacman -S skanpage`

To make sure the scanner is accessable, run the following command:

`scanimage -L`

It should tell you the model of the scanner.
