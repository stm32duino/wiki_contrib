# Functions reference

This document lists all the functions defined in the [`/cmake`](../blob/cmake_dev/cmake) folder in this project.
It would be a good idea to add this folder to the "CMake search path" in your project :

```cmake
list(APPEND CMAKE_MODULE_PATH ${CORE_PATH}/cmake)
```
(done by default in the [quickstart template](./Quickstart-guide#Quickstart-script).)

All the functions are defined in a CMake module of the same name. Therefore, you have to include said module before calling the function:

```cmake
include(foo)
foo()
```

(Of course, this does _not_ apply to the CMake built-in functions as described in [Introduction to CMake](./Introduction-to-CMake#CMake-language). These can be called directly.)

# Functions emulating the Arduino behavior

## build_sketch

__Syntax:__

```cmake
build_sketch(TARGET <targetName>
  SOURCES <sourcefile...>
  [DEPENDS <dependency...>]
)
```

This is the main function that encapsulates most of the automation of Arduino. It should only be called _after_ `overall_settings` and `set_board`.

- `targetName` is the name of the [binary target](https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html#binary-executables) that will be created as a result of this function; this is a handle that may be reused in later calls, to e.g., `insights()`.
- `sourcefile...` is a list of sources files to be compiled. This does not comprise header files (`.h`).
  You are strongly advised to hard-code the list of files directly in the CMakeLists.txt. Using [wildcards](https://cmake.org/cmake/help/latest/command/file.html#glob) is possible, but not guaranteed to work in all cases.
- the optional `dependencies` are targets, usually Arduino libraries such as created by `external_library()`, that the sketch depdends on.
  The CMake build model makes it awkward at best to automatically handle dependencies the way Arduino does, so they have to be specified explicitely.

What this function does is the following:

- Include the parts of Arduino_Core_STM32 needed for the project (core + right variant);
- Preprocess the sources: turn the `.ino` files to `.cpp`;
- Create the binary executable target;
- Bind the target to its dependencies (core + "DEPENDS");
- Add post-build hooks to:
  - Display the size report message ("Sketch uses xxx bytes of program storage space. Maximum is yyy bytes...";
  - Convert the binary to `.bin` and `.hex`.

## external_library

__Syntax:__

```cmake
external_library(PATH <path_to_lib>
  [DEPENDS <dependency...>]
  [FORCE]
)
```

This function is used to add a third-party library in the build description. It takes as arguments:
- the path to the library to parse;
- as with `build_sketch()`, an optional list of dependencies of the library;
- optionally, the `FORCE` keyword; read below about it.

Most third-party libraries do not ship with a CMakeLists.txt.
Therefore, one needs to be generated before that library can be used in a CMake build.
This function wraps the generation of the CMakeLists.txt and the subsequent `add_subdirectory()` to actually add the library to the build.

If no CMakeLists.txt is found, it is autogenerated by a Python script after reading `library.properties`.
The `FORCE` keyword lets you override this behavior and overwrite the CMakeLists.txt unconditionally.

In the default case, the autogenerated CMakeLists.txt will create for the library __a target with the same name as the folder name__.
You can then use this target as a dependency of another library or of your sketch.

Note: libraries built into Arduino_Core_STM32 are handled automatically; they do not need this function and can be used out-of-the-box.
Such libraries include EEPROM, Servo, SPI, Mouse, or Wire.
Libraries that are shipped with Arduino IDE (SD, Ethernet, ...) are not covered by this convenience.

## insights

__Syntax:__

```cmake
insights(TARGET <targetName>
  [DIRECT_INCLUDES]
  [TRANSITIVE_INCLUDES]
  [SYMBOLS]
  [ARCHIVES]
  [LOGIC_STRUCTURE]
)
```

This function lets you produce insights about the build process.
It uses Graphviz to generate SVG files in order to better understand what happens throughout the build: configuration, compilation, linking.
The mandatory TARGET argument is the name of the element to analyze, usually your sketch target (crated with `build_sketch()`).
Each insight keyword is optional; even when provided, they are not built by default, you have to explicitely generate them with the build tool (e.g., `ninja symbols.svg`).

| Keyword | Generated file | Description |
| :------ | :------------- | :---------- |
| DIRECT_INCLUDES | direct_includes.svg | Shows which source files include which |
| TRANSITIVE_INCLUDES | transitive_includes.svg | Shows which source files include which, both directly and indirectly (chained `#include`) |
| SYMBOLS | symbols.svg | Shows which symbol pull which other(s), at link-time |
| ARCHIVES | archives.svg | Shows which archive pull which other(s), at link-time |
| LOGIC_STRUCTURE | logicstructure.svg | Shows the targets involved in the project, and the dependencies they share. This is a wrapper around a built-in feature of CMake, read about details [here](https://cmake.org/cmake/help/latest/module/CMakeGraphVizOptions.html). |

Note: Enabling some of these graphs can hinder performances much (in the order of +50% build time).

## overall_settings
__Syntax:__

```cmake
overall_settings(
  [STANDARD_LIBC]
  [PRINTF_FLOAT]
  [SCANF_FLOAT]
  [DEBUG_SYMBOLS]
  [LTO]
  [NO_RELATIVE_MACRO]
  [UNDEF_NDEBUG]
  [CORE_CALLBACK]
  [OPTIMIZATION <optLevel>]
  [BUILD_OPT <path_to_build.opt>]
  [DISABLE_HAL_MODULES <modules...>]
)
```

This function replaces, with additions, some of the options of the menu bar of Arduino IDE.
All the keywords are optional; the default behavior is selected on fallback. The order of the keywords does not matter.

Keywords that take no argument:
- STANDARD_LIBC: switch to Newlib Standard as the runtime library, instead of Newlib Nano;
- PRINTF_FLOAT: enable `%f` in `printf` (Newlib Nano only);
- SCANF_FLOAT: enable `%f` in `scanf` (Newlib Nano only);
- DEBUG_SYMBOLS: add `-g` to GCC (for debug);
- LTO: enable Link-Time Optimizations (`-flto`);
- NO_RELATIVE_MACRO: make `__FILE__` yield absolute paths; the default is the oppisite, for size and security reasons;
- UNDEF_NDEBUG: do not define the `NDEBUG` macro; use this keyword for debug builds;
- CORE_CALLBACK: define the `CORE_CALLBACK` macro; read about use cases [here](https://github.com/stm32duino/wiki/wiki/API#core-callback).

Keywords that take a single argument:
- OPTIMIZATION: takes an optimization level (one of `0123gs`); this will then be passed to GCC's as a `-O` flag;
- BUILD_OPT: add the specified file to GCC's command line, as a `@file`. The file is usually named "build.opt", hence the keyword name. Note: with Arduino IDE, the file is taken by default into account; with CMake, it is not, only this keyword triggers this.

Keyword that takes several arguments:
- DISABLE_HAL_MODULES: lets you disable any unused HAL modules as an optimization.
  Read about it [on the wiki](https://github.com/stm32duino/wiki/wiki/HAL-configuration).
  The supported HAL modules are:
  - ADC
  - I2C
  - RTC
  - SPI
  - TIM
  - DAC
  - EXTI
  - ETH
  - SD
  - QSPI
  Disabling them all (when possible) yields a significant additional size gain.

## set_board

__Syntax:__

```cmake
set_board(<boardName>
  [SERIAL <serialSetting>]
  [USB <usbSetting>]
  [XUSB <usbSpeed>]
  [VIRTIO <virtioSetting>]
)
```

This function replaces the options of the menu bar of Arduino IDE that are related to board-specific features.
It manages to stay up-to-date with what Arduino IDE would offer by parsing `board.txt`/`platform.txt` as needed,
and caches the result in a CMake-readable database.

The first argument to this function must be the board codename, as used in boards.txt.
E.g., "GENERIC_L010RBTX", not "Generic L010RBTx" (the latter being what the IDE displays).
Then come any number of the four keywords, in any order. As with `overall_settings`, default values are used on fallback.
Depending on your board, not all features may be meaningful. Note: the values for each keyword are case-sensitive!
- SERIAL: Serial support. Usually one of `generic`, `disabled`, `none` (standing for "Enabled (no generic 'Serial')");
- USB: USB support. Usually one of `none`, `CDCgen`, `CDC`, `HID`;
- XUSB: USB speed. Usually one of `FS`, `HS`, `HSFS`;
- VIRTIO: virtIO support. Usually one of `disable`, `generic`, `enabled`.