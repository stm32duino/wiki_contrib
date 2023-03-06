To use the [Arduino_Core_STM32](../) git repository instead of the package version, follow those steps:

## 1. Install the STM32 Cores package

To get started with development on `main` branch, correct versions of the required dependencies have to be installed (see: [platform.txt](../blob/main/platform.txt)):
   * [CMSIS](https://www.arm.com/products/processors/cortex-m/cortex-microcontroller-software-interface-standard.php): ARM® Cortex® Microcontroller Software Interface Standard 
   * [GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm): Arm Embedded GCC compiler, libraries and other GNU tools necessary for bare-metal software development on devices based on the Arm Cortex-M. Packages are provided thanks [The xPack GNU Arm Embedded GCC](https://xpack.github.io/arm-none-eabi-gcc/): https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack
   * [STM32Tools](https://github.com/stm32duino/Arduino_Tools): upload tools for STM32 based boards and some other useful scripts

Using the git repository requires sometimes to update tools dependencies.

Example when the arm-none-abi-gcc toolchain or the CMSIS version are updated. In that case, all dependencies are available in the [package_stmicroelectronics_index.json](https://github.com/stm32duino/BoardManagerFiles/blob/dev/package_stmicroelectronics_index.json) of the BoardManagerFiles `dev` branch. 

See the [[Getting Started]] page to see how to install the core and its tools dependencies but use this link in the "Additional Boards Managers URLs" field:

https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/dev/package_stmicroelectronics_index.json

Then install the latest version displayed by the board manager, if a version is suffixed by `-dev` it means one or more dependencies have been updated else no change done since the last release.

This will install the required dependencies for the main branch.

## 2. Delete the stm32 core extracted package
Go to the installed package directory: [[Where-are-sources]]

Delete the version directory: `<x.y.z>` or `<x.y.z-dev>`

Note: There must be no other directories along side the `<x.y.z>` or `<x.y.z-dev>` directory, so don't just rename the old one - it will cause problems later. If you want to keep it, move it somewhere else entirely.

## 3. Cloning the git repository to replace the stm32 core version package (1st method)

Directory of step 2 is now deleted.<br>

In the "_**\<local Arduino directory\>/packages/STMicroelectronics/hardware/stm32/**_" do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git <version>`

where _\<version\>_ is the one you delete in step [2.](#2-delete-the-stm32-core-extracted-package)<br>
For this example: _**2.0.0**_<br>
So, do:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git 2.0.0`

[[/img/Tips-icon.png|alt="Tips"]] _On Linux, It is possible to clone it elsewhere and create a symlink named \<version>_<br>

[[/img/Important-icon.png|alt="Important"]] _Uninstalling from the boards managers will remove the git repository!_

[[/img/Note-icon.png|alt="Note"]] If you do not have deleted the stm32 core extracted package (step [2.](#2-delete-the-stm32-core-extracted-package)), in "**Tools > Board**" menu, you will have twice the "**STM32 board**" menu.<br>