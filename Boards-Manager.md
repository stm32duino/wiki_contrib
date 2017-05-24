## Boards manager concept
Arduino.cc IDE allows to add easily new board thanks the "**Boards Managers**".
More information about "**Boards Managers**" is available on Arduino.cc official website:

[Installing additional Arduino Cores](https://www.arduino.cc/en/guide/cores)

The corresponding STM32 cores packages are provided thanks to:

https://github.com/stm32duino/BoardManagerFiles

Follow the below steps to get STM32 boards installed to your Arduino IDE.

## Installing STM32 Cores

1- Launch Arduino.cc IDE. Click on "**File**" menu and then "**Preferences**".

[[img/preferences.png|alt=Preferences]]

The "**Preferences**" dialog will open, then add the following link to the "*Additional Boards Managers URLs*" field:

https://github.com/stm32duino/BoardManagerFiles/raw/master/STM32/package_stm_index.json

Click "**Ok**"

2- Click on "**Tools**" menu and then "**Boards > Boards Manager**"

[[img/menu_bm.png|alt="BoardsManager Menu"]]

The board manager will open and you will see a list of installed and available boards. 

Select "**Contributed**" type.

[[img/boardsmanager.png|alt="BoardsManager dialog"]]

Select the "**STM32 Cores**" and click on install.

[[img/boardsmanager2.png|alt="BoardsManager dialog"]]

After installation is complete an "*INSTALLED*" tag appears next to the core name. 

You can close the Board Manager.

[[img/boardslist.png|alt="Boards list"]]

Now you can find the STM32 boards package in the "**Board**" menu.

Select the desired boards series: _Nucleo-64 / Nucleo-144 / Discovery_

[[img/boardslist2.png|alt="Boards list2"]]

Then you can find the Nucleo-64 boards available in a sub-menu of the "Tools" menu.

## Troubleshooting

If you have any issue to download/use a package, you could [file an issue on Github](https://github.com/stm32duino/BoardManagerFiles/issues/new).

Or submit a topic on the [stm32duino forum](http://stm32duino.com):

 * questions on the [STM32 Core](http://stm32duino.com/viewforum.php?f=48)

 * bugs/enhancements on the [STM core: Bugs and enhancements](http://stm32duino.com/viewforum.php?f=49)

### Proxy
If you have any issue to download a package, ensure to not be behind a proxy.

Else configure the proxy in the Arduino.cc IDE (open the "**Preferences**" dialog and select "**Network**" tab).