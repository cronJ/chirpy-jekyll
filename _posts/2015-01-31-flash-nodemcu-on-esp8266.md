---
title: Flash NodeMcu on ESP8266 (ESP-01 Modul)
date: 2015-01-31 21:52:32 +0200
categories: [Electronics]
tags: [electronic, esp8266, nodemcu]
---

<!-- prettier-ignore-start -->
> There is a new guide for flashing NodeMcu on ESP8266. See [link](/posts/getting-nodemcu-running-on-an-ESP-01-module-in-2016/)
{: .prompt-info }
<!-- prettier-ignore-end -->

## Introduction

A little instruction on how to flash NodeMCU on your ESP-01 module.
Then you can run LUA code on your ESP8266.

Hardware needed:

- ESP-01 module
- FTDI UM232R as USB-to-serial adapter (or a compatible adapter)

Software needed:

- Git
- Python 2
- Hterm (or any software to view serial communication)

## Connection of the module

Pin definition and mapping to the signal names:

![ESP-01_PinNumber](/assets/img/2015/01/ESP-01_PinNumber.png)

1. GND
2. UTXD
3. GPIO2
4. CH_PD
5. GPIO0
6. RST/GPIO16
7. URXD
8. VCC

The following mapping works for me:

```
VCC   -> 3V3
GND   -> GND
RST   -> 3V3
CH_PD -> 3V3
URXD  -> DB0 (UM232R)
UTXD  -> DB1 (UM232R)
GPIO0 -> GND
GPIO2 -> 3V3
```

The jumper for JP1 on the FTDI serial adapter needs to connect 1 and 2, which selects an IO voltage of 3.3 V.
Power will be supplied from an external power supply.

## Preparation for the flashing

Load the following flash tool by cloning the GitHub repository:

```
git clone https://github.com/themadinventor/esptool.git
```

Now you can load the NodeMCU firmware by cloning it from GitHub:

```
git clone https://github.com/nodemcu/nodemcu-firmware.git
```

After the last step, you can copy the `nodemcu_latest.bin` from `./pre_build/latest/` into the esptool folder.
It is also sufficient to only load this file from GitHub without cloning the whole repository.

## Flash NodeMCU

Now we can flash the NodeMCU firmware to the module.
Check the serial port number in your hardware manager.
My module is connected to port 11.
So, I will use COM11 for the next command.

```
python esptool.py --port COM11 write_flash 0x0000 nodemcu_latest.bin
```

When you encounter an issue where the module is not found, try installing the pyserial module which seems to be missing.

```
pip install pyserial
```

If there are connection problems, try reconnecting pin CH_PD to 3.3 V.
Maybe you need to repeat this step until the flash process starts.

## Test the new firmware

If the flash process was successful we can check if the new firmware runs.
We need to establish a serial communication to the module.
Use the following settings for the connection with Hterm:

- `COM-port` - Used for the flash command (COM11 on my module)
- `baud rate` is 9600
- `newline` needs to be set to CR+LF (carriage return and line feed)
- `Input control` set to ASCII
- `CR+LF` for “send on enter”.

When you reset your module the following should be written to the serial interface:

```
NodeMCU 0.9.5 build 20150127 &nbsp;powered by Lua 5.1.4
lua: cannot open init.lua>
```

For a quick test, we connect an LED with a resistor from GPIO0 to GND.
With the following commands, we can toggle the LED via the console.

```lua
gpio.mode(3, gpio.OUTPUT) -- GPIO set to OUTPUT
gpio.write(3, 1) -- GPIO set to HIGH
gpio.write(3, 0) -- GPIO set to LOW
```

The number 3 in the command describes the IO index. GPIO0 has the IO index 3 and not 0. Here you can find the [pin map for the `gpio` module](https://nodemcu.readthedocs.io/en/master/modules/gpio/#gpio-module).

I will add other test scripts with advanced functionality in the future.
