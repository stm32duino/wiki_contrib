# How to generate the pin mapping

[[/img/Warning-icon.png|alt="Warning"]] Prerequisites:
* [Python](https://www.python.org/) is required to use the script!
* [STM32CubeMX ](http://www.st.com/en/development-tools/stm32cubemx.html) is required as script parses MCU xml file description provided with the tool.

Go to the '_**src/genpinmap/**_' folder of the STM32 Tools.<br>
Follow this page: [Where are sources](https://github.com/stm32duino/wiki/wiki/Where-are-sources#stm32-tools-files-location)
or get it from [Arduino_Tools github repo](https://github.com/stm32duino/Arduino_Tools/tree/master/src/genpinmap)

**_genpinmap_arduino.py_** script allows to generate the pins mapping of an STM32 MCU.

```
genpinmap_arduino.py -h
usage: genpinmap_arduino.py [-h] [-l | -m xml]

By default, generate PeripheralPins.c and PinNamesVar.h for all xml files description available in
STM32CubeMX directory defined in 'config.json':
        $HOME/STM32CubeMX/db/mcu

optional arguments:
  -h, --help         show this help message and exit
  -l, --list         list available xml files description in STM32CubeMX
  -m xml, --mcu xml  Generate PeripheralPins.c and PinNamesVar.h for specified mcu xml file description
                     in STM32CubeMX. This xml file contains non alpha characters in
                     its name, you should call it with double quotes

After files generation, review them carefully and please report any issue to github:
        https://github.com/stm32duino/Arduino_Tools/issues

Once generated, you have to comment a line if the pin is generated several times
for the same IP or if the pin should not be used (overlaid with some HW on the board,
for instance)
```

Files are generated under: **_src/genpinmap/Arduino/<STM32 serie>\<MCU name\>/_**

[[/img/Warning-icon.png|alt="Warning"]]xml file contains non alpha characters in its name, you should call it with quotes!<br>
[[/img/Warning-icon.png|alt="Warning"]] Script uses default  [STM32CubeMX](http://www.st.com/en/development-tools/stm32cubemx.html) installation directory. If you changed it, update the installation path in the `config.json`.<br>
[[/img/Tips-icon.png|alt="Tips"]] _\<product xml file name\>_ could be find in **_\<STM32CubeMX\>/db/mcu_** folder<br>

**Example** for the [Nucleo-F207ZG](http://www.st.com/en/evaluation-tools/nucleo-f207zg.html):

`python genpinmap_arduino.py -m "STM32F207Z(C-E-F-G)Tx.xml"`

will produced:

**_src/genpinmap/Arduino/STM32F2/STM32F207Z(C-E-F-G)Tx/PeripheralPins.c_**<br>
**_src/genpinmap/Arduino/STM32F2/STM32F207Z(C-E-F-G)Tx/PinNamesVar.h_**<br>