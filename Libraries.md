

Libraries using basic features like Serial, SPI, I2C,... should be fully compatible with [STM32](https://github.com/stm32duino/Arduino_Core_STM32) core. Pin updates could be required in the sketch.

* [Built-in (delivered with the core package)](https://github.com/stm32duino/wiki/wiki/Libraries#built-in-delivered-with-the-core-package)
* [Dedicated](https://github.com/stm32duino/wiki/wiki/Libraries#dedicated)
* [Expansion boards](https://github.com/stm32duino/wiki/wiki/Libraries#expansion-boards)
  * [X-NUCLEO Expansion Boards](https://github.com/stm32duino/wiki/wiki/Libraries#x-nucleo-expansion-boards)
  * [Other expansion board](https://github.com/stm32duino/wiki/wiki/Libraries#other-expansion-board)
* [Official from Arduino](https://github.com/stm32duino/wiki/wiki/Libraries#official-from-arduino)
* [Third party](https://github.com/stm32duino/wiki/wiki/Libraries#third-party)
  * [Tested](https://github.com/stm32duino/wiki/wiki/Libraries#tested)

[[/img/Warning-icon.png|alt="Warning"]] _Arduino boards provide ICSP connector used by several Arduino shields for SPI signal: MISO/MOSI/SCK. STM32 boards do not have this ICSP connector, so this requires to manually wire those SPI signals to the desired pin (mainly: D11 to D13)_

[[/img/Note-icon.png|alt="Note"]] All dedicated STM32 libraries are available through the "_**Library Manager**_"
or have a look hereafter to see which one is available:

* http://www.arduinolibraries.info/architectures/stm32

## Built-in (delivered with the core package)

* EEPROM: follow the official [EEPROM](https://www.arduino.cc/en/Reference/EEPROM) API
* Servo: follow the official [Servo](https://www.arduino.cc/en/Reference/Servo) API
* SoftwareSerial: follow the official [SoftwareSerial](https://www.arduino.cc/en/Reference/softwareSerial) API.<br>
  It uses an **hardware timer**. Interrupt is triggered at a `frequency = Baudrate * OVERSAMPLE` (by default _3*baudrate_) to handle RX as well as TX transmissions.
  This impacts CPU load specially at high baudrate.
* SPI: follow the official [SPI](https://www.arduino.cc/en/Reference/SPI) API
* Wire (I2C): follow the official [Wire](https://www.arduino.cc/en/Reference/Wire) API

## Dedicated

Some libraries have been developped to support specific features (hardware or not):

* [STM32Ethernet](https://github.com/stm32duino/STM32Ethernet): for on board Ethernet port (ex: Nucleo-F429ZI). This library is fully compatible with Arduino [Ethernet](https://www.arduino.cc/en/Reference/Ethernet) API. It depends on the following libraries:
  * [LwIP](https://github.com/stm32duino/LwIP): lightweight TCP/IP stack (LwIP) is a small independent implementation of the TCP/IP protocol suite
  
  Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/STM32Ethernet)
* [STM32FreeRTOS](https://github.com/stm32duino/STM32FreeRTOS): this is a port of [FreeRTOS](https://www.freertos.org/) for STM32 as Arduino libraries
* [STM32LowPower](https://github.com/stm32duino/STM32LowPower): to support some STM32 low power mode. It depends on the following libraries:
  * [STM32RTC](https://github.com/stm32duino/STM32RTC)
* [STM32RTC](https://github.com/stm32duino/STM32RTC): to support the real-time clock (RTC) controller embedded in the STM32 microcontrollers. It is based on the Arduino RTCZero library
* [STM32SD](https://github.com/stm32duino/STM32SD): to support SDIO or SDMMC controller for board with SD card slot (ex: Disco-F746). This library is fully compatible with Arduino [SD](https://www.arduino.cc/en/Reference/SD) API. It depends on the following libraries:
  * [FatFS](https://github.com/stm32duino/FatFs): FatFs is a generic FAT file system module for small embedded systems. The FatFs is written in compliance with ANSI C and completely separated from the disk I/O layer. Therefore it is independent of hardware architecture


* [HTS221](https://github.com/stm32duino/HTS221): to support the HTS221 capacitive digital sensor for relative humidity and temperature.
  Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/HTS221)
* [IIS2MDC](https://github.com/stm32duino/IIS2MDC):  to support the IIS2MDC high-performance 3-axis magnetometer
* [ISM330DLC](https://github.com/stm32duino/ISM330DLC): to support the ISM330DLC 3D accelerometer and 3D gyroscope
* [LIS2DW12](https://github.com/stm32duino/LIS2DW12): to support the LIS2DW12 3D accelerometer
* [LIS2MDL](https://github.com/stm32duino/LIS2MDL):  to support the LIS2MDL high-performance 3-axis magnetometer
* [LIS3DHH](https://github.com/stm32duino/LIS3DHH): to support the LIS3DHH 3D accelerometer
* [LIS3MDL](https://github.com/stm32duino/LIS3MDL): to support the LIS3MDL high-performance 3-axis magnetometer. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/LIS3MDL)
* [LPS22HB](https://github.com/stm32duino/LPS22HB): to support the LPS22HB 260-1260 hPa absolute digital ouput barometer. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/LPS22HB)
* [LPS25HB](https://github.com/stm32duino/LPS25HB): to support the LPS25HB 260-1260 hPa absolute digital ouput barometer
* [LPS22HH](https://github.com/stm32duino/LPS22HH): to support the LPS22HH 260-1260 hPa absolute digital ouput barometer
* [LSM303AGR](https://github.com/stm32duino/LSM303AGR): to support the LSM303AGR 3D accelerometer and 3D magnetometer
* [LSM6DSO](https://github.com/stm32duino/LSM6DSO): to support the LSM6DSO 3D accelerometer and 3D gyroscope
* [LSM6DSOX](https://github.com/stm32duino/LSM6DSOX): to support the LSM6DSOX 3D accelerometer and 3D gyroscope
* [LSM6DS0](https://github.com/stm32duino/LSM6DS0): to support the LSM6DS0 3D accelerometer and 3D gyroscope
* [LSM6DS3 ](https://github.com/stm32duino/LSM6DS3): to support the LSM6DS3 3D accelerometer and 3D gyroscope
* [LSM6DSL](https://github.com/stm32duino/LSM6DSL): to support the LSM6DSL 3D accelerometer and 3D gyroscope. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/LSM6DSL)
* [M24SR64-Y](https://github.com/stm32duino/M24SR64-Y): to support the dynamic NFC/RFID Tag IC dual interface M24SR64-Y. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/M24SR64-Y)
* [MX25R6435F](https://github.com/stm32duino/MX25R6435F): to support the Quad-SPI NOR Flash memory MX25R6435F. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/MX25R6435F)
* [Proximity Gesture](https://github.com/stm32duino/Proximity_Gesture): o support gesture-detection using proximity sensors (VL53L0X or VL53L1X or VL6180X). The APIs provide single swipe gesture detection, directional (left/right) swipe gesture detection and single tap gesture detection
* [SPBTLE-RF](https://github.com/stm32duino/SPBTLE-RF): to support the Bluetooth (V4.1 compliant) SPBTLE-RF. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/SPBTLE-RF)
* [ST25DV](https://github.com/stm32duino/ST25DV): to support the ST25DV components
* [STTS22H](https://github.com/stm32duino/STTS22H): to support the STTS22H digital temperature sensor
* [STTS751](https://github.com/stm32duino/STTS751): to support the STTS751 digital temperature sensor
* [VL53L0X](https://github.com/stm32duino/VL53L0X): to support the VL53L0X Time-of-Flight and gesture-detection sensor. Dedicated [Wiki page](https://github.com/stm32duino/wiki/wiki/VL53L0X)
* [VL53L1X](https://github.com/stm32duino/VL53L1X): to support the VL53L1X Time-of-Flight and gesture-detection sensor
* [VL6180X](https://github.com/stm32duino/VL6180X): to support the VL6180X proximity and ambient light sensing (ALS) sensor
* [WiFi-ISM43362-M3G-L44](https://github.com/stm32duino/WiFi-ISM43362-M3G-L44): to support the Wi-Fi module Inventek ISM43362-M3G-L44 (802.11 b/g/n)

## Expansion boards

### [X-NUCLEO Expansion Boards](https://www.st.com/en/evaluation-tools/stm32-nucleo-expansion-boards.html])

Hereafter, an exhaustive list of Arduino libraries to support [X-NUCLEO Expansion Boards](https://www.st.com/en/evaluation-tools/stm32-nucleo-expansion-boards.html]).
These libraries are guaranteed to work fine with all NUCLEO boards supported in the [STM32](https://github.com/stm32duino/Arduino_Core_STM32) Core. They could also work with standard Arduino boards but I suggest to check before electrical and pinout compatibility of [X-NUCLEO Expansion Boards](https://www.st.com/en/evaluation-tools/stm32-nucleo-expansion-boards.html]) with standard Arduino boards.


* [X-NUCLEO-53L0A1](https://github.com/stm32duino/X-NUCLEO-53L0A1): it is an expansion board for the STM32 Nucleo based on VL53L0X Time-of-Flight and gesture-detection sensor. It depends on the following libraries:

  * [VL53L0X](https://github.com/stm32duino/VL53L0X)
  * [Proximity Gesture](https://github.com/stm32duino/Proximity_Gesture)

* [X-NUCLEO-53L1A1](https://github.com/stm32duino/X-NUCLEO-53L1A1): it is an expansion board for the STM32 Nucleo based on VL53L1X Time-of-Flight and gesture-detection sensor. It depends on the following libraries:

  * [VL53L1X](https://github.com/stm32duino/VL53L1X)
  * [Proximity Gesture](https://github.com/stm32duino/Proximity_Gesture)

* [X-NUCLEO-6180XA1](https://github.com/stm32duino/X-NUCLEO-6180XA1): it is an expansion board for the STM32 Nucleo based on VL6180X proximity sensor, gesture and ambient light sensing (ALS) module. It depends on the following libraries:

  * [VL6180X](https://github.com/stm32duino/VL6180X)
  * [Proximity Gesture](https://github.com/stm32duino/Proximity_Gesture)

* [X-NUCLEO-GNSS1A1](https://github.com/stm32duino/X-NUCLEO-GNSS1A1): to support the X-NUCLEO-GNSS1A1 expansion board using the TESEO-LIV3F module. It depends on the following libraries:
  * [MicroNMEA](https://github.com/stevemarple/MicroNMEA)

[[/img/Note-icon.png|alt="Note"]] In order to perform the firmware upgrade, the following Java application should be used:
  * [Teseo-LIV3F-Flash-Updater](https://github.com/stm32duino/Teseo-LIV3F-Flash-Updater)

* [X-NUCLEO-IDB05A1](https://github.com/stm32duino/X-NUCLEO-IDB05A1): it is a Bluetooth Low Energy evaluation board based on the SPBTLE-RF BlueNRG-MS RF module. It depends on the following library:

  * [SPBTLE-RF](https://github.com/stm32duino/SPBTLE-RF)

* [X-NUCLEO-IKA01A1](https://github.com/stm32duino/X-NUCLEO-IKA01A1): it is a multifunctional expansion board based on operational amplifiers.

* [X-NUCLEO-IKS01A1](https://github.com/stm32duino/X-NUCLEO-IKS01A1): it is a motion MEMS and environmental sensor expansion board for the STM32 Nucleo. It depends on the following libraries:

  * [LSM6DS0](https://github.com/stm32duino/LSM6DS0)
  * [LSM6DS3 ](https://github.com/stm32duino/LSM6DS3)
  * [LIS3MDL](https://github.com/stm32duino/LIS3MDL)
  * [LPS25HB](https://github.com/stm32duino/LPS25HB)
  * [HTS221](https://github.com/stm32duino/HTS221)

* [X-NUCLEO-IKS01A2](https://github.com/stm32duino/X-NUCLEO-IKS01A2): it is a motion MEMS and environmental sensor expansion board for the STM32 Nucleo. It depends on the following libraries:

  * [LSM6DSL](https://github.com/stm32duino/LSM6DSL)
  * [LSM303AGR](https://github.com/stm32duino/LSM303AGR)
  * [LPS22HB](https://github.com/stm32duino/LPS22HB)
  * [HTS221](https://github.com/stm32duino/HTS221)

* [X-NUCLEO-IKS01A3](https://github.com/stm32duino/X-NUCLEO-IKS01A3): it  is a motion MEMS and environmental sensor expansion board for the STM32 Nucleo. It depends on the following libraries:

  * [LSM6DSO](https://github.com/stm32duino/LSM6DSO)
  * [LIS2DW12](https://github.com/stm32duino/LIS2DW12)
  * [LIS2MDL](https://github.com/stm32duino/LIS2MDL)
  * [HTS221](https://github.com/stm32duino/HTS221)
  * [LPS22HH](https://github.com/stm32duino/LPS22HH)
  * [STTS751](https://github.com/stm32duino/STTS751)
  * [LSM6DSOX](https://github.com/stm32duino/LSM6DSOX)

* [X-NUCLEO-IHM02A1](https://github.com/stm32duino/X-NUCLEO-IHM02A1): it is a two axis stepper motor driver expansion board based on the L6470 component.
* [X-NUCLEO-IHM12A1](https://github.com/stm32duino/X-NUCLEO-IHM12A1): it is a low voltage dual brush DC motor driver expansion board based on the STSPIN240.
* [X-NUCLEO-LED61A1](https://github.com/stm32duino/X-NUCLEO-LED61A1): it is an expansion board based on the LED6001 component.
* [X-NUCLEO-NFC01A1](https://github.com/stm32duino/X-NUCLEO-NFC01A1): it is a Dynamic NFC tag evaluation board based on the M24SR64-Y NFC Type 4/RFID tag IC. It depends on the following library:

  * [M24SR64-Y](https://github.com/stm32duino/M24SR64-Y)

* [X-NUCLEO-NFC03A1](https://github.com/stm32duino/X-NUCLEO-NFC03A1): it is an NFC card reader evaluation board based on CR95HF-VMD5T that supports the detection, reading and writing of NFC Forum Type 1, 2, 3 and 4 tags.
* [X-NUCLEO-NFC04A1](https://github.com/stm32duino/X-NUCLEO-NFC04A1): it is a dynamic NFC/RFID tag IC expansion board based on the ST25DV04K NFC Type V/RFID tag IC. It depends on the following library:

  * [ST25DV](https://github.com/stm32duino/ST25DV)

* [X-NUCLEO-S2868A1](https://github.com/stm32duino/X-NUCLEO-S2868A1): it is a wireless sub-1 GHz expansion board based on S2-LP radio and operates in the 868 MHz ISM frequency band. It depends on the following libraries:

  * [S2-LP](https://github.com/stm32duino/S2-LP)
  * [M95640-R](https://github.com/stm32duino/M95640-R)

* [X-NUCLEO-S2868A2](https://github.com/stm32duino/X-NUCLEO-S2868A2): it is a wireless sub-1 GHz expansion board based on S2-LP radio and operates in the 868 MHz ISM frequency band. It depends on the following libraries:

  * [S2-LP](https://github.com/stm32duino/S2-LP)
  * [M95640-R](https://github.com/stm32duino/M95640-R)

* [X-NUCLEO-S2915A1](https://github.com/stm32duino/X-NUCLEO-S2915A1): it is a wireless sub-1 GHz expansion board based on S2-LP radio and operates in the 915 MHz ISM frequency band. It depends on the following libraries:

  * [S2-LP](https://github.com/stm32duino/S2-LP)
  * [M95640-R](https://github.com/stm32duino/M95640-R)


### Other expansion board

* [I-NUCLEO-LRWAN1](https://github.com/stm32duino/I-NUCLEO-LRWAN1): to support I-NUCLEO-LRWAN1 LoRa® expansion board based on USI® LoRaWAN™ technology module

Herafter, a non exhaustive list of libraries known as compatible with the [STM32](https://github.com/stm32duino/Arduino_Core_STM32) core.

## Official from Arduino
* [TFT](https://github.com/arduino-libraries/TFT/): since release [1.0.6](https://github.com/arduino-libraries/TFT/releases/tag/1.0.6) else use [Ucglib_Arduino](https://github.com/olikraus/Ucglib_Arduino)
* [LiquidCrystal](https://github.com/arduino-libraries/LiquidCrystal)
* [Ethernet](https://github.com/arduino-libraries/Ethernet)
* [WiFi](https://github.com/arduino-libraries/WiFi)

## Third party
`ARDUINO_ARCH_STM32` must be used as differentiator.
### Tested
* [arduino-LoRa](https://github.com/sandeepmistry/arduino-LoRa): tested with B-L072Z-LRWAN1
* [Firmata](https://github.com/firmata/arduino): since release [2.5.7](https://github.com/firmata/arduino/releases/tag/2.5.7)
* [OneWire](https://github.com/PaulStoffregen/OneWire): Library for Dallas/Maxim 1-Wire Chips
* [PubSubClient](https://github.com/knolleary/PubSubClient): tested using L475 disco IOT using WiFi
* [RTClib](https://github.com/adafruit/RTClib): tested with Adafruit module 3296
* [Ucglib_Arduino](https://github.com/olikraus/Ucglib_Arduino): tested with ST7735
* [UIPEthernet](https://github.com/UIPEthernet/UIPEthernet): tested with ENC28j60 module
