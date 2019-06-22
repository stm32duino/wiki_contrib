# Custom definitions

Several definitions can be redefined by the end user by different ways:
 * using `build_opt.h` file, see [[Customize-build-options-using-build_opt.h]]
 * in the `variant.h`
 * using `hal_conf_extra.h` file, see [[HAL-configuration#core-version--150-1]]

## Re-evaluate interrupt priority values

Default IRQ priorities are defined in the core which can be re-defined using below definitions:
* `UART_IRQ_PRIO`
* `EXTI_IRQ_PRIO`
* `I2C_IRQ_PRIO`
* `RTC_IRQ_PRIO`
* `TIM_IRQ_PRIO`
* `USBD_IRQ_PRIO`

Same for IRQ sub-priorities:
* `UART_IRQ_SUBPRIO`
* `EXTI_IRQ_SUBPRIO`
* `I2C_IRQ_SUBPRIO`
* `RTC_IRQ_SUBPRIO`
* `TIM_IRQ_SUBPRIO`
* `USBD_IRQ_SUBPRIO`

#### Example:
Using `build_opt.h`:
`-DUSBD_IRQ_PRIO=2 -DUSBD_IRQ_SUBPRIO=2`

## Custom startup file

Core use a default startup file included thanks `CMSIS_STARTUP_FILE` definition:

https://github.com/stm32duino/Arduino_Core_STM32/blob/master/cores/arduino/stm32/startup_stm32yyxx.S

which is defined thanks:

https://github.com/stm32duino/Arduino_Core_STM32/blob/master/cores/arduino/stm32/stm32_def_build.h

and  provided thanks the CMSIS Device from ST (in `STM32YYxx/Source/Templates/gcc/`):

https://github.com/stm32duino/Arduino_Core_STM32/tree/master/system/Drivers/CMSIS/Device/ST

It is possible to redefine the `CMSIS_STARTUP_FILE` or define a custom startup file in the variant.
    
### Redefine the default startup file:

Using `build_opt.h`:
  `-DCMSIS_STARTUP_FILE=\"mystartup_file.s\"`

Then add your `mystartup_file.s` in the sketch folder (i.e. in a tab of your sketch files).

#### Example for _Nucleo_L476RG_:

`-DCMSIS_STARTUP_FILE=\"startup_stm32l476xx.s\`

### Custom startup file in the variant

It required to define `CUSTOM_STARTUP_FILE` in the `boards.txt` and add a `*.S` file in the `variant/` folder.

Syntax in the board.txt:
`xxx.build.startup_file=-DCUSTOM_STARTUP_FILE`
    
#### Example for _Nucleo_L476RG_:

`Nucleo_64.menu.pnum.NUCLEO_L476RG.build.startup_file=-DCUSTOM_STARTUP_FILE`

Then add a `*.S` file in the `variant/NUCLEO_L476RG/` folder.

[[/img/Important-icon.png|alt="Important"]] **Important note: file extension must be `.S` not `.s`**