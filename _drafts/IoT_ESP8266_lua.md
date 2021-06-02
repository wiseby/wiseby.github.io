---
layout: post
title: "Lua Interpreter On ESP8266"
---

You don't have to be stuck with Arduino and it's IDE. Me for example am not a big fan of this workflow and have missing skills in producing c++ programs.
Lua takes a little bit of distance through abstraction and makes it easier to build what you want fast.
Lua is like Python, a Interpreted language and the syntax is similar. The most important thing is that the Lua interpreter can be flashed to a ESP8266, my favorite is the ESP-01.

### Prerequisites

- An image built for your needs, using (NodeMCU Firmware builder)[https://nodemcu-build.com/index.php]
- (esptool.py)[https://github.com/espressif/esptool] from espressif for flashing.
- (NodeMCU-uploader)[https://github.com/kmpm/nodemcu-uploader] to upload files/programs running NodeMCU firmware.

- (Reflash your ESP)[https://learn.adafruit.com/diy-esp8266-home-security-with-lua-and-mqtt/how-to-re-flash-your-esp8266]
- (NodeMCU Docs)[https://nodemcu.readthedocs.io/en/release/modules/file/]
