STM32duinoBLE library does not work with the stock firmware that is loaded in the BLE module of X-NUCLEO-BNRG2A1 expansion board.

For this reason, first of all, it is needed to solder on X-NUCLEO-BNRG2A1, if it is not soldered, a 0 Ohm resistor at R117.

Then you can use a standard ST-Link V2-1 with 5 jumper wires female-female together with [STSW-BNRGFLASHER](https://www.st.com/content/st_com/en/products/embedded-software/wireless-connectivity-software/stsw-bnrgflasher.html) software tool (currently available only for Windows PC) in order to update the firmware of the BLE module of X-NUCLEO-BNRG2A1.

You need to connect the J12 pins of the X-NUCLEO-BNRG2A1 to the pins of the ST-Link V2-1 as shown in the picture below.

[[/img/X_NUCLEO_BNRG2A1_1.PNG|alt="Connection among the J12 pins of the X-NUCLEO-BNRG2A1 and the ST-Link V2-1"]]

In particular we have the following connections:

| | J12 | ST-Link V2-1 |
| --- | --- | --- |
| Pin | 1 | 1  |
| Pin | 2 | 9  |
| Pin | 3 | 12 |
| Pin | 4 | 7  |
| Pin | 5 | 15 |

First of all, install the ST BlueNRG-1_2 Flasher Utility and open it, then select the SWD tab:

[[/img/X_NUCLEO_BNRG2A1_2.PNG|alt="SWD tab of ST BlueNRG-1_2 Flasher Utility"]]

Erase the flash memory of the BlueNRG-2 chip:

[[/img/X_NUCLEO_BNRG2A1_3.PNG|alt="Erase of the BlueNRG-2 chip"]]

Download the Link Layer Only firmware for the BLE module from the following link:

[DTM_LLOnly.bin](https://github.com/stm32duino/wiki/raw/master/X-NUCLEO-BNRG2A1/DTM_LLOnly.bin)

Load the Link Layer Only firmware in the ST BlueNRG-1_2 Flasher Utility and then press the "Flash" button:

[[/img/X_NUCLEO_BNRG2A1_4.PNG|alt="Load and flash the new firmware into BlueNRG-2 chip"]]

If you need to restore the stock firmware of the BLE module of X-NUCLEO-BNRG2A1, you can repeat the procedure using this firmware image:

[DTM_Full.bin](https://github.com/stm32duino/wiki/raw/master/X-NUCLEO-BNRG2A1/DTM_Full.bin)

If you should find some issues during the update process, you can try to repeat the procedure closing the J15 jumper on the X-NUCLEO-BNRG2A1 expansion board.
