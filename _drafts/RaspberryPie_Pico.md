---
layout: post
title:  "Raspberry Pi Pico"
categories: ['Raspberry Pi']
---

Not fair, but here is a comparison of the Pico and a Arduino Uno:

|                   | Raspberry Pie Pico  | Arduino Uno |
| ---------------------- |:-------------:|:-------------:| 
| Operating Voltage      | 3.3V          | 5V            | 
| Input Voltage          | 3.3V          | 5V            | 
| Digital I/O Pins       | 26            | 14 (of which 6 provide PWM output)              |
| PWM Digital I/O Pins   |16 × controllable PWM channels | 6 |
| Analog Input Pins      | 3x 12-bit ADC | 6 |
| DC Current per I/O Pin |               | 20 mA |
| Flash Memory           | 2MB | 32 KB (ATmega328P) of which 0.5 KB used by bootloader |
| SRAM                   |    264 kB      | 2 kB (ATmega328P) |
| EEPROM | | 1 KB (ATmega328P) |
| Clock Speed | 133 MHz | 16 MHz |
| Length |  | 68.6 |
| Width |  |53.4 mm |
| Weight |    |	25 g |


[AMPY Adafruit MicroPython Tool](https://github.com/scientifichackers/ampy)

## Getting started

Documentation for developing programs for the Pico with MicroPython can be found [here](https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-python-sdk.pdf)

Install [MicroPyCli](https://github.com/BradenM/micropy-cli). Prerequisites are Python 3.10 and pip.

`pip install --upgrade micropy-cli`

Run `micropy search stubs <term, example pico>` will give you hints on what stubs are available.

Then you can add them by using the following command 

```bash
micropy add stubs <name of stub from search>
```

Using VS Code and the [Pymakr Extension](https://marketplace.visualstudio.com/items?itemName=pycom.Pymakr) enables intellisense and linting, using stubs installed from previous step.


If you have trouble flashing, its probably a bad USB cable with missing data pins/wires. A so called charging cable.

## Utilities

For easier debugging and interctions to the Pico device, I suggest that you use a program called [rshell](https://github.com/dhylands/rshell). It can act as a terminal emulator to access the REPL instead of other serial communication software such as minicom, which I think is a little hard to use. The rshell is as it says a shell that can do much of the communication tasks when developing software for the device, such as sending python snippets and copying files to and from MicroPythons FileSystem. You can read more about it's capabilities on [github](https://github.com/dhylands/rshell).



### Usefull links that helped me gather information to write this post

- [IDE setup](https://lemariva.com/blog/2019/08/micropython-vsc-ide-intellisense)
- 