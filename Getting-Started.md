## Install Arduino.cc IDE
Download and install [Arduino software (IDE)](https://www.arduino.cc/en/Main/Software) for the required OS.
([Windows](https://www.arduino.cc/en/Guide/Windows), [Linux](https://www.arduino.cc/en/Guide/linux) or [Mac](https://www.arduino.cc/en/Guide/MacOSX) instructions)

## Add STM32 boards support
See the [[Boards Manager|Boards-Manager]] page.

## Configuring IDE 
1. Connect a board to the computer USB port. For this example: [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)

2. Launch the Arduino software

    [[/img/arduino.png|alt="Arduino icon"]]

3. Select the [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html) board from the "**Tools > Board**" menu

  [[/img/SelectBoard.png|alt="Board selection"]]

3. Select the serial port from the "**Tools > Port**" menu

    * On Mac, it's something like _/dev/tty.usbmodem-1511_.
    * On Windows, it's often the highest-numbered COM port. In this example, it's _COM40_
    * On Linux, it's something like _/dev/ttyACM0_.

    (Or unplug the board, check the menu, and then plug the board and check what new port appears)

  [[/img/SelectPort.png|alt="Port selection"]]

### Upload method
Depending of the board, several upload method could be proposed, thanks the "**Tools > Upload Method**" menu
* Mass Storage: copy binary to the mass storage
* [STLink](http://www.st.com/en/development-tools/st-link-v2.html): use STLink to flash
* [DFU](https://en.wikipedia.org/wiki/USB#Device_Firmware_Upgrade): use USB to flash

[[/img/UploadMethod.png|alt="Upload Method"]]

## Examples
* [[Blink-example]]
* [[Firmata-example]]
