## Install Arduino.cc IDE
Download and install [Arduino software (IDE)](https://www.arduino.cc/en/Main/Software) for the required OS.
([Windows](https://www.arduino.cc/en/Guide/Windows), [Linux](https://www.arduino.cc/en/Guide/linux) or [Mac](https://www.arduino.cc/en/Guide/MacOSX) instructions)

## Add STM32 boards support
See the [[Boards Manager|Boards-Manager]] page.

## My first run

### Blink example on [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)
1. If not already done, download and install the [Arduino software (IDE)](https://www.arduino.cc/en/Main/Software) for the required OS.
([Windows](https://www.arduino.cc/en/Guide/Windows), [Linux](https://www.arduino.cc/en/Guide/linux) or [Mac](https://www.arduino.cc/en/Guide/MacOSX) instructions)

2. Connect the board to your computer's USB port. For this example: [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)

3. Launch the Arduino software

    [[/img/arduino.png|alt="Arduino icon"]]

4. Select the [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html) board from the "**Tools > Board**" menu
[[/img/SelectBoard.png|alt="Board selection"]]

5. Select the serial port from the "**Tools > Port**" menu

    * On Mac, it's something like _/dev/tty.usbmodem-1511_.
    * On Windows, it's often the highest-numbered COM port. In this example, it's _COM40_
    * On Linux, it's something like _/dev/ttyACM0_.

    (Or unplug the Arduino, check the menu, and then replug the board and see what new port appears.)
[[/img/SelectPort.png|alt="Port selection"]]

6. Open the Blink sketch from the "**File> Examples > 01.Basics > Blink**"
[[/img/SelectBlinkExample.png|alt="Blink example selection"]]

7. Click the upload button
[[/img/Upload.png|alt="Upload"]]

That's all. LED should blink on the [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)
