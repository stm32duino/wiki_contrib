# Using Eclipse and Sloeber
## 1 - Software requirements
### 1.1 - Install Eclipse C/C++ IDE
+	**If you do not have any Eclipse package installed** <br>
Download Eclipse installer from [Eclipse website](http://eclipse.org/downloads) , choose _**Eclipse IDE for C/C++ Developers**_ and follow the installer instructions . 

+ **If you already have an Eclipse packages (Java, Java EE, …) on your system** <br>
You can install the CDT (C/C++ Development Tooling ) plugin as follow :
 1. Launch _**"Eclipse > Help > Install New Software".**_<br>
 2.  In the _“**Work with**”_ section, choose: Oxygen - http://download.eclipse.org/releases/oxygen (depending on your Eclipse packages version).
 3.  In the _“**Name**”_ box, expand _“**Programming Language**”_ and choose _**“C/C+ Development Tools > Next > Finish”**_.<br>

**1.1.1.	Install OpenOCD from the GNU MCU Eclipse plug-ins** 

The GNU MCU Eclipse plug-ins provide multiple tools based on the GNU toolchains to ease project development. To use Eclipse debugging features, it is necessary to download OpenOCD, an open source software that provides debugging and in-system programming for embedded device.

Launch Eclipse, go to _**“Help > Eclipse Marketplace”**_ and search for the _**"GNU MCU plug-in"**_. <br>

[[/img/EclipseMP.png|alt="EclipseMarketPlace"]]

In the tree view, expand _**“GNU MCU Eclipse {version}”**_ and uncheck all items expect _**“GNU MCU C/C++ OpenOCD Debugging”**_, confirm and follow the recommended instructions. Then restart Eclipse.<br>

[[/img/EclipseMPGNU.png|alt="EclipseMarketPlaceGNU"]]

To finish the OpenOCD plug-in configuration, and for a simpler integration, install OpenOCD binaries by following the [“How to install the OpenOCD binaries”](https://gnu-mcu-eclipse.github.io/openocd/install/ 
) tutorial.

###  1.2 - Install Sloeber (The Arduino Eclipse Plugin) 
From the Eclipse main tab, go to _**“Help > Eclipse Marketplace”**_ and search for _**Sloeber**_. <br>
Download the _**"Sloeber plugin"**_ , follow the recommended instructions and restart Eclipse. <br>
By now, the main tab should look like the following:
[[/img/SloeberMenu.png|alt="SloeberMenu"]]

### 1.3 - Install STM32 Cores
Open _**“Arduino > Preferences”**_.<br>
In the tree view that pops up, go to _**“Arduino > Third party index url’s”**_ and add the STM32 support package URL:

https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/master/STM32/package_stm_index.json

[[/img/UrlIndex.png|alt="UrlIndex"]]

Hit _**“Apply and Close”**_ then re-open the _**“Arduino > Preferences”**_ menu. The STM32 Core is now available in the _**“Platforms and Boards”**_ menu.

[[/img/CoreInstall.png|alt="CoreInstall"]]

Select the latest core version and hit _**“Apply and Close”**_.

## 2 - Programming the boards
[[/img/Important-icon.png|alt="ImportantIcon"]]
Arduino build recipe hooks are currently not supported by Sloeber (See GitHub issue [#927](https://github.com/Sloeber/arduino-eclipse-plugin/issues/927)), leading to some build issues. In order to avoid this, and before starting a new project, some configurations needs to be done. Open your STM32 core package folder; it might be in your Eclipse installation folder. The path should look like this one:
 
```
<Eclipse installation path>\eclipse\arduinoPlugin\packages\STM32\hardware\stm32\<core version>. 
```

In this folder, open the _**platform.txt**_ file and follow **carefully** these steps   : 
-	Find the: _**“compiler.extra_flags=-mcpu={build.mcu} -mthumb @{build.opt.path}”**_ line.
-	Delete the _**“ @{build.opt.path} “**_ part.
-	Save your modification.
-	Relaunch Eclipse. 

Otherwise, you can also get around these issues by using the [Sloeber nightly version](http://eclipse.baeyens.it/nightly.php) : open _**"Help > Check for updates"**_ and follow the recommended instructions. 

Once the update is completed, relaunch Eclipse then open your project properties and go to _**"C/C++ Build > Settings"**_. In the _**Pre-build steps**_ section, fill the **_"Command"_** field with **_"${A.RECIPE.HOOKS.PREBUILD.1.PATTERN}"_**

[[/img/Note-icon.png|alt="Note"]] Do not forget to do these steps after each core update

Now, let's create our first project . 

[[/img/Tips-icon.png|alt="Tips"]] Make sure your board is correctly connected before go any further.

There is multiple options to start a new project. 

--> _**Option A:**_ From the _**“Arduino“**_ menu, click on _**“New Sketch”**_. <br>
--> _**Option B:**_ Click on the new sketch icon directly from the toolbar.<br>
--> _**Option C:**_ From the _**“File > New > Project…”**_ click on _**“Arduino New Sketch”**_.

Regardless of the chosen method, set your _**“Project name”**_ and the _**“Location”**_ of your project. Then, push the _**“Next”**_ button.
Complete the Arduino required information (board type, port number …) form and click _**“Next”**_.

Do not forget to select the _**“Platform folder”**_ that corresponding to the STM32 Core version previously installed.

[[/img/ProjectConfig.png|alt="ProjectConfig"]] 

[[/img/Note-icon.png|alt="Note"]] If you plan to debug, select "_**Debug (-g)**_" from the "_**Optimize**_" list else you will not have debugging symbols.

From there, you can create your own sketch or use pre-configured examples. <br>
In this case, we will try the _**“Blink”**_ example.<br>
From the _**“select code”**_ bar, apply _**“Sample sketch”**_ and then choose _**“Examples > 01.Basics > Blink”**_ and _**“Finish”**_.

[[/img/BuiltInExamples.png|alt="BuiltInExamples"]] 

[[/img/Note-icon.png|alt="Note"]] As the GCC ARM Toolchain is provided by the STM32 core, you do not have to download it in order to program your board.

Use the _**“Arduino”**_ menu or the upload button on the toolbar to upload your sketch. If the setup is correct, the LED should blink on your board.

## 3 - Debugging Arduino Code

First, make sure your board can work with STLink. The debugger support is currently fully tested with the board supported by the STM32Core (Full list on [boards available section](https://github.com/stm32duino/Arduino_Core_STM32#boards-available)). 

### 3.1 Software requirements

Two standard tools are required in order to debug the code: 
+  **GDB, the GNU Debugger**. The STM32 core provides a GDB executable. This executable is located in the arm-none-eabi-gcc binaires folder in your STM32 core package. The path should look like this one: 

```
<Eclipse installation path>\eclipse\arduinoPlugin\packages\STM32\tools\arm-none-eabi-gcc\6-2017-q2-update\bin\arm-none-eabi-gdb.exe
```
+  **OpenOCD**, installed in 1.1.1 section.

[[/img/Important-icon.png|alt="ImportantIcon"]] Make sure these tools are correctly installed on your platform before proceeding any further.

[[/img/Important-icon.png|alt="ImportantIcon"]] Do not forget to select "_**Debug (-g)**_" to the "_**Optimize**_" list in the "_**Arduino Board Selection**_" of your project else you will not have debugging symbols.

### 3.2 Setting up debug configuration 

From the _**“Run”**_ menu, select _**“Debug Configurations”**_.
Double-click on **_“GDB OpenOCD Debugging”_** to create a new configuration and set the configuration name.

[[/img/DebugMenu.png|alt="DebugMenu"]]

Move to the _**“Debugger”**_ tab in order to configure OpenOCD and GDB. 

#### 3.2.1 Setting up OpenOCD

1. First, set the OpenOCD executable path. If OpenOCD was installed following the recommended instructions from the GNU MCU plug-in installation guide _(see section 1.1.1)_, Eclipse should auto detect the latest version of OpenOCD and you should be able to use global variable to define your path. Your  executable path should look like this one : 
```
        ${openocd_path}/${openocd_executable}
```

The _**“Actual executable”**_ field show the full executable path. 

2. Set the _**“GDB port”**_ to 3333 , the _**“Telnet port”**_ to 4444 and the _**“Tcl port”**_ to 6666.

3. Finally, set the debugger configuration in the _**“Config options”**_ field; specify the script path folder and configuration files (.cfg) related to your MCU. In this case, we use a Nucleo F030R8, so the configuration arguments are : 
```
        -s "${openocd_path}/../scripts" -f interface/stlink-v2-1.cfg -f target/stm32f0x.cfg
```

[[/img/OCDConfig.png|alt="OpenOCD-config"]]

[[/img/Important-icon.png|alt="ImportantIcon"]] Do not forget to replace the config files with the version of the board you are using.

#### 3.2.1 Setting up GDB

In the _**“Debugger”**_ tab, scroll to the GDB Client setup field. 
 * Set the _**“Executable name”**_ field to the path of the arm-none-eabi-gdb executable by adding:
```
         ${A.COMPILER.PATH}/arm-none-eabi-gdb
```

By now, the _**“Debugger”**_ tab should look like the following: 

[[/img/DebugConfig.png|alt="DebugConfig"]]

Move to the _**“Startup”**_ tab, scroll until the _**“Run/Restart Commands”**_ fields and add:<br> 
``` 
         monitor reset halt
         monitor reset init
```

Then go to the _**“Common”**_ tab and check _**“Debug”**_ and _**“Run”**_ in the _**“Display in favorites menu”**_.
Finally, click on _**“Apply”**_ and _**“Close”**_. 

### 3.3 Launching a debug session

Launch the debug session from the _**“Debug”**_ or _**“Run”**_ button in the toolbar.<br>
If the configuration process runs correctly, you will be able to see the debug capabilities of the chip in the Debug console (number of breakpoints, watchpoints, …).

[[/img/DebugConsole.png|alt="DebugConsole"]]

Now, you can easily debug your code by using the Eclipse debug features including running step-by-step mode, live breakpoint, inspecting memory access, live view of variable contents and many more.

[[/img/DebugView.png|alt="DebugView"]]