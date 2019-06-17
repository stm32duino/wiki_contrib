# Custom definitions

Several definitions can be redefined by the end user in different ways:
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