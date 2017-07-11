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
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-tools-files-location)<br>
or get it from [Arduino_Tools github repo](https://github.com/stm32duino/Arduino_Tools/tree/master/src/genpinmap)


