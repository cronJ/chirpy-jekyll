---
title: Starting with MicroPython on ESP32
date: 2018-12-30 09:43:00 +0200
categories: [Electronics, ESP32, Python]
tags: [electronics, esp32, micropython, python]
---

Yesterday I saw the recording of the talk from Christine Spindler on the 35c3 about MicroPython [here](https://media.ccc.de/v/35c3-9648-micropython_python_for_microcontrollers#t=2465), which was great by the way.
I heard about MicroPython before and had already looked into it.

So, because I have a MicroPython capable board lying on my bench, I will play a little with it.

## Get MicroPython running on the ESP32

The board lying on my bench is a `ESP32 DOIT v1`.
So, I need the MicroPython binary for this board.
You can find the binaries in the [download section](http://micropython.org/download) of the MicroPython page.
Scroll down to ESP32 or click on the ESP32 link on the page.
I'm using the latest version which is `esp32-20181230-v1.9.4-771-gb33f108cd.bin` at this time.
For the ESP32 are two firmware versions available.
One is the standard firmware (which I use here) and the other has built-in SPI RAM support.
So if you are unsure which version you need, take the standard version.
The website states that this version will work on any board.

To flash the binary onto the ESP32 board you need the [ESPTool](https://github.com/espressif/esptool).
For me the easiest way to install it was with `pip`.
So, if you already have Python installed on your computer, just install it that way.
I had to open a command line window under Windows 10 as administrator to install it properly.
Then type:

```
pip install esptool
```

It is recommended by the MicroPython website to erase the flash before flashing the MicroPython code onto the ESP32.
My board is detected on serial port COM4.
So, I use this command to erase the flash:

```
esptool.py --port COM4 erase_flash
```

Which results in this output:

```
esptool.py v2.5.1
Serial port COM4
Connecting........\_\_
Detecting chip type... ESP32
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...
Chip erase completed successfully in 4.5s
Hard resetting via RTS pin...
```

Now we can flash the MicroPython binary to the microcontroller:

```
esptool.py --chip esp32 --port COM4 write_flash -z 0x1000 esp32-20181230-v1.9.4-771-gb33f108cd.bin
```

This results in the following output:

```
esptool.py v2.5.1
Serial port COM4
Connecting........\_
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 1084016 bytes to 685353...
Wrote 1084016 bytes (685353 compressed) at 0x00001000 in 61.0 seconds (effective 142.3 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```

And that's it.
You now have MicroPython running on your ESP32.
And to check this we connect to the board via serial port.
I'm using Putty for that.
The default baud rate of the board is `115200`.

![MicroPython - Putty](/assets/img/2018-12-30-micropython/2018-12-30-micropython-putty.png)

## Conclusion

The installation of MicroPython onto the ESP32 is very easy.
But currently I only can write my code via the REPL.
So, I have to find a way to send my Python script from my preferred editor to the board.
We will see how practical the workflow is after using it a while.
