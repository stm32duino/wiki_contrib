
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
This is probably due to the missing `MSVCR100.dll`.

You can easily check that by trying to launch manually `ST-LINK_CLI.exe` which is in your Arduino install packages folder:

`STM32Tools\<x.y.z>\tools\win\stlink\`

To solve this, install  _Microsoft Visual C++ 2010 Redistributable_ to get `MSVCR100.dll`
