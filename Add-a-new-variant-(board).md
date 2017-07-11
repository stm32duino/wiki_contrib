[[/img/under-construction.jpg|alt="under construction"]]

# Create a new variant
Go to the '_**variant**_' folder of the STM32 core.<br>
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-core-sources-files-location)

## 1- Create a copy of the _**stm32/variants/board_template**_ folder with a name of your choice.

**Example**: To add variant for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html)

`cp -a board_template NUCLEO_F207ZG` (_linux_)

[[/img/Tips-icon.png|alt="Tips"]]It's also possible to copy one of the most similar board variant<br>

## 2- Generate the pin mapping

[[/img/Warning-icon.png|alt="Warning"]] Prerequisites:
* [Python](https://www.python.org/) is required to use the script!
* [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) is required as script parses MCU xml file description provided with the tool.

Go to the '_**src/genpinmap/**_' folder of the STM32 Tools.<br>
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-tools-files-location)
or get it from [Arduino_Tools github repo](https://github.com/stm32duino/Arduino_Tools/tree/master/src/genpinmap)

**_genpinmap_arduino.py_** script allows to generate the pins mapping of an STM32 MCU.

> USAGE: genpinmap_arduino.py _\<BOARD_NAME\> \<product xml file name\>_<br>
>        _\<BOARD_NAME\>_ is the name of the board as it will be named in variant folder<br>
>        _\<product xml file name\>_ is the STM32 file description in [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html)

[[/img/Warning-icon.png|alt="Warning"]]This xml file contains non alpha characters in its name, you should call it with quotes!<br>
[[/img/Warning-icon.png|alt="Warning"]] Script uses default  [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html) installation directory. If you changed it, update the installation path in the script.<br>
[[/img/Tips-icon.png|alt="Tips"]] _\<product xml file name\>_ could be find in **_\<STM32CubeMX\>/db/mcu_** folder<br>

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):

`python genpinmap_arduino.py NUCLEO_F207ZG "STM32F207Z(C-E-F-G)Tx.xml"`

Copy the generated **_src/genpinmap/Arduino/\<BOARD_NAME\>/PeripheralPins.c_** file in the variant folder created.

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):

copy **_src/genpinmap/Arduino/NUCLEO_F207ZG/PeripheralPins.c_** to  **_variant/NUCLEO_F207ZG/_**

## 3- Review pins mapping
 
Use the related user manual to define the best pins mapping:<br>
**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):<br>
[UM1974: STM32 Nucleo-144 boards](http://www.st.com/resource/en/user_manual/dm00244518.pdf)<br>
    
[[/img/Tips-icon.png|alt="Tips"]] It is also possible to check the equivalent file for mbed os:
    [ST-Nucleo-F207ZG](https://developer.mbed.org/platforms/ST-Nucleo-F207ZG/)

