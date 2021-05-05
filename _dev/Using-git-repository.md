To use the [Arduino_Core_STM32](https://github.com/stm32duino/Arduino_Core_STM32) git repository instead of the package version, follow those steps:

## 1. Install the STM32 Cores package
See the [[Getting Started|Getting-Started]] page.
This will install the required dependencies for the current released version. 
To get started with development on master you must install the correct versions of the required dependencies (see: [platform.txt](https://github.com/stm32duino/Arduino_Core_STM32/blob/master/platform.txt)):
   * [CMSIS](https://www.arm.com/products/processors/cortex-m/cortex-microcontroller-software-interface-standard.php): ARM® Cortex® Microcontroller Software Interface Standard 
   * [arm-none-eabi-gcc](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm): GNU ARM Embedded Toolchain
   * [STM32Tools](https://github.com/stm32duino/Arduino_Tools): upload tools for STM32 based boards and some other useful scripts

## 2. Delete the stm32 core extracted package
Go to the installed package directory: [[Where-are-sources]]

Delete the version directory: `<x.y.z>`

Note: There must be no other directories along side the `<x.y.z>` directory, so don't just rename the old one - it will cause problems later. If you want to keep it, move it somewhere else entirely.

## 3. Hereafter, 2 methods to use git repository
Directory of step 2 is now deleted.<br>

  ### 3.1. Cloning the git repository to replace the stm32 core version package (1st method)
In the "_**\<local Arduino directory\>/packages/STMicroelectronics/hardware/stm32/**_" do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git <version>`

where _\<version\>_ is the one you delete in step 2.<br>
For this example: _**2.0.0**_<br>
So, do:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git 2.0.0`

[[/img/Tips-icon.png|alt="Tips"]] _It is possible to clone it elsewhere and create a symlink named \<version>_<br>

[[/img/Important-icon.png|alt="Important"]] _Uninstalling from the boards managers will remove the git repository!_

  ### 3.2. Adding repositories in _Arduino/hardware_ directory (2nd method)
Go to the "_**\<Arduino install directory\>/hardware/**_" and create a directory named: _**STM32**_<br>
[[/img/Warning-icon.png|alt="Warning"]] The name of the new directory to clone into must be _**STM32**_!

Go to this new directory then do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git stm32`

[[/img/Warning-icon.png|alt="Warning"]] The name of the new directory to clone into must be _**stm32**_!

[[/img/Note-icon.png|alt="Note"]] If you do not have deleted the stm32 core extracted package (step [2.](https://github.com/stm32duino/wiki/wiki/Using-git-repository/_edit#2-delete-the-stm32-core-extracted-package)), in "**Tools > Board**" menu, you will have twice the "**STM32 board**" menu.<br>