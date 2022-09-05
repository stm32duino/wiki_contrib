Welcome to the CMake port of Arduino_Core_STM32!

--------------------------

[[/img/Important-icon.png]] Warning: work-in-progress!
================

The tool described in this section is currently subject to a pull request [PR #1776](https://github.com/stm32duino/Arduino_Core_STM32/pull/1776).
Until it is merged, consider using the fork repo at [massonal/Arduino_Core_STM32](https://github.com/massonal/Arduino_Core_STM32).

--------------------------

The goal of this tool is to let users build Arduino sketches for STM32 boards, without using neither Arduino IDE nor `arduino-cli`.
Advantages of this approach include:
- faster build time (about -50%, tested on Windows 10 and Ubuntu20.04);
- flexibility: CMake has a full language centered around build description;
- integration with IDEs: CMake integrates with most recent IDEs, easing the work of those who code outside of Arduino IDE;
- better support of incremental compilation;
- overstepping limits set by Arduino: sketch filename, library selection...

Of course, this all has a cost: building is no longer as simple as hitting "build" in Arduino IDE; there is a CMake file to write and maintain.
However, much has been done to make the file as high-level as possible: it is written in CMake's own syntax, but makes heavy use of the custom functions defined here in the [`cmake/` folder](../blob/cmake_dev/cmake).
Didactic examples can be found on a separate repository: [https://github.com/stm32duino/CMake_workspace](https://github.com/stm32duino/CMake_workspace).

Before delving into this wiki, be sure to read [the dedicated README](https://github.com/massonal/Arduino_Core_STM32/blob/cmake_dev/README_CMAKE.md) first!


## Pages in this section:
- [[Setup]]
- [[Quickstart guide]]
- [[Introduction to CMake]]
- [[Functions reference]]
- [[Arduino (in)compatibility]]
- [[Advanced usage]]
- [[cubeIDE]]
