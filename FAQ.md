
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
