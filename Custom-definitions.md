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

## Custom PinMap array

Each variant provides a `PeripheralPins.c` including all `PinMap` arrays per STM32 peripherals: `ADC`, `I2C`, `SPI`, `TIM`, `U(S)ART`, `USB`,...

Each array provides a default mapping for which peripheral instance is used for a pin.

Anyway, a pin can be used with several peripheral instances so to be able to override this default mapping, those arrays can be overridden at sketch level as they are defined as `WEAK`.

### Example for the [ADC PinMap](https://github.com/stm32duino/Arduino_Core_STM32/blob/801ce35cea1faaf78c53ab501765d53fa3a60ced/variants/NUCLEO_F103RB/PeripheralPins.c#L43) of the NUCLEO_F103RB:

```C
#ifdef HAL_ADC_MODULE_ENABLED
WEAK const PinMap PinMap_ADC[] = {
  {PA_0,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 0, 0)}, // ADC1_IN0
  //  {PA_0,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 0, 0)}, // ADC2_IN0
  {PA_1,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 1, 0)}, // ADC1_IN1
  //  {PA_1,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 1, 0)}, // ADC2_IN1
  //  {PA_2,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 2, 0)}, // ADC1_IN2 - STLink Tx
  //  {PA_2,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 2, 0)}, // ADC2_IN2 - STLink Tx
  //  {PA_3,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 3, 0)}, // ADC1_IN3 - STLink Rx
  //  {PA_3,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 3, 0)}, // ADC2_IN3 - STLink Rx
  {PA_4,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 4, 0)}, // ADC1_IN4
  //  {PA_4,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 4, 0)}, // ADC2_IN4
  {PA_5,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 5, 0)}, // ADC1_IN5
  //  {PA_5,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 5, 0)}, // ADC2_IN5
  {PA_6,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 6, 0)}, // ADC1_IN6
  //  {PA_6,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 6, 0)}, // ADC2_IN6
  {PA_7,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 7, 0)}, // ADC1_IN7
  //  {PA_7,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 7, 0)}, // ADC2_IN7
  {PB_0,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 8, 0)}, // ADC1_IN8
  //  {PB_0,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 8, 0)}, // ADC2_IN8
  {PB_1,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 9, 0)}, // ADC1_IN9
  //  {PB_1,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 9, 0)}, // ADC2_IN9
  {PC_0,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 10, 0)}, // ADC1_IN10
  //  {PC_0,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 10, 0)}, // ADC2_IN10
  {PC_1,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 11, 0)}, // ADC1_IN11
  //  {PC_1,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 11, 0)}, // ADC2_IN11
  {PC_2,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 12, 0)}, // ADC1_IN12
  //  {PC_2,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 12, 0)}, // ADC2_IN12
  {PC_3,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 13, 0)}, // ADC1_IN13
  //  {PC_3,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 13, 0)}, // ADC2_IN13
  {PC_4,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 14, 0)}, // ADC1_IN14
  //  {PC_4,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 14, 0)}, // ADC2_IN14
  {PC_5,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 15, 0)}, // ADC1_IN15
  //  {PC_5,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 15, 0)}, // ADC2_IN15
  {NC,    NP,    0}
};
#endif
```

PA_0 is configured to use ADC1 with channel 0 while it could also used ADC2 with channel 0.

So, it can be redefined at sketch level to use the `ADC2` and also remove useless ADC pin to save space, hereafter PA_1 is kept (_-144 bytes_):
```C
const PinMap PinMap_ADC[] = {
  {PA_0,  ADC2,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 0, 0)}, // ADC2_IN0
  {PA_1,  ADC1,  STM_PIN_DATA_EXT(STM_MODE_ANALOG, GPIO_NOPULL, 0, 1, 0)}, // ADC1_IN1
  {NC,    NP,    0}
};
```