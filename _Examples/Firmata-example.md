## Firmata example on [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)

See [Firmata library](https://www.arduino.cc/en/Reference/Firmata) for further information.

1. If not already done, download and install the [Arduino software (IDE)](https://www.arduino.cc/en/Main/Software) for the required OS.
([Windows](https://www.arduino.cc/en/Guide/Windows), [Linux](https://www.arduino.cc/en/Guide/linux) or [Mac](https://www.arduino.cc/en/Guide/MacOSX) instructions)

2. Configure the IDE to the desired board. 

  See [[Getting-Started#configuring-ide]]

3. Open the Firmata sketch from the "**File> Examples > Firmata > StandardFirmata**"

  **Note:** Firmata library has been updated for the STM32 core. That's why _Firmata_ is displayed twice.
  1. "Examples for any board" section
  2. "Examples for Nucleo-64" section

  Select the _firmata_ for the _Nucleo-64_
  [[/img/SelectSpecificExample.png|alt="StandardFirmata example selection"]]

4. Click the upload button

  See [[Getting-Started#upload-method]] to change the upload method.

  [[/img/Upload.png|alt="Upload"]]

When board restart, LED blinking several time (indicating Firmata version). **Firmata **is ready to use.

## Test with [ScratchX](http://scratchx.org/)
**Firmata **client test are available here: (no installation required)
[www.firmata.org](http://www.firmata.org/wiki/Main_Page)

## Test with [ScratchX](http://scratchx.org/)
Firmata can be tested with [ScratchX](http://scratchx.org/) using the [Scratch Arduino Extension](http://khanning.github.io/scratch-arduino-extension/index.html).
Please, follow the [Getting Started](http://khanning.github.io/scratch-arduino-extension/gettingstarted.html) since step 2.

Some examples, which could be loaded with the plugin, for the Nucleo L476RG:
*  [Blink-Nucleo-l476.sbx](https://github.com/stm32duino/wiki/raw/master/examples/scratchx/Blink-Nucleo-l476.sbx): LED blinking every second.
*  [Button-Nucleo-l476.sbx](https://github.com/stm32duino/wiki/raw/master/examples/scratchx/Button-Nucleo-l476.sbx): LED is switch off when blue button is pressed.
*  [ToggleButton-Nucleo-l476.sbx](https://github.com/stm32duino/wiki/raw/master/examples/scratchx/ToggleButton-Nucleo-l476.sbx): LED state changes each time blue button is pressed.
