# API

 * [Core](https://github.com/stm32duino/wiki/wiki/API#core)
   * [Core version](https://github.com/stm32duino/wiki/wiki/API#core-version)
   * [Core Callback](https://github.com/stm32duino/wiki/wiki/API#core-callback)
 * [Wiring](https://github.com/stm32duino/wiki/wiki/API#wiring)
   * [Analog](https://github.com/stm32duino/wiki/wiki/API#analog)
   * [HardwareSerial](https://github.com/stm32duino/wiki/wiki/API#hardwareserial)
 * [Built-In Library](https://github.com/stm32duino/wiki/wiki/API#built-in-ibrary)
   * [SPI](https://github.com/stm32duino/wiki/wiki/API#spi)
   * [I2C](https://github.com/stm32duino/wiki/wiki/API#i2C)

# Core

This part describes the STM32 core functions.

## Core version
This was introduced introduced core version greater than **1.5.0**.
It is based on Semantic Versioning 2.0.0 (https://semver.org/).

This ease core dependencies and defined [here](https://github.com/stm32duino/Arduino_Core_STM32/blob/d7c6b8b39b5dad3e5aa929cfa6ff235197aeea36/cores/arduino/stm32/stm32_def.h#L5-L21).

`STM32_CORE_VERSION` defines the core version with:
 * `STM32_CORE_VERSION_MAJOR`: major version [31:24]
 * `STM32_CORE_VERSION_MINOR`: minor version [23:16]
 * `STM32_CORE_VERSION_PATCH`: patch version [15:8]
 * `STM32_CORE_VERSION_EXTRA`: Extra label [7:0]
   with:
   * `0`: official release
   * `[1-9]`: release candidate
   * `F[0-9]`: development

### Example

```C
#if !defined(STM32_CORE_VERSION) || (STM32_CORE_VERSION  <= 0x01050000)
/* Do something for core version lesser than or equal to 1.5.0 */
#else
/* Do something for core version greater than 1.5.0 */
#endif
```

## Core Callback

CoreCallback functions allows to register a callback function called in the loop of the `main()` function. 
If you need to call as often as possible a function to update your system and you want to be sure this function to be called, you can add it to the callback list. Otherwise, your function should be called inside the `loop()` function of
the sketch.

* `void registerCoreCallback(void (*func)(void))`: register a callback function  
_Params_ `func` pointer to the callback function  

* `void unregisterCoreCallback(void (*func)(void))`: unregister a callback function  
_Params_ `func` pointer to the callback function  

[[/img/Warning-icon.png|alt="Warning"]] By default, the core callback feature is disabled, to enable it `CORE_CALLBACK` must be defined.

`build_opt.h` can be used to define it by adding `-DCORE_CALLBACK`, see [build_opt.h wiki](https://github.com/stm32duino/wiki/wiki/Customize-build-options-using-build_opt.h).

# Wiring

## Analog

### Frequency
`analogWriteFrequency(freq)` has been added in core version greater than **1.5.0** to set the frequency used by `analogWrite()`. Default is `PWM_FREQUENCY` (1000) in Hertz.

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

### ADC internal channels
Available in core version greater than **1.5.0**

`analogRead()` can now be used to read some  internal channels with the following definitions:
 * `ATEMP`: internal temperature sensor
 * `AVREF`: VrefInt, internal voltage reference
 * `AVBAT`: Vbat voltage

A minimum ADC sampling time is required when reading internal channels so default is set it to max possible value. It can be defined more precisely by defining:
 * `ADC_SAMPLINGTIME_INTERNAL`
to the desired ADC sample time.

`ADC_SAMPLINGTIME` and `ADC_CLOCK_DIV` could also be redefined by the variant or using `build_opt.h`.

#### Example
Hereafter an usage example which read then convert to proper Unit the 3 internal channels + A0:
```C
#include "stm32yyxx_ll_adc.h"

/* Values available in datasheet */
#define CALX_TEMP 25
#if defined(STM32F1xx)
#define V25       1430
#define AVG_SLOPE 4300
#define VREFINT   1200
#elif defined(STM32F2xx)
#define V25       760
#define AVG_SLOPE 2500
#define VREFINT   1210
#endif

/* Analog read resolution */
#if ADC_RESOLUTION == 10
#define LL_ADC_RESOLUTION LL_ADC_RESOLUTION_10B
#define ADC_RANGE 1024
#else
#define LL_ADC_RESOLUTION LL_ADC_RESOLUTION_12B
#define ADC_RANGE 4096
#endif
// the setup routine runs once when you press reset:
void setup() {
  // initialize serial communication at 9600 bits per second:
  Serial.begin(9600);
  analogReadResolution(ADC_RESOLUTION);
}

static int32_t readVref()
{
#ifdef __LL_ADC_CALC_VREFANALOG_VOLTAGE
  return (__LL_ADC_CALC_VREFANALOG_VOLTAGE(analogRead(AVREF), LL_ADC_RESOLUTION));
#else
  return (VREFINT * ADC_RANGE / analogRead(AVREF)); // ADC sample to mV
#endif
}

#ifdef ATEMP
static int32_t readTempSensor(int32_t VRef)
{
#ifdef __LL_ADC_CALC_TEMPERATURE
  return (__LL_ADC_CALC_TEMPERATURE(VRef, analogRead(ATEMP), LL_ADC_RESOLUTION));
#elif defined(__LL_ADC_CALC_TEMPERATURE_TYP_PARAMS)
  return (__LL_ADC_CALC_TEMPERATURE_TYP_PARAMS(AVG_SLOPE, V25, CALX_TEMP, VRef, analogRead(ATEMP), LL_ADC_RESOLUTION));
#else
  return 0;
#endif
}
#endif

static int32_t readVoltage(int32_t VRef, uint32_t pin)
{
  return (__LL_ADC_CALC_DATA_TO_VOLTAGE(VRef, analogRead(pin), LL_ADC_RESOLUTION));
}

// the loop routine runs over and over again forever:
void loop() {
  // print out the value you read:
  Serial.print("VRef(mv)= ");
  int32_t VRef = readVref();
  Serial.print(VRef);

#ifdef ATEMP
  Serial.print("\tTemp(°C)= ");
  Serial.print(readTempSensor(VRef));
#endif
#ifdef AVBAT
  Serial.print("\tVbat(mv)= ");
  Serial.print(readVoltage(VRef, AVBAT));
#endif

  Serial.print("\tA0(mv)= ");
  Serial.println(readVoltage(VRef, A0));
  delay(200);
}
```

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

### New API functions

#### Change default `Serial` instance pins 
It is also possible to change the default pins used by the `Serial` instance using above API:

* `void setRx(uint32_t rx)`
* `void setTx(uint32_t tx)`
* `void setRx(PinName rx)`
* `void setTx(PinName tx)`

##### Example:
```C++
    Serial.setRx(PG_9); // using pin name PY_n
    Serial.setTx(PG14); // using pin number PYn
    Serial.begin(9600);
```

# Built-In Library

This part describes the STM32 libraries provide with the core.

## SPI

STM32 SPI library has been modified with the possibility to manage several CS pins without to stop the SPI interface.  
_We do not describe here the [SPI Arduino API](https://www.arduino.cc/en/Reference/SPI) but the functionalities added._  

We give to the user 3 possibilities about the management of the CS pin:  
* the CS pin is managed directly by the user code before to transfer the data (like the Arduino SPI library)  
* or the user gives the CS pin number to the library API and the library manages itself the CS pin (see example below)  
* or the user uses a hardware CS pin linked to the SPI peripheral  

### New API functions

* `SPIClass::SPIClass(uint8_t mosi, uint8_t miso, uint8_t sclk, uint8_t ssel)`: alternative class constructor  
_Params_ SPI `mosi` pin  
_Params_ SPI `miso` pin  
_Params_ SPI `sclk` pin  
_Params_ (optional) SPI `ssel` pin. This pin must be an hardware CS pin. If you configure this pin, the chip select will be managed by the SPI peripheral. Do not use API functions with CS pin in parameter.

* `void SPIClass::begin(uint8_t _pin)`: initialize the SPI interface and add a CS pin  
_Params_ SPI CS `pin` to be managed by the SPI library  

* `void beginTransaction(uint8_t pin, SPISettings settings)`: allows to configure the SPI with other parameter. These new parameter are saved this an associated CS pin.  
_Params_ SPI CS `pin` to be managed by the SPI library  
_Params_ SPI `settings`  

* `void endTransaction(uint8_t pin)`: removes a CS pin and the SPI settings associated  
_Params_ SPI CS `pin` managed by the SPI library  

**_Note 1_** The following functions must be called after initialization of the SPI instance with `begin()` or `beginTransaction()`.  
If you have several device to manage, you can call `beginTransaction()` several time with different CS pin in parameter.  
Then you can call the following functions with different CS pin without call again `beginTransaction()` (until you call `end()` or `endTransaction()`).  

**_Note 2_** If the mode is set to `SPI_CONTINUE`, the CS pin is kept enabled. Be careful in case you use several CS pin.  

* `byte transfer(uint8_t pin, uint8_t _data, SPITransferMode _mode = SPI_LAST)`: write/read one byte  
_Params_ SPI CS `pin` managed by the SPI library  
_Params_ `data` to write  
_Params_ (optional) if `SPI_LAST` `mode` the CS pin is reset, `SPI_CONTINUE` `mode` the CS pin is kept enabled.
_Return_ byte received  

* `uint16_t transfer16(uint8_t pin, uint16_t _data, SPITransferMode _mode = SPI_LAST)`: write/read half-word  
_Params_ SPI CS `pin` managed by the SPI library  
_Params_ 16 bits `data` to write  
_Params_ (optional) if `SPI_LAST` `mode` the CS pin is reset, `SPI_CONTINUE` `mode` the CS pin is kept enabled.
_Return_ 16 bits data received  

* `void transfer(uint8_t pin, void *_buf, size_t _count, SPITransferMode _mode = SPI_LAST)`: write/read several bytes. Only one buffer used to write and read the data  
_Params_ SPI CS `pin` managed by the SPI library  
_Params_ pointer to `data` to write. The `data` will be replaced by the data read.  
_Params_ `count` is number of data to write/read.
_Params_ (optional) if `SPI_LAST` `mode` the CS pin is reset, `SPI_CONTINUE` `mode` the CS pin is kept enabled.

* `void transfer(byte _pin, void *_bufout, void *_bufin, size_t _count, SPITransferMode _mode = SPI_LAST)`: write/read several bytes. One buffer for the output data and one for the input data  
_Params_ SPI CS `pin` managed by the SPI library  
_Params_ `_bufout` is pointer to data to write.  
_Params_ `_bufin` id pointer where to store the data read.  
_Params_ `count` is number of data to write/read.  
_Params_ (optional) if `SPI_LAST` `mode` the CS pin is reset, `SPI_CONTINUE` `mode` the CS pin is kept enabled.  

##### Example

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

#### Change default `SPI` instance pins 
It is also possible to change the default pins used by the `SPI` instance using above API:

* `void setMISO(uint32_t miso)`
* `void setMOSI(uint32_t mosi)`
* `void setSCLK(uint32_t sclk)`
* `void setSSEL(uint32_t ssel)`
* `void setMISO(PinName miso)`
* `void setMOSI(PinName mosi)`
* `void setSCLK(PinName sclk)`
* `void setSSEL(PinName ssel)`

##### Example:
```C++
    SPI.setMISO(PC_4); // using pin name PY_n
    SPI.setMOSI(PC2); // using pin number PYn
    SPI.begin(2);
```

## I2C

By default, only one `Wire` instance is available and it uses the Arduino pins 14 and 15.
To use a second I2C port, a `TwoWire` object should be declared in the sketch before the `setup()` function:
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

Refers to [I2C Timing](https://github.com/stm32duino/wiki/wiki/Custom-definitions#i2c-timing) to customize I2C speed if needed.

### New API functions

#### Change default `Wire` instance pins 
It is also possible to change the default pins used by the `Wire` instance using above API:

* `void setSCL(uint32_t scl)`
* `void setSDA(uint32_t sda)`
* `void setSCL(PinName scl)`
* `void setSDA(PinName sda)`

##### Example:
```C++
    Wire.setSDA(PC_4); // using pin name PY_n
    Wire.setSCL(PC2); // using pin number PYn
    Wire.begin();
```

#### Enable general call mode
Available in core version greater than **1.5.0**

Adding `true` as last parameters of the 3 `Wire::begin()` methods will enable the general call mode otherwise `false` per default:

* `void begin(bool generalCall = false)`
* `void begin(uint8_t, bool generalCall = false)`
* `void begin(int, bool generalCall = false)`

##### Example
`Wire.begin(true);` or `Wire.begin(0x70,true);`