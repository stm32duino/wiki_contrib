# Upload methods

[[/img/under-construction.jpg|alt="Under construction"]]

## Mass Storage

## STLink
[[/img/Warning-icon.png|alt="Warning"]] _**Deprecated since core version > 1.5.0**_

## Serial
[[/img/Warning-icon.png|alt="Warning"]] _**Deprecated since core version > 1.5.0**_

## BMP (Black Magic Probe)

## STM32CubeProgrammer
[[/img/Warning-icon.png|alt="Warning"]] _**Since core version > 1.5.0**_

### SWD

### Serial

### DFU

## HID Bootloader 2.2 (HID BL)
This is a driverless USB bootloader for `STM32F10x` and `STM32F4xx` MCUs and is based on [HID protocol](https://en.wikipedia.org/wiki/Human_interface_device). No special USB drivers needed, even on Windows.


The bootloader is installed at `0x8000000` address.
On **STM32F103**, the bootloader consumes only `2 kB` of flash memory (0x800). 
The user code area starts at `0x8000800`

The **STM32F4xx** MCUs have built-in `DFU` (Device Firmware Upgrade) but you can also use HID BL for uploading firmwares.

* The advantage of using HID BL instead of the DFU bootloader is that the entire firmware update process is automatic. You do not have to press any button or set any PCB jumper. 

* The downside is that the `F4` HID BL firmware is larger than the `F1` version, consuming `16kB` (0x4000) of available flash memory.

The `hid-flash` tool is available on Windows, Linux and MacOS.

Details of HID bootloader v2.2 (and newer) hid-flash tool as well as ready-to-use binary files can be found at the GitHub repository: https://github.com/Serasidis/STM32_HID_Bootloader

## Maple DFU Bootloader
[[/img/Warning-icon.png|alt="Warning"]] _**Since core version > 1.5.0**_

Extract from the legacy wiki page about bootloaders (http://wiki.stm32duino.com/index.php?title=Bootloader):

In order to simplify the upload process leveraging the USB device, Leaflabs developed a custom DFU bootloader that needs to be uploaded in the MCU at address `0x08000000` via one of the standard STM upload methods (ST Link or standard STM serial bootloader); this custom bootloader is called the **_original Maple bootloader_**.
Leaflabs' documentation about the original Maple bootloader can be found here: 
http://docs.leaflabs.com/static.leaflabs.com/pub/leaflabs/maple-docs/latest/bootloader.html

[stm32duino.com](http://stm32duino.com/) guys modified the **_original Maple bootloader_** in order to:
 * enable support for STM32F103 non-Maple boards (blue pill and other generic boards)
 * fix issues found in the original Maple bootloader
 * reduce the bootloader size so that enlarging the memory available to user sketches
 * remove the option to upload to RAM

This modified version of the _Maple bootloader_ is known as STM32duino-bootloader or also **_bootloader 2.0_**.
Details about the STM32duino-bootloader as well as ready to use binary files can be found in the GitHub repository: https://github.com/rogerclarkmelbourne/STM32duino-bootloader

**Notes:**
 * Maple devices (including clones) generally come with the original Maple bootloader preloaded.
 * Generic STM32F103 boards on the other side come with no custom bootloader installed.
 * Maple bootloader 2.0 consumes 8KB of flash.
 * Maple bootloader original consumes 20kb of flash and some of the SRAM.

