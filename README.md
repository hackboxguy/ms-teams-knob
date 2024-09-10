# ms-teams-knob
![ms-teams-knob-picture](/images/3key1knob.png "3key1knob-picture.")
Alternative firmware for CH552 based [3key-1knob COTS HW](https://amzn.eu/d/6oloNJh). It is Based on [3keys-1knob-firmware](https://github.com/biemster/3keys_1knob) but modified to be used as a shortcut keys for ms-teams application

- when key-1 is pressed, RGB LED's will turn **ON** to allow user to sync with current microphone mute/unmute state of ongoing teams-call
- when key-2 is pressed, **SHIFT+CTRL+M** key is sent to the host pc and LEDs on the shortcut keys will toggle, this results into microphone mute/unmoute action if MS-Teams app is highlighted on the windows PC
- when key-3 is pressed, RGB LED's will turn **OFF** to allow user to sync with current microphone mute/unmute state of ongoing teams-call

### compile:
`$ make bin`

### compile & flash to pad:
- If on original firmware of OEM: As explained [here](#howto),connect pin-12(UDP) of CH552 to +5V through a 10k resistor to enter bootloader mode
- If on this firmware: press key1 while connecting USB
- `$ make flash`
```
user@machine:~/multi-key-knob$ make flash
Compiling ms-teams-knob.c ...
Compiling include/usb_handler.c ...
Compiling include/usb_hid.c ...
Compiling include/delay.c ...
Compiling include/neo.c ...
Compiling include/usb_conkbd.c ...
Compiling include/usb_descr.c ...
Building multi-key-knob.ihx ...
Building multi-key-knob.bin ...
------------------
FLASH: 3205 bytes
IRAM:  26 bytes
XRAM:  274 bytes
------------------
Removing temporary files ...
Uploading to CH55x ...
Connecting to device ...
FOUND: CH552 with bootloader v2.50.
Erasing chip ...
Flashing multi-key-knob.bin to CH552 ...
SUCCESS: 3205 bytes written.
Verifying ...
SUCCESS: 3205 bytes verified.
DONE.
```

### How to overwrite OEM-Firmware? <a name="howto"></a>
![overwrite-oem-firmware](/images/overwrite-oem-firmware.jpg "overwrite-oem-firmware.")
- As shown above, prepare the setup by connecting a 10k pullup resistor(Pin-12 of CH552) to +5V
- When inserting mini-key-board to USB port of your Linux-Host-PC, ensure Pin-12 of CH552 is pulled up
- On your Linux-Host-PC, run ```make flash```
- Unplug mini-key-board and plug it back to see the effect of modifed opensource firmware(using sudo evtest /dev/input/eventX).
