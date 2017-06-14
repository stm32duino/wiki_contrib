To use the [Arduino_Core_STM32](https://github.com/stm32duino/Arduino_Core_STM32) git repository instead of the package version, follow those steps:

## 1. Install the STM32 Cores package
See the [[Getting Started|Getting-Started]] page.
This will install the required dependencies:
   * [CMSIS](https://www.arm.com/products/processors/cortex-m/cortex-microcontroller-software-interface-standard.php): ARM® Cortex® Microcontroller Software Interface Standard 
   * [arm-none-eabi-gcc](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm): GNU ARM Embedded Toolchain
   * [STM32Tools](https://github.com/stm32duino/Arduino_Tools): upload tools,...

## 2. Delete the stm32 core extracted package
Go to the local Arduino directory<br>
    [[/img/Tips-icon.png|alt="Tips icon"]] _The location is displayed in the "**Preferences**" dialog._<br>

It should be:

* `/Users/\<USERNAME\>/Library/Arduino15/` _(Mac)_
* `c:\Documents and Settings\\<USERNAME\>\Application Data\Arduino15\` _(Windows XP)_
* `c:\Users\\<USERNAME\>\AppData\Roaming\Arduino15\` _(Windows Vista)_
* `c:\Users\\<USERNAME\>\AppData\Local\Arduino15\` _(Windows 7)_
* `~/.arduino15/` _(Linux)_

Then, go to "_**\<local Arduino directory\>/packages/STM32/hardware/stm32/**_" directory.<br> 
You should see a directory named with the STM32 Core version installed. Example: _2017.6.2_<br>
Delete this directory.

## 3. Hereafter, 2 methods to use git repository
Directory of step 2 is now deleted.<br>

  ### 3.1. Cloning the git repository to replace the stm32 core version package (1st method)
In the "_**\<local Arduino directory\>/packages/STM32/hardware/stm32/**_" do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git <version>`

where _\<version\>_ is the one you delete in step 2.<br>
For this example: _**2017.6.2**_<br>
So, do:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git 2017.6.2`

[[/img/Tips-icon.png|alt="Tips"]] _It is possible to clone it elsewhere and create a symlink named \<version>_<br>

At this step, you are able to build using the git repository but upload is broken.<br>
`.../massStorageCopy": error=2, No such file or directory`<br>
or<br>
`.../stlink_upload": error=2, No such file or directory `<br>

Uploader tools path need to be updated in _**platform.txt**_ at the root of the git repository.<br>
Replace all `{runtime.hardware.path}` by `{runtime.tools.STM32Tools.path}`<br>
That's all.<br>

[[/img/Important-icon.png|alt="Important"]] _Uninstalling from the boards managers will remove the git repository!_

  ### 3.2. Adding repositories in _Arduino/hardware_ directory (2nd method)
Go to the "_**\<Arduino install directory\>/hardware/**_" and create a directory named: _**stm**_<br>
[[/img/Note-icon.png|alt="Note"]] Directory name is not important _**stm**_ is an example.<br>

Go to this new directory then do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git stm32`

[[/img/Warning-icon.png|alt="Warning"]] The name of the new directory to clone into must be _**stm32**_!

At this step, you are able to build using the git repository but upload is broken.<br>
`.../massStorageCopy": error=2, No such file or directory`<br>
or<br>
`.../stlink_upload": error=2, No such file or directory `<br>

From the same directory clone the [Arduino_Tools](https://github.com/stm32duino/Arduino_Tools) git repository:

  `git clone https://github.com/stm32duino/Arduino_Tools.git tools`

[[/img/Warning-icon.png|alt="Warning"]] The name of the new directory to clone into must be _**tools**_!

So, you should have two directories in `\<Arduino install directory\>/hardware/stm/`: `stm32` and `tools`

[[/img/Note-icon.png|alt="Note"]] If you do not have delete the stm32 core extracted package, in "**Tools > Board**" menu, you will have twice the "**STM32 board**" menu.<br>