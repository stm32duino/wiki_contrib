# How to generate the pin mapping

[[/img/Warning-icon.png|alt="Warning"]] Prerequisites:
* [Python](https://www.python.org/) is required to use the script!
* [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) is required as script parses MCU xml file description provided with the tool.

Go to the '_**src/genpinmap/**_' folder of the STM32 Tools.<br>
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-tools-files-location)
or get it from [Arduino_Tools github repo](https://github.com/stm32duino/Arduino_Tools/tree/master/src/genpinmap)

**_genpinmap_arduino.py_** script allows to generate the pins mapping of an STM32 MCU.

Usage: `python genpinmap_arduino.py <Board name> <product xml file name>`<br>
* `<Board name>` is the name of the board as it will be named in variant folder<br>
* `<product xml file name>` is the STM32 file description in [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html)

The file is generated under: **_src/genpinmap/Arduino/\<Board name\>/PeripheralPins.c_**

[[/img/Warning-icon.png|alt="Warning"]]This xml file contains non alpha characters in its name, you should call it with quotes!<br>
[[/img/Warning-icon.png|alt="Warning"]] Script uses default  [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html) installation directory. If you changed it, update the installation path in the script.<br>
[[/img/Tips-icon.png|alt="Tips"]] _\<product xml file name\>_ could be find in **_\<STM32CubeMX\>/db/mcu_** folder<br>

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):

`python genpinmap_arduino.py NUCLEO_F207ZG "STM32F207Z(C-E-F-G)Tx.xml"`

will produced:
**_src/genpinmap/Arduino/NUCLEO_F207ZG/PeripheralPins.c_**<br>
