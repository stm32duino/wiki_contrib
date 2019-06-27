# Upload methods

## Mass Storage

This upload method is mainly dedicated to boards manufactured by ST which integrate a ST-Link: [Nucleo](https://www.st.com/en/evaluation-tools/stm32-nucleo-boards.html), [Discovery](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-discovery-kits.html), [Eval](https://www.st.com/en/evaluation-tools/stm32-eval-boards.html).

This enables drag-and-drop flash programming, so there is no need for a separate debug probe. 
The mass storage device of the ST-Link is a virtual disk, copy on this disk a binary will program it.
Once programmed into the MCU the copied binary disappears from the virtual disk.

## STLink
[[/img/Warning-icon.png|alt="Warning"]] _**Deprecated since core version > 1.5.0**_ replaced by [STM32CubeProgrammer (SWD)](https://github.com/stm32duino/wiki/wiki/Upload-methods#SWD)

Requires a [ST-Link/V2](https://www.st.com/content/st_com/en/products/development-tools/hardware-development-tools/hardware-development-tools-for-stm32/st-link-v2.html) device connected to the PC over USB and to the board via the SWD interface.

[[/img/Tips-icon.png|alt="Tips"]]  Several boards manufactured by ST integrate ST-Link: [Nucleo](https://www.st.com/en/evaluation-tools/stm32-nucleo-boards.html), [Discovery](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-discovery-kits.html), [Eval](https://www.st.com/en/evaluation-tools/stm32-eval-boards.html).

Be sure that the necessary driver for Windows is installed ([available here](https://www.st.com/en/development-tools/stsw-link009.html)) and the ST-Link adapter is updated to the latest firmware ([application to upgrade the firmware](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-programmers/stsw-link007.html)).

Only 3 pins are required for basic programming and debugging of the STM32 MCU devices (4 if the board is powered by the programmer) using Serial Debug Wire (SWD):

* GND
* SWDIO
* SWCLK
* 3.3V (optional)

[[/img/Important-icon.png|alt="ImportantIcon"]] **Avoid wired 3.3V to the target board if it is already powered by an other source (external supply, USB,..) else you may damage the board, programmer, USB port or external supply.**

Refers to [ST-Link V2 user Manual](https://www.st.com/resource/en/user_manual/dm00026748.pdf) and the board documentations (User Manual, schematics,...) to ensure connect to the right pins.

## Serial
[[/img/Warning-icon.png|alt="Warning"]] _**Deprecated since core version > 1.5.0**_ replaced by [STM32CubeProgrammer (Serial)](https://github.com/stm32duino/wiki/wiki/Upload-methods#serial-1)

This requires to restart the STM32 in 'native bootloader' mode and rely on `Boot` pins. Check in [STM32 microcontroller system memory boot mode AN2606](https://www.st.com/content/ccc/resource/technical/document/application_note/b9/9b/16/3a/12/1e/40/0c/CD00167594.pdf/files/CD00167594.pdf/jcr:content/translations/en.CD00167594.pdf) which pattern to apply to activate the bootloader for the dedicated STM32 MCU. Check also which U(S)ART is used.

[[/img/Warning-icon.png|alt="Warning"]] A serial port or additional USB to Serial adapter is needed.

Connect `power`, `GND`, and `Tx/Rx` pins of the serial adapter to your STM32 U(S)ART. 

Adapter `Tx` goes to STM32 `Rx` and `Rx` goes to STM32 `Tx`.

## BMP (Black Magic Probe)

Refers to [Black Magic Probe](https://github.com/blacksphere/blackmagic) site and its [Getting-Started](https://github.com/blacksphere/blackmagic/wiki/Getting-Started) Wiki.

## STM32CubeProgrammer
[[/img/Warning-icon.png|alt="Warning"]] _**Since core version > 1.5.0**_

[[/img/under-construction.jpg|alt="Under construction"]]

### SWD

### Serial

### DFU

## HID Bootloader 2.2 (HID BL)
This is a driverless USB bootloader for `STM32F10x` and `STM32F4xx` MCUs and is based on [HID protocol](https://en.wikipedia.org/wiki/Human_interface_device). No special USB drivers are needed, even on Windows.


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

