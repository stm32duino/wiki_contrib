# Core

This part describes the STM32 core functions.

## Core Callback

CoreCallback functions allows to register a callback function called in the loop of the main() function.  
If you need to call as often as possible a function to update your system and you want to be sure this function to be called, you can add it to the callback list. Otherwise, your function should be called inside the loop() function of
the sketch.

* **void registerCoreCallback(void (*func)(void))**: register a callback function  
_Params_ func pointer to the callback function  

* **void unregisterCoreCallback(void (*func)(void))**: unregister a callback function  
_Params_ func pointer to the callback function  

## Wiring

### Analog

`analogWriteFrequency(freq)` has been added in core version **> 1.5.0** to set the frequency used by `analogWrite()`. Default is `PWM_FREQUENCY` (1000) in Hertz.

**_Note_** frequency is common to all channels of a specified timer, setting the frequency for one channel will impact all others of the same timer.

#### Example
```C
  // Assuming Ax pins have PWM capabilities and use a different Timer.
  analogWrite(A1, 127); // Start PWM on A1, at 1000 Hz with 50% duty cycle
  analogWriteFrequency(2000); // Set PMW period to 2000 Hz instead of 1000
  analogWrite(A2, 64); // Start PWM on A2, at 2000 Hz with 25% duty cycle
  analogWriteFrequency(500); // Set PMW period to 500 Hz
  analogWrite(A3, 192); // Start PWM on A3, at 500 Hz with 75% duty cycle
```

[[/img/PWM_Freq.png|alt="PWM Freq result"]]

## HardwareSerial

By default, only one `Serial` instance is available.
To use a second serial port, a `HardwareSerial` object should be declared in the sketch before the `setup()` function:
```C++
//                      RX    TX
HardwareSerial Serial1(PA10, PA9);

void setup() {
  Serial1.begin(115200); 
}

void loop() {
  Serial1.println("Hello World!");
  delay(1000);
}
```
Another solution is to add a `build_opt.h` file alongside your main `.ino` file with: `-DENABLE_HWSERIAL1`.
This will define the `Serial1` instance using the first `USART1` instance found in the `PeripheralPins.c` of your variant.

Note that only the latter solution allows to use the `serialEvent1()` callback in the sketch.

# Built-In Library

This part describes the STM32 libraries provide with the core.

## SPI

STM32 SPI library has been modified with the possibility to manage several CS pins without to stop the SPI interface.  
_We do not describe here the [SPI Arduino API](https://www.arduino.cc/en/Reference/SPI) but the functionalities added._  

We give to the user 3 possiblities about the management of the CS pin:  
* the CS pin is managed directly by the user code before to transfer the data (like the Arduino SPI library)  
* or the user gives the CS pin number to the library API and the library manages itself the CS pin (see example below)  
* or the user uses a hardware CS pin linked to the SPI peripheral  

### New API functions

* **SPIClass::SPIClass(uint8_t mosi, uint8_t miso, uint8_t sclk, uint8_t ssel)**: alternative class constructor  
_Params_ SPI mosi pin  
_Params_ SPI miso pin  
_Params_ SPI sclk pin  
_Params_ (optional) SPI ssel pin. This pin must be an hardware CS pin. If you configure this pin, the chip select will be managed by the SPI peripheral. Do not use API functions with CS pin in parameter.

* **void SPIClass::begin(uint8_t _pin)**: initialize the SPI interface and add a CS pin  
_Params_ spi CS pin to be managed by the SPI library  

* **void beginTransaction(uint8_t pin, SPISettings settings)**: allows to configure the SPI with other parameter. These new parameter are saved this an associated CS pin.  
_Params_ SPI CS pin to be managed by the SPI library  
_Params_ SPI settings  

* **void endTransaction(uint8_t pin)**: removes a CS pin and the SPI settings associated  
_Params_ SPI CS pin managed by the SPI library  

**_Note 1_** The following functions must be called after initialization of the SPI instance with begin() or beginTransaction().  
If you have several device to manage, you can call beginTransaction() several time with different CS pin in parameter.  
Then you can call the following functions with different CS pin without call again beginTransaction() (until you call end() or endTransaction()).  

**_Note 2_** If the mode is set to SPI_CONTINUE, the CS pin is kept enabled. Be careful in case you use several CS pin.  

* **byte transfer(uint8_t pin, uint8_t _data, SPITransferMode _mode = SPI_LAST)**: write/read one byte  
_Params_ SPI CS pin managed by the SPI library  
_Params_ data to write  
_Params_ (optional) if SPI_LAST CS pin is reset, SPI_CONTINUE the CS pin is kept enabled.  
_Return_ byte received  

* **uint16_t transfer16(uint8_t pin, uint16_t _data, SPITransferMode _mode = SPI_LAST)**: write/read half-word  
_Params_ SPI CS pin managed by the SPI library  
_Params_ 16bits data to write  
_Params_ (optional) if SPI_LAST CS pin is reset, SPI_CONTINUE the CS pin is kept enabled.  
_Return_ 16bits data received  

* **void transfer(uint8_t pin, void *_buf, size_t _count, SPITransferMode _mode = SPI_LAST)**: write/read several bytes. Only one buffer used to write and read the data  
_Params_ SPI CS pin managed by the SPI library  
_Params_ pointer to data to write. The data will be replaced by the data read.  
_Params_ number of data to write/read.
_Params_ (optional) if SPI_LAST CS pin is reset, SPI_CONTINUE the CS pin is kept enabled.  

* **void transfer(byte _pin, void *_bufout, void *_bufin, size_t _count, SPITransferMode _mode = SPI_LAST)**: write/read several bytes. One buffer for the output data and one for the input data  
_Params_ SPI CS pin managed by the SPI library  
_Params_ pointer to data to write.  
_Params_ pointer where to store the data read.  
_Params_ number of data to write/read.  
_Params_ (optional) if SPI_LAST CS pin is reset, SPI_CONTINUE the CS pin is kept enabled.  

### Example

This is an example of the use of the CS pin management:  

```C++
#include <SPI.h>
//            MOSI  MISO  SCLK
SPIClass SPI3(PC12, PC11, PC10);

void setup() {
  SPI3.begin(2); //Enables the SPI3 instance with default settings and attaches the CS pin  
  SPI3.beginTransaction(1, settings); //Attaches another CS pin and configure the SPI3 instance with other settings  
  SPI3.transfer(2, 0x52); //Transfers data to the first device
  SPI3.transfer(1, 0xA4); //Transfers data to the second device. The SPI3 instance is configured with the right settings  
  SPI3.end() //SPI3 instance is disabled
}
```

## I2C
By default, only one `Wire` instance is available and it uses the Arduino pins 14 and 15.
To use a second i2c port, a `TwoWire` object should be declared in the sketch before the `setup()` function:
```C++
#include <Wire.h>
//            SDA  SCL
TwoWire Wire2(PB3, PB10);

void setup() {
  Wire2.begin(); 
}

void loop() {
  Wire2.beginTransmission(0x71);
  Wire2.write('v');
  Wire2.endTransmission();
  delay(1000);
}
```