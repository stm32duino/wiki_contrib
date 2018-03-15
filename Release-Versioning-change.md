In order to allow a better project management for planned release or quick fix the release versioning should use semantic one (https://semver.org/) instead of date.

If you have the STM32 core installed with a date version (yyyy.mm.dd) you will probably have an issue after installing the semantic one (X.Y.Z).

Example of possible issue:

`Board Disco (platform stm32, package STM32) is unknown`

`Error compiling for board Discovery.`

# Update to new versioning

## Remove the old version based on date versioning

### 1st method: using the board manager
1. Use the following link to the "*Additional Boards Managers URLs*" field of the "**Preferences**" dialog:

https://github.com/stm32duino/BoardManagerFiles/raw/oldversioning/STM32/package_stm_index.json

Click "**Ok**"

2. Click on "**Tools**" menu and then "**Boards > Boards Manager**"

Select "**Contributed**" type.

Select the "**STM32 Cores**" and click on remove.

After remove is complete the "*INSTALLED*" tag disappears next to the core name. 

You can close the Boards Manager.

### 2nd method: manually delete core and tools
1. Follow the [[Where-are-sources]] page to find the STM32 core and tools location.
2. Delete STM32 core and tools folder with a date versioning.

## Install the new version based on semantic versioning
Follow the [standard installation](https://github.com/stm32duino/wiki/wiki/Getting-Started#installing-stm32-cores) using Arduino boards manager with the standard link:

https://github.com/stm32duino/BoardManagerFiles/raw/master/STM32/package_stm_index.json

# Equivalent version
[stm32duino/Arduino_Core_STM32](https://github.com/stm32duino/Arduino_Core_STM32)

| old | new |
| --- | :---: |
| 2017.5.12 | 0.1.0 |
| 2017.6.2 | 0.1.1 |
| 2017.7.13 | 0.2.0 |
| 2017.8.4 | 0.2.1 |
| 2017.8.31 | 1.0.0 |
| 2017.9.22 | 1.0.1 |
| 2017.11.24 | 1.1.0 |
| 2018.1.18 | 1.1.1 |

[stm32duino/Arduino_Tools](https://github.com/stm32duino/Arduino_Tools)

| old | new |
| --- | :---: |
| 2017.5.12 | 0.1.0 |
| 2017.7.13 | 0.2.0 |
| 2017.8.31 | 1.0.0 |
| 2017.9.22 | 1.0.1 |