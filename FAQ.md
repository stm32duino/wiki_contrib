
### When using "Mass Storage" upload method, following error is displayed:
`NODE_xxxxxx not found. Please ensure the device is correctly connected.`

Checklist:
* Verify this is the right board selected in Arduino IDE: "**Tools -> Boards Manager**" 
* Verify if you board is correctly connected
* Verify if a mount point exists and check the mount point name. It should be the same than the one searched by the upload tool. 

If not, then probably you have an older board with a different label used for the mount point.<br>
Update the "_board.txt_" file to add <your_node_label> to the targeted board.<br>
Example:<br>
`Nucleo_64.menu.pnum.NUCLEO_xxxxxx.node=NODE_xxxxxx`<br>
becomes<br>
`Nucleo_64.menu.pnum.NUCLEO_xxxxxx.node="NODE_xxxxxx,<your_node_label>"`

Node names list has to be separated by ',' and double quoted (for Windows).

### When using "STLink" upload method on Windows, nothing is happening:

[[/img/Warning-icon.png|alt="Warning"]] _**deprecated since core version > 1.5.0**_

This is probably due to the missing `MSVCR100.dll`.

You can easily check that by trying to launch manually `ST-LINK_CLI.exe` which is in your Arduino install packages folder:

`STM32Tools\<x.y.z>\tools\win\stlink\`

To solve this, install  _Microsoft Visual C++ 2010 Redistributable_ to get `MSVCR100.dll`



## OS specific
### Linux

#### USB serial stalls initially and connecting using a serial monitor fails

problem:
in some Linux distributions. usb (cdc) serial initially stalls could be into the 10s of seconds after a reset. There is no response in the serial monitor (e.g. putty), in fact the serial monitor (e.g. putty) simply won't connect. running _dmesg_ command did show a /dev/ttyACMx device.

discussion and solution:
create a udev rules file e.g.
/etc/udev/rules.d/45-stm32duino.rules
add a line like
```
ATTRS{idProduct}=="5740", ATTRS{idVendor}=="0483", MODE="664", GROUP="plugdev" SYMLINK+="stm32duino" ENV{ID_MM_DEVICE_IGNORE}="1"
```
make sure that the product id and vendor id matches that used in your sketch.

the main thing is that 
``
ENV{ID_MM_DEVICE_IGNORE}="1"
``
which tells udev not to treat it as a modem
that issue is explored in this thread
https://www.stm32duino.com/viewtopic.php?f=62&t=1000
