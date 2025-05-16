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

Start and enable cups service:

`sudo systemctl enable cups.service`
`sudo systemctl start cups.service`

Use the lpadmin tool to add your printer through airprint everywhere. Use your specific ip address for your printer.

`lpadmin -p AirPrint -E -v "ipp://192.168.0.21/ipp/print" -m everywhere`
