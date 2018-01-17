# BSidesLeeds2018Badge

A repo for code and information about the BSides Leeds Badge 2018!

## Badge Information

The badge requires two things:
1. STM32F103 development board - a 'blue pill' dev board for the ARM-based STM32F103 chip
1. A USB to UART board using the CP2102 IC
1. 2x 20x1 pin female header for 2.54mm pitch pins
1. 1x 6x1 pin femal header for 2.54mm pitch pins
1. 1x ST-Link v2 programmer

## Setup

Solder the pin headers onto the PCB, and plug in the STM32F1 board as indicated (with the USB socket on the correct side) and connect the USB to UART board, too, ensuring that the GND pin is on the right side. 

Now, wire up the ST-Link v2 programmer to the programming pins (a 4-pin header on the dev board) in the usual way. If this is your first time, this should be: 
* 3V3 to 3V3
* SWDIO to SWDIO
* SWCLK to SWCLK (might just be labelled 'CLK' on the board)
* GND to GND

Now you are ready to program the dev board.

## Programming the STM32F103

There are some given firmware files, ending in `.bin` in the repo, but we'll give a generic method for programming a file `firmware.bin` onto the SMT32F1 board. We will assume you're using a Linux system/VM. 

First download and install OpenOCD - download and instruction can be found here: https://sourceforge.net/projects/openocd/files/openocd/0.10.0/

Now that this is installed, `cd` to the directory where `firmware.bin` is located. Connect the ST-Link V2 programmer to a USB port, and use the following command 
```sudo openocd -f target/stm32f1x.cfg -f interface/stlink-v2.cfg -c "init" -c "reset halt" -c "stm32f1x unlock 0" -c "flash write_image erase unlock firmware.bin 0x08000000" -c "exit" ```

**NB** - make sure to change `firmware.bin` for the name of the `.bin` file you want to flash. 

## Hacking stuff

Well, now you know how to flash firmware, and you're probably familiar with some basic C code, the world is now your oyster! :) Source code is/will be included in this repo so you can tinker to your heart's content, and maybe make something cool!

# HAPPY HACKING!
