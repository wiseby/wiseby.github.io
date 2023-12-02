---
layout: post
title: "Raspberry Pie Proxy-server"
categories: ["Raspberry Pie", "Server"]
---

Time to build that proxy server, a gateway to all my self-hosted services!

Starting up from scratch with a Raspberry Pi OS Lite with the Rpi-Imager. Installed on a RaspberryPi 4 4GB.

- Install Nginx.
- Install UFW.
  - Allow 'Nginx full'
  - Allow 'SSH'
  - Enable
- Create SSL certificate
  - Install [snapd](https://snapcraft.io/docs/installing-snap-on-raspbian)
  - Install [certbot](https://certbot.eff.org/instructions?ws=nginx&os=debianbuster)
  - Create the certificate.
