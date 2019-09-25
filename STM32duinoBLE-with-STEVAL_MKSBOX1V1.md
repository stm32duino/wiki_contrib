STM32duinoBLE library does not work with the stock firmware that is loaded in the BLE module of STEVAL-MKSBOX1V1.
For this reason, first of all, it is needed to solder on STEVAL-MKSBOX1V1 a JTAG/SWD 0.05" pitch 10pin male connector in the apposite space of the PCB.

[[/img/SensorTile_Box1.PNG|alt="Space on PCB where soldering the JTAG connector"]]

Then you can use a standard ST-Link V2-1 with a JTAG/SWD 0.05" pitch 10pin to 20pin IDC cable together with [STSW-BNRGFLASHER](https://www.st.com/content/st_com/en/products/embedded-software/wireless-connectivity-software/stsw-bnrgflasher.html) software tool (currently available only for Windows PC) in order to update the firmware of the BLE module of STEVAL-MKSBOX1V1.

First of all, install the ST BlueNRG-1_2 Flasher Utility and open it, then select the SWD tab:

[[/img/SensorTile_Box2.PNG|alt="SWD tab of ST BlueNRG-1_2 Flasher Utility"]]

Erase the flash memory of the BlueNRG-1 chip:

[[/img/SensorTile_Box3.PNG|alt="Erase of the BlueNRG-1 chip"]]

Download the Link Layer Only firmware for the BLE module from the following link:

[DTM_LLOnly.bin](https://github.com/stm32duino/wiki/raw/master/wiki/STEVAL-MKSBOX1V1/DTM_LLOnly.bin)

Load the Link Layer Only firmware in the ST BlueNRG-1_2 Flasher Utility and then press the "Flash" button:

[[/img/SensorTile_Box4.PNG|alt="Load and flash the new firmware into BlueNRG-1 chip"]]

If you need to restore the original version of the BlueNRG-1 firmware, you can repeat the procedure using this firmware image:

[DTM_Full.bin](https://github.com/stm32duino/wiki/raw/master/wiki/STEVAL-MKSBOX1V1/DTM_Full.bin)
