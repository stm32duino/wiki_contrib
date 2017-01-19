Arduino.cc IDE allows to add easily new board thanks the "**Boards Managers**".

More information available on Arduino.cc official website:

[Installing additional Arduino Cores](https://www.arduino.cc/en/guide/cores)

STM32 cores packages are provided thanks:

https://github.com/stm32duino/BoardManagerFiles

### Installing STM32 Cores

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

Select the STM32 core wanted and click on install.

[[img/boardsmanager2.png|alt="BoardsManager dialog"]]

After installation is complete an "*INSTALLED*" tag appears next to the core name. 

You can close the Board Manager.

[[img/boardslist.png|alt="Boards list"]]

Now you can find the new board in the "**Board**" menu. 

### Troubleshooting

If you have any issue to download a package, ensure to not be behind a proxy.

Else configure the proxy in the Arduino.cc IDE (open the "**Preferences**" dialog and select "**Network**" tab).