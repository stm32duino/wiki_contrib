[[/img/Tips-icon.png|alt="Tips"]]Example of all below steps are shown in this PR: [Add Nucleo-F207ZG](https://github.com/stm32duino/Arduino_Core_STM32/pull/63) (ignore the 2 last commits)

[[/img/Warning-icon.png|alt="Warning"]] Since this PR, some enhancement has been done.
* CMSIS startup file definition is no more needed as they are all defined in the core. See [#70](https://github.com/stm32duino/Arduino_Core_STM32/issues/70)
* Custom startup file can be defined. [#353](https://github.com/stm32duino/Arduino_Core_STM32/pull/353)
* Use define instead of enum for pins in `variant.h`. See [#356](https://github.com/stm32duino/Arduino_Core_STM32/pull/353)
* STM32 HAL configuration is no more needed. See [#518](https://github.com/stm32duino/Arduino_Core_STM32/pull/518)

# Create a new variant
Go to the '_**variant**_' folder of the STM32 core.<br>
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-core-sources-files-location)

## 1 - Create a copy of the _**stm32/variants/board_template**_ folder with a name of your choice.

**Example**: To add variant for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html)

`cp -a board_template NUCLEO_F207ZG` (_linux_)

[[/img/Tips-icon.png|alt="Tips"]]It's also possible to copy one of the most similar board variant<br>

## 2 - Add pins mapping

All `PeripheralPins.c` and `PinNamesVar.h` for all STM32 MCU are provided with STM32 Tools packages and are available here: [Arduino_Tools/genpinmap/Arduino](https://github.com/stm32duino/Arduino_Tools/tree/master/src/genpinmap/Arduino)

[[/img/Tips-icon.png|alt="Tips"]]It's also possible to generate them manually, see [[genpinmap]] how to.

Copy the `PeripheralPins.c` and `PinNamesVar.h` file in the variant folder created.

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):

**_[genpinmap/Arduino/STM32F207Z(C-E-F-G)Tx/PeripheralPins.c](https://github.com/stm32duino/Arduino_Tools/blob/master/src/genpinmap/Arduino/STM32F207Z(C-E-F-G)Tx/PeripheralPins.c)_**<br>
and<br>
**_[genpinmap/Arduino/STM32F207Z(C-E-F-G)Tx/PinNamesVar.h](https://github.com/stm32duino/Arduino_Tools/blob/master/src/genpinmap/Arduino/STM32F207Z(C-E-F-G)Tx/PinNamesVar.h)_**<br>
to<br>
**_variant/NUCLEO_F207ZG/_**

## 3 - Review pins mapping
 
After **_PeripheralPins.c_** addition, review it carefully.<br>
Comment a line if the pin is generated several times for the same IP or<br>
if the pin should not be used (overlaid with some HW on the board, for instance)

Use the related user manual to define the best pins mapping:<br>
**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):<br>
[UM1974: STM32 Nucleo-144 boards](http://www.st.com/resource/en/user_manual/dm00244518.pdf)<br>
    
[[/img/Tips-icon.png|alt="Tips"]] It is also possible to check the equivalent file for mbed os:
[ST-Nucleo-F207ZG](https://developer.mbed.org/platforms/ST-Nucleo-F207ZG/)

## 4 - Review pins and signals pins numbering
Edit the **_variant.h_** and **_variant.cpp_** file.<br>
In **_variant.cpp_**:<br>
1. Fill the array `const PinName digitalPin[]`. This array allows to wrap Arduino pin number(Dx or x or PYx)
to STM32 PinName (PY_x).

In **_variant.h_**:<br>
1. Align the number of PinName defined above in `digitalPin[]` array in **_variant.h_**.<br>
Define all usable pins and its linked pin number which is the index in the `digitalPin[]` array.<br>
Example:
```
#define PG9  0
#define PG14 1
#define PF15 2
#define PE13 3
#define PF14 4
```

2. Review macros to point to the right pin name/number: `LED_BUILTIN, MOSI, MISO, SCLK, SDA, SCL,...`<br>
Note that some of them have a default value in the core. Only redefine them if different from the default one.<br>
See: https://github.com/stm32duino/Arduino_Core_STM32/blob/c392140415b3cf29100062ecb083adfa0f59f8b1/cores/arduino/pins_arduino.h#L142 <br>
[[/img/Tips-icon.png|alt="Tips"]] Here, you can add custom define to fit your needs<br>

## 5 - System Clock configuration
In **_variant.cpp_**, `void SystemClock_Config(void)` need to be defined.<br>
It could be generated thanks [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) or <br>
copied from a [STM32CubeYY](http://www.st.com/en/embedded-software/stm32cube-embedded-software.html?querycriteria=productId=LN1897) project examples 
(where 'YY' is the MCU serie)

From [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html):
1. Run [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html), create a _New Project_ and select the targeted MCU or the board if listed.
2. Go to **_Pinout_** tab, enable desired peripherals: `I2C, SDIO, SPI, USB,...`
3. Configure the clock:
    * If the board has an external crystal: set in **_Pinout_** tab `RCC->HSE` peripheral to `Crystal`.<br>
In **_Clock Configuration_**, set `HSE Input frequency` to the crystal one then set `PLL Source Mux` to `HSE`.<br>
    * Set `HCLK` to the maximum frequency, [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) will automatically configure the clock tree and resolve conlict if any.
4. Generate code. Set **_Toolchain/IDE_**: `SW4STM32`.<br>
[[/img/Tips-icon.png|alt="Tips"]] Clock configuration for peripherals will be also generated
5. Copy the `void SystemClock_Config(void)` generated in `src/main.c` to **_variant.cpp_**

## 6 - Update ldscript.ld
It could be generated thanks [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) or <br>
copied from a [STM32CubeYY](http://www.st.com/en/embedded-software/stm32cube-embedded-software.html?querycriteria=productId=LN1897) project examples 
(where 'YY' is the MCU serie)<br>
Replace the **_ldscript.ld_** in variant folder by the `STM32YYxxxxxx_FLASH.ld` generated by [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) in the root folder.<br>
**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html): `STM32F207ZGTx_FLASH.ld`

## 7 - HAL configuration
Since core version greater than **1.5.0**, a default STM32 HAL configuration is provided per STM32 series.
Refer to [[hal-configuration]].

Add in **_variant.h_** any extra HAL module to define.

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):<br>
```C
/* Extra HAL modules */
#define HAL_DAC_MODULE_ENABLED
#define HAL_ETH_MODULE_ENABLED
```

## 8 - Declare the variant
It still to add the menu and add relevant information (Flash and SRAM sizes, cpu freq,...)<br>
[[/img/Tips-icon.png|alt="Tips"]] See: [Arduino Boards.txt specifications](https://github.com/arduino/Arduino/wiki/Arduino-IDE-1.5-3rd-party-Hardware-specification#boardstxt) for further options.<br>
Edit **_boards.txt_** file, then:<br>
1. Copy one section which is the most similar to your board
2. Rename all `menu.pnum.<old_board_name>` by `menu.pnum.<new_board_name>`
3. Update `build.mcu=` and `build.cmsis_lib_gcc=` to the correct cortex-mX version
4. Update `build.series=` to the correct `STM32YYxx` (where `YY` is the MCU serie)
5. Update `build.product_line=` to the correct `STM32YYXXxx` MCU version.
6. Update `upload.maximum_size=` and `upload.maximum_data_size=` to the correct Flash and SRAM sizes

## 9 - Restart
Restart Arduino IDE and try your new board with [[Blink-example]]

