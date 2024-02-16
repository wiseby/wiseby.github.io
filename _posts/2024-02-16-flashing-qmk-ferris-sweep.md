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

### My first Keymapping

This is the first mapping where I did a port of my [Planck EZ Glow layout](https://configure.zsa.io/planck-ez/layouts/PqRlE/latest/2). I removed all RGB code because my Ferris Sweep lacks that feature. I also ad some issues with my macros and Tap-Dancing features, I have to implement these later when I got better knowledge of the QMK Firmware. Down below you can find my mappings and configuration (still in progress!):

#### keymap.c

```c
#include QMK_KEYBOARD_H

#include "eeprom.h"

#include "keymap_swedish.h"

#define KC_MAC_UNDO LGUI(KC_Z)
#define KC_MAC_CUT LGUI(KC_X)
#define KC_MAC_COPY LGUI(KC_C)
#define KC_MAC_PASTE LGUI(KC_V)
#define KC_PC_UNDO LCTL(KC_Z)
#define KC_PC_CUT LCTL(KC_X)
#define KC_PC_COPY LCTL(KC_C)
#define KC_PC_PASTE LCTL(KC_V)
#define ES_LESS_MAC KC_GRAVE
#define ES_GRTR_MAC LSFT(KC_GRAVE)
#define ES_BSLS_MAC ALGR(KC_6)
#define NO_PIPE_ALT KC_GRAVE
#define NO_BSLS_ALT KC_EQUAL
#define LSA_T(kc) MT(MOD_LSFT | MOD_LALT, kc)
#define BP_NDSH_MAC ALGR(KC_8)
#define SE_SECT_MAC ALGR(KC_6)

enum layers {
  _BASE,
  _LOWER,
  _RAISE,
  _NAV,
  _FUNCTION,
};

#define LOWER LT(_LOWER, KC_SPACE)
#define RAISE LT(_RAISE, KC_ENT)
#define FUNCTION LT(_FUNCTION, KC_BSPC)
#define NAV LT(_NAV, KC_ESC)

const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
  [_BASE] = LAYOUT(
    KC_Q,    KC_W,    KC_E,    KC_R,    KC_T,               KC_Y,    KC_U,    KC_I,    KC_O,    KC_P,        
    KC_A,    KC_S,    KC_D,    KC_F,    KC_G,               KC_H,    KC_J,    KC_K,    KC_L,    KC_NO, 
    KC_Z,    KC_X,    KC_C,    KC_V,    KC_B,               KC_N,    KC_M,    SE_ARNG, SE_ADIA, SE_ODIA,          
                                  FUNCTION,    NAV,    LOWER,    RAISE
  ),

  [_LOWER] = LAYOUT(
    KC_EXLM,    SE_AT,    KC_HASH,    SE_DLR,     KC_PERC,             SE_CIRC,    SE_AMPR,    SE_LPRN,    SE_RPRN,    SE_PIPE,
    KC_TRNS,    SE_TILD,  MT(SE_BSLS, SE_SLSH),    MT(MOD_LSFT | KC_QUOT, KC_QUOT),    SE_LABK,             SE_RABK,    SE_LCBR,    SE_RCBR,    SE_LBRC,    SE_RBRC,        
    KC_TRNS,    KC_TRNS,  KC_TRNS,    KC_EXLM,    SE_QUES,             SE_EQL,     SE_PLUS,    SE_ASTR,    SE_MINS,    SE_PIPE,
                                                KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS        
  ),

  [_RAISE] = LAYOUT(
    KC_1,         KC_2,          KC_3,          KC_4,          KC_5,               KC_6,       KC_7,       KC_8,      KC_9,        KC_0,          
    KC_DELETE,    LCTL(KC_Z),    KC_TRNS,    KC_TRNS,    KC_TRNS,            KC_LEFT,    KC_DOWN,    KC_UP,     KC_RIGHT,    KC_TRNS, 
    TG(6),        LCTL(KC_Y),    KC_TRNS,       KC_TRNS,       KC_TRNS,            KC_TRNS,    KC_HOME,    KC_END,    KC_PGUP,     KC_PGDN,
                                                        KC_TRNS,    KC_TRNS,    KC_TRNS,    KC_TRNS
  ),

  [_NAV] = LAYOUT(
    KC_TRNS,             KC_MS_BTN1,    KC_MS_UP,       KC_MS_BTN2,     KC_TRNS,                 KC_TRNS,    KC_TRNS,    KC_MS_WH_UP,      KC_MS_BTN3,       KC_TRNS,
    KC_MS_ACCEL1,        KC_TRNS,       KC_MS_LEFT,     KC_MS_DOWN,     KC_MS_RIGHT,             KC_TRNS,    KC_TRNS,    KC_MS_WH_LEFT,    KC_MS_WH_DOWN,    KC_MS_WH_RIGHT,
    KC_MS_ACCEL2,        KC_TRNS,       KC_MS_ACCEL0,   KC_MS_ACCEL1,   KC_MS_ACCEL2,            KC_TRNS,    KC_TRNS,    KC_MS_BTN4,       KC_MS_BTN5,       KC_TRNS, 
                                                                    KC_TRNS,    KC_TRNS,    KC_TRNS,    KC_TRNS
  ),

  [_FUNCTION] = LAYOUT(
    KC_F1,      KC_F2,      KC_F3,      KC_F4,      KC_F5,              KC_F6,    KC_F7,    KC_F8,    KC_F9,    KC_F10,         
    KC_F11,     KC_F12,     KC_TRNS,    KC_TRNS,    KC_TRNS,            KC_TRNS,  KC_TRNS,  KC_TRNS,  KC_TRNS,  KC_TRNS,
    KC_TRNS,    KC_TRNS,    KC_TRNS,    KC_TRNS,    KC_TRNS,            KC_TRNS, KC_TRNS, KC_TRNS, KC_TRNS, QK_BOOT, 
                                    KC_TRNS,    KC_TRNS,    KC_TRNS,    KC_TRNS
  )
};
```

#### config.h

```h
/*
Copyright 2020 Pierre Chevalier <pierrechevalier83@gmail.com>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
*/

#pragma once
// Set the mouse settings to a comfortable speed/accuracy trade-off,
// assuming a screen refresh rate of 60 Htz or higher
// The default is 50. This makes the mouse ~3 times faster and more accurate
#define MOUSEKEY_INTERVAL 16
// The default is 20. Since we made the mouse about 3 times faster with the previous setting,
// give it more time to accelerate to max speed to retain precise control over short distances.
#define MOUSEKEY_TIME_TO_MAX 40
// The default is 300. Let's try and make this as low as possible while keeping the cursor responsive
#define MOUSEKEY_DELAY 100
// It makes sense to use the same delay for the mouseweel
#define MOUSEKEY_WHEEL_DELAY 100
// The default is 100
#define MOUSEKEY_WHEEL_INTERVAL 50
// The default is 40
#define MOUSEKEY_WHEEL_TIME_TO_MAX 100

// Pick good defaults for enabling homerow modifiers
#define TAPPING_TERM 200
#define PERMISSIVE_HOLD
#define TAPPING_FORCE_HOLD

#define EE_HANDS
```

#### rules.mk

```make
# Bootloader selection
BOOTLOADER = rp2040
CONVERT_TO = promicro_rp2040

# Build Options
#   change yes to no to disable
#
BOOTMAGIC_ENABLE = yes      # Enable Bootmagic Lite
MOUSEKEY_ENABLE = yes       # Mouse keys
EXTRAKEY_ENABLE = yes       # Audio control and System control
CONSOLE_ENABLE = no         # Console for debug
COMMAND_ENABLE = no         # Commands for debug and configuration
NKRO_ENABLE = no            # Enable N-Key Rollover
BACKLIGHT_ENABLE = no       # Enable keyboard backlight functionality
RGBLIGHT_ENABLE = no        # Enable keyboard RGB underglow
UNICODE_ENABLE = yes        # Unicode
AUDIO_ENABLE = no           # Audio output
SPLIT_KEYBOARD = yes        # Use shared split_common code
LAYOUTS = split_3x5_2xza
```

Useful resources:

- [Gettind Started with QMK](https://docs.qmk.fm/#/newbs_getting_started)
- [Firmware Configuration](https://docs.qmk.fm/#/feature_split_keyboard?id=firmware-configuration)
- [Basic Keycodes](https://docs.qmk.fm/#/keycodes_basic)
- [Mod Tapping](https://docs.qmk.fm/#/mod_tap)
