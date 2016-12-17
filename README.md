# How to configure GH60 keyboard on Mac
-------------------

## Preparation
* `homebrew` install `crosspack` and `dfu-programmer`

## Download firmware
First clone `git clone https://github.com/kairyu/tmk_keyboard_custom.git`, next
```
cd tmk_keyboard_custom
git clone https://github.com/kairyu/tmk_core_custom.git
rm -rf tmk_core
ln -s tmk_core_custom tmk_core
```

## Modify the source code

`cd ~/tmk_keyboard_custom/keyboard/gh60`

* Configure the GH60 type: In `config.h`, after `#define CONFIG_H`, add
```
#define GH60_REV_CHN 1
```
* In the makefile, comment out this line `KEYMAP_IN_EEPROM_ENABLE = yes`

## Make your customized keyboard layout in `keymap_yourname.c`
Reference: [`keymap_bigeagle.c`](https://gist.github.com/bigeagle/16a6c48dde34076f7649)

## Build and download it to the keyboard
Check your device status: `system_profiler SPUSBDataType`.
**Keyboard mode**
```
GH60:

          Product ID: 0x6060
          Vendor ID: 0xfeed
          Version: 0.01
          Speed: Up to 12 Mb/sec
          Manufacturer: geekhack
          Location ID: 0x14100000 / 14
          Current Available (mA): 500
          Current Required (mA): 100
```

Reset your keyboard and you could enter writable mode:
**Writable mode**
```
ATm32U4DFU:

          Product ID: 0x2ff4
          Vendor ID: 0x03eb  (Atmel Corporation)
          Version: 0.00
          Serial Number: 1.0.0
          Speed: Up to 12 Mb/sec
          Manufacturer: ATMEL
          Location ID: 0x14100000 / 15
          Current Available (mA): 500
          Current Required (mA): Unknown (Device has not been configured)
```

Then, `make KEYMAP=jenny dfu`. Done!

## References:
* [Philo](http://www.philo.top/2016/01/03/gh60/)
* [ptt](https://www.ptt.cc/bbs/Key_Mou_Pad/M.1430970988.A.4D9.html) 
* [blog](http://blog.dm4.tw/blog/2015/03/17/build-gh60-revchn-on-mac/)
