# Install Arduino.cc IDE
Download and install [Arduino software (IDE)](https://www.arduino.cc/en/Main/Software) for the required OS.
([Windows](https://www.arduino.cc/en/Guide/Windows), [Linux](https://www.arduino.cc/en/Guide/linux) or [Mac](https://www.arduino.cc/en/Guide/MacOSX) instructions)

## About Boards manager concept
Arduino.cc IDE allows to add easily new board thanks the "**Boards Managers**".
More information about "**Boards Managers**" is available on Arduino.cc official website:

[Installing additional Arduino Cores](https://www.arduino.cc/en/guide/cores)

The corresponding STM32 cores packages are provided thanks to:

https://github.com/stm32duino/BoardManagerFiles

Follow the below steps to get STM32 boards installed to your Arduino IDE.

# Add STM32 boards support to Arduino
This is the needed step to get STM32 targets added to Arduino.
So carefully follow the following steps.

## Installing STM32 Cores

1- Launch Arduino.cc IDE. Click on "**File**" menu and then "**Preferences**".

[[img/preferences.png|alt=Preferences]]

The "**Preferences**" dialog will open, then add the following link to the "*Additional Boards Managers URLs*" field:

https://github.com/stm32duino/BoardManagerFiles/raw/master/package_stmicroelectronics_index.json

[[/img/Important-icon.png|alt="Important"]] **Important note: Since core 2.0.0, the below link is deprecated**

_https://github.com/stm32duino/BoardManagerFiles/raw/master/STM32/package_stm_index.json_

Click "**Ok**"

2- Click on "**Tools**" menu and then "**Boards > Boards Manager**"

[[img/menu_bm.png|alt="BoardsManager Menu"]]

The board manager will open and you will see a list of installed and available boards. 

Select "**Contributed**" type.

[[img/boardsmanager.png|alt="BoardsManager dialog"]]

Select the "**STM32 MCU based boards**" and click on install.

[[img/boardsmanager2.png|alt="BoardsManager dialog"]]

After installation is complete an "*INSTALLED*" tag appears next to the core name. 

You can close the Board Manager.

[[img/boardslist.png|alt="Boards list"]]

Now you can find the STM32 boards package in the "**Board**" menu.

Select the desired boards series: _Nucleo-64 / Nucleo-144 / Discovery_

[[img/SelectBoard.png|alt="Select boards"]]

Then you can find the Nucleo-64 boards available in a sub-menu of the "Tools" menu.

## Extra step

To upload through SWD (STLink), Serial or DFU, [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html) needs to be installed. See [Upload methods](https://github.com/stm32duino/wiki/wiki/Upload-methods#stm32cubeprogrammer).

## Troubleshooting

If you have any issue to download/use a package, you could [file an issue on Github](https://github.com/stm32duino/BoardManagerFiles/issues/new).

### Proxy
If you have any issue to download a package, ensure to not be behind a proxy.

Else configure the proxy in the Arduino.cc IDE (open the "**Preferences**" dialog and select "**Network**" tab).

# Configuring IDE 
1. Connect a board to the computer USB port. For this example: [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)

2. Launch the Arduino software

    [[/img/arduino.png|alt="Arduino icon"]]

3. Select the [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html) board in two steps:

a. From the "**Tools > Board**" menu, select the STM32 board series: _Nucleo-64_

  [[/img/boardslist.png|alt="Board selection"]]

b. Then from the "**Tools > Nucleo 64 boards**" menu, select the [Nucleo L476RG](http://www.st.com/en/evaluation-tools/nucleo-l476rg.html)

  [[/img/SelectBoard.png|alt="Board selection"]]

3. Select the serial port from the "**Tools > Port**" menu

    * On Mac, it's something like _/dev/tty.usbmodem-1511_.
    * On Windows, it's often the highest-numbered COM port. In this example, it's _COM5_
    * On Linux, it's something like _/dev/ttyACM0_.

    (Or unplug the board, check the menu, and then plug the board and check what new port appears)

  [[/img/SelectPort.png|alt="Port selection"]]

## Upload methods
Depending of the board, several upload methods could be proposed, thanks the "**Tools > Upload Method**" menu.

See [Upload methods](https://github.com/stm32duino/wiki/wiki/Upload-methods) for more details.

[[/img/UploadMethod.png|alt="Upload Method"]]

# Examples
* [[Blink-example]]
* [[Firmata-example]] (to use with [ScratchX](http://scratchx.org/) for example)
