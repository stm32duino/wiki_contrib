Herafter, a non exhaustive list of libraries compatible with the [STM32](https://github.com/stm32duino/Arduino_Core_STM32) core. 

Currently, libraries that come with the Arduino IDE should work (could required some pins update in the sketch).

All those using SPI, I2C should be fully compatible.

[[/img/Warning-icon.png|alt="Warning"]] _Arduino boards provide ICSP connector used by several Arduino shield for SPI signal: MISO/MOSI/SCK. STM32 boards do not have this ICSP connector, so this requires to manually wire those SPI signal on the desire pin (mainly: D11 to D13)_

## Built-in (delivered with the core package)
* SPI: follow the official [SPI](https://www.arduino.cc/en/Reference/SPI) API
* Wire (I2C): follow the official [Wire](https://www.arduino.cc/en/Reference/Wire) API.
* EEPROM: follow the official [EEPROM](https://www.arduino.cc/en/Reference/EEPROM) API.
* Servo: follow the official [Servo](https://www.arduino.cc/en/Reference/Servo) API. Need some review. Range is not correct.

## Dedicated
Some libraries have been developed to support specific hardware features:
* [STM32Ethernet](https://github.com/stm32duino/STM32Ethernet): for on board Ethernet port (ex: Nucleo-F429ZI).<br>
This library is fully compatible with Arduino [Ethernet](https://www.arduino.cc/en/Reference/Ethernet) API.
* [STM32SD](https://github.com/stm32duino/STM32SD): for board with SD card slot (ex: Disco-F746).<br>
This library is fully compatible with Arduino [SD](https://www.arduino.cc/en/Reference/SD) API.

Goal is to have all dedicated STM32 libraries available through the "_**Library Manager**_"

Have a look here to see which one are available or thanks the "_**Library Manager**_"

http://www.arduinolibraries.info/architectures/stm32

## Official from Arduino
* [TFT](https://github.com/arduino-libraries/TFT/): required [arduino-libraries/TFT#11](https://github.com/arduino-libraries/TFT/pull/11) else use [Ucglib_Arduino](https://github.com/olikraus/Ucglib_Arduino)
* [LiquidCrystal](https://github.com/arduino-libraries/LiquidCrystal)
* [Ethernet](https://github.com/arduino-libraries/Ethernet)
* [WiFi](https://github.com/arduino-libraries/WiFi)

## Third party
`ARDUINO_ARCH_STM32` must be used as differentiator.
### Tested
* [Firmata](https://github.com/firmata/arduino): since release [2.5.7](https://github.com/firmata/arduino/releases/tag/2.5.7)
* [Ucglib_Arduino](https://github.com/olikraus/Ucglib_Arduino): tested with ST7735
