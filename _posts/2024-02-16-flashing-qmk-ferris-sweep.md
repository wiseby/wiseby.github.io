---
layout: post
title: "Flashing QMK Firmware for Ferris Sweep"
categories: ["Hardware"]
---

### This is how I flash my Ferris-Sweep.

First of all you need the qmk-cli. It can be installed with Python and it's package-manager pip.

`python -m pip install qmk`

Use it to setup the environment, this clones the latest qmk-firmware from github and sets everything up for you, all you need to do is to create your own mappings:

`qmk setup`

Create your own mapping:

`qmk new-keymap`

When your done with your keymap you can check if there are any errors by compiling it:

`qmk compile -kb ferris/sweep -km my-custom-keymap`

When everything compiles without errors and warnings it's time to flash it to the board. First of all you need to enter _bootsel mode_ for your RP2040 chip. This can be done by holding the reset-button pressed before you plug it in or by clicking it twice and hold it in. A new partition should be available on the system if you succeed. Now it's ready to be flashed.

`qmk flash -kb ferris/sweep -km my-custom-keymap -bl uf2-split-left`

When you setup the keyboard for the first time, you need to flash the right half once with the following bootloader option:

`qmk flash -kb ferris/sweep -km my-custom-keymap -bl uf2-split-right`

After this has been done you only need to flash the left one (witch you use to plug into your computer) whenever you upload a new keymap.

Useful resources:

- [Gettind Started with QMK](https://docs.qmk.fm/#/newbs_getting_started)
- [Firmware Configuration](https://docs.qmk.fm/#/feature_split_keyboard?id=firmware-configuration)
- [Basic Keycodes](https://docs.qmk.fm/#/keycodes_basic)
- [Mod Tapping](https://docs.qmk.fm/#/mod_tap)
