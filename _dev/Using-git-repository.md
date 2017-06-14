[[/img/under-construction.jpg|alt="under construction"]]

To use the [Arduino_Core_STM32](https://github.com/stm32duino/Arduino_Core_STM32) git repository instead of the package version, follow those steps:

## 1. Install the STM32 Cores package, see the [[Getting Started|Getting-Started]] page.
This will install the required dependencies:
   * [CMSIS](https://www.arm.com/products/processors/cortex-m/cortex-microcontroller-software-interface-standard.php): ARM® Cortex® Microcontroller Software Interface Standard 
   * [arm-none-eabi-gcc](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm): GNU ARM Embedded Toolchain
   * [STM32Tools](https://github.com/stm32duino/Arduino_Tools): upload tools,...

## 2. Delete the stm32 core extracted package.
Go to the local Arduino directory<br>
    [[/img/Tips-icon.png|alt="Tips icon"]] _The location is displayed in the "**Preferences**" dialog._<br>
It should be:

    * `/Users/\<USERNAME\>/Library/Arduino15/` _(Mac)_
    * `c:\Documents and Settings\\<USERNAME\>\Application Data\Arduino15\` _(Windows XP)_
    * `c:\Users\\<USERNAME\>\AppData\Roaming\Arduino15\` _(Windows Vista)_
    * `c:\Users\\<USERNAME\>\AppData\Local\Arduino15\` _(Windows 7)_
    * `~/.arduino15/` _(Linux)_

Then, go to "**<local Arduino directory>/packages/STM32/hardware/stm32/**" directory.<br> 
You should see a directory named with the STM32 Core version installed. Example: _2017.6.2_<br>
Delete this directory.

## 3. Hereafter, 2 methods to use git repository:
Directory of step 2 is now deleted.<br>

  ### 3.1. Cloning the git repository to replace the stm32 core version package (1st method)
In the "**<local Arduino directory>/packages/STM32/hardware/stm32/**" do the clone:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git <version>`

where _\<version\>_ is the one you delete in step 2.<br>
For this example: _2017.6.2_<br>
So, do:<br>

  `git clone https://github.com/stm32duino/Arduino_Core_STM32.git 2017.6.2`

[[/img/Tips-icon.png|alt="Tips icon"]] _It is possible to clone it elsewhere and create a symlink named \<version>_<br>

At this step, you are able to build using the git repository but upload is broken.<br>
`.../massStorageCopy": error=2, No such file or directory`<br>
or<br>
`.../stlink_upload": error=2, No such file or directory `<br>

Uploader tools path need to be updated in **platform.txt** at the root of the git repository.<br>
Replace all `{runtime.hardware.path}` by `{runtime.tools.STM32Tools.path}`<br>
That's all.<br>

[[/img/Warning_icon.png|alt="Warning icon"]] _Uninstalling from the boards managers will remove the git repository!_

  ### 3.2. Adding repositories in _Arduino/hardware_ directory (2nd method)
