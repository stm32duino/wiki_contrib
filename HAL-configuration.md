# HAL module configuration

## core version <= **1.5.0**
Each variants had to include a STM32 HAL configuration file named `stm32yyxx_hal_conf.h`.
Where `yy` is one of the supported STM32 series in lowercase (ex: `f2`).

File can be:
 * generated thanks [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html).
Copy the `stm32yyxx_hal_conf.h` file generated to the `Inc/` folder to variant folder. 

 * copied from a [STM32CubeYY](http://www.st.com/en/embedded-software/stm32cube-embedded-software.html?querycriteria=productId=LN1897) project examples (where `YY` is the MCU serie)

**Example name** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html): `stm32f2xx_hal_conf.h`

[[/img/Tips-icon.png|alt="Tips"]] If you copied the `variants/board_template` folder, **_stm32yyxx_hal_conf.h_** have to be deleted.<br>

Then edit copied file in order to:
 * Remove line: `#include "main.h"`
 * Enable/Disable (un)desired HAL modules by (un)commenting line like:
 `#define HAL_XXX_MODULE_ENABLED`
 where "`_XXX_`" is the feature (`ETH`, `I2S`,...)
 * Adjust `HSE`/`HSI` values adaptation if needed
 * Update any other configurations if needed

[[/img/Warning-icon.png|alt="Warning"]] Below HAL module have to be disabled, they are handled thanks Arduino menu:
 * `HAL_UART_MODULE_ENABLED`
 * `HAL_PCD_MODULE_ENABLED`

## core version > **1.5.0**
Since core version greater than **1.5.0**, a default STM32 HAL configuration is provided per STM32 series.
As those files were almost the same for the same series, a default one per series avoid to add one for each variant.

Each required STM32 HAL configuration file is in `system/STM32YYxx/` (where `YY` is the MCU serie).<br>

It allows to wrap to the correct HAL configurations. Example for a STM32F2: [stm32f2xx_hal_conf.h](https://github.com/stm32duino/Arduino_Core_STM32/blob/master/system/STM32F2xx/stm32f2xx_hal_conf.h)
```C
/* STM32F2xx specific HAL configuration options. */
#if __has_include("hal_conf_custom.h")
#include "hal_conf_custom.h"
#else
#if __has_include("hal_conf_extra.h")
#include "hal_conf_extra.h"
#endif
#include "stm32f2xx_hal_conf_default.h"
#endif
```
Each `stm32yyxx_hal_conf_default.h` file disabled all HAL modules and include the same `stm32yyxx_hal_conf.h` file available here: [cores/arduino/stm32/stm32yyxx_hal_conf.h](
https://github.com/stm32duino/Arduino_Core_STM32/blob/master/cores/arduino/stm32/stm32yyxx_hal_conf.h)

This file handles:
 * mandatory HAL modules definition
the default list of modules to be used in the HAL driver
 * HAL module enabled by default which can be disabled
 * HAL modules not defined by default

Extra HAL modules can be enabled/disabled in `variant.h` (if required) or in a file named (at sketch level):
 * `hal_conf_extra.h`
    
Custom HAL configuration file can replace the default one by adding a file named (at sketch level):
 * `hal_conf_custom.h`

[[/img/Important-icon.png|alt="Important"]] **All below HAL modules or defines are listed for convenience but  may not be up to date. Refer to [cores/arduino/stm32/stm32yyxx_hal_conf.h](
https://github.com/stm32duino/Arduino_Core_STM32/blob/master/cores/arduino/stm32/stm32yyxx_hal_conf.h) to make sure having up to date values.**

## Mandatory HAL module enabled by default
* `HAL_MODULE_ENABLED`
* `HAL_CORTEX_MODULE_ENABLED`
* `HAL_DMA_MODULE_ENABLED`: Required by other modules
* `HAL_FLASH_MODULE_ENABLED`
* `HAL_GPIO_MODULE_ENABLED`
* `HAL_PWR_MODULE_ENABLED`
* `HAL_RCC_MODULE_ENABLED`

## HAL module enabled by default which can be disabled
* `HAL_ADC_MODULE_ENABLED`
* `HAL_I2C_MODULE_ENABLED`
* `HAL_RTC_MODULE_ENABLED`
* `HAL_SPI_MODULE_ENABLED`
* `HAL_TIM_MODULE_ENABLED`

## HAL modules not defined by default
* `HAL_DAC_MODULE_ENABLED`
* `HAL_ETH_MODULE_ENABLED`
* `HAL_SD_MODULE_ENABLED`
* `HAL_QSPI_MODULE_ENABLED`

## HAL modules not defined, handled thanks Arduino menu
* `HAL_UART_MODULE_ENABLED`
* `HAL_PCD_MODULE_ENABLED`

## List of `DISABLED` definition
* `HAL_ADC_MODULE_DISABLED`
* `HAL_I2C_MODULE_DISABLED`
* `HAL_RTC_MODULE_DISABLED`
* `HAL_SPI_MODULE_DISABLED`
* `HAL_TIM_MODULE_DISABLED`
* `HAL_DAC_MODULE_DISABLED`
* `HAL_EXTI_MODULE_DISABLED`: interrupt API does not used HAL EXTI module anyway API is cleaned with this
* `HAL_ETH_MODULE_DISABLED`
* `HAL_SD_MODULE_DISABLED`
* `HAL_QSPI_MODULE_DISABLED`

[[/img/Tips-icon.png|alt="Tips"]] Disable unused features can reduce significantly FLASH and RAM usage.

### Example of `Blink.ino` for Nucleo-L031K6 with 32768 bytes of Flash and 8192 bytes of RAM:

| | Flash Size(%) | RAM Size(%) |
| :---: | :---: | :---: |
| Default (Serial enabled) | 11152 (34%) | 780 (9%) |
| HAL disabled* | 4292 (13%) | 52 (0%) |
| diff size(%) | -6860 (-21%) | -778 (-9%) |

\*With all `HAL_*_MODULE_DISABLED` defined in `hal_conf_extra.h` and `Serial` disabled