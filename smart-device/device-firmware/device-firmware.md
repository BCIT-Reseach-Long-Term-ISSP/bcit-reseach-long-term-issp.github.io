---
layout: default
title: Device Firmware
has_children: true
permalink: /docs/firmware
parent: Smart Device
has_toc: true
nav_order: 1
---

# Device Firmware

The firmware for the smart device is written in Bare-metal C using CMake for its build system and runs on the Arduino Zero board. Cross-platform directions on how to set up the toolchain can be found under [Getting Set-Up](#getting-set-up).

## How the code is built

This project uses CMake for building the firmware. Once the tool chain has been successfully set up, Visual Studio Code will automatically discover the CMakeLists.txt file within the firmware directory. Building of the firmware is done in several steps. Firstly, the configure stage is run by [CMake](https://cmake.org/) to generate the build scripts. These are placed within a "build" directory inside of firmware. Secondly, Visual Studio Code calls [Ninja](https://ninja-build.org/) to run the build scripts. In the build script, a device image is built using GCC, then flashed to the board using OpenOCD. Once flashed, OpenOCD runs a GDB Server which uses the built files in conjunction with the live device to provide utilities such as single stepping or viewing memory.

![Build Steps](/docs/assets/buildsteps.svg)

# Getting Set-Up

Getting started with the code is done in three steps:
 - Cloning the Repository
 - Installing the toolchain
 - Setting up your IDE

Detailed instructions for each are provided below:

## Cloning the repository

To get started, you first need to clone the code repository. The git repository is located at <https://github.com/BCIT-Reseach-Long-Term-ISSP/device-firmware> and includes git submodules. When cloning this repository *make sure* to also download the submodules. This can be done through the command line by adding the argument `--recursive` when cloning:

`git clone --recursive git@github.com:BCIT-Reseach-Long-Term-ISSP/device-firmware.git`

The above command clones through SSH, which allows you to push changes back to github.

## Installing the toolchain

Next up, you need to set up your toolchain. There are several programs which need to be installed and accessible on your `PATH` in order to build, flash, and debug the code. The programs are as follows:
- [Cmake](https://cmake.org/download/)
- [Ninja Build](https://ninja-build.org/)
- [ARM GNU toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
- [openocd](https://openocd.org/pages/getting-openocd.html)

Instructions on how to set things up on most major operating systems are provided below:

### Microsoft Windows
On Windows, these packages are accessible using a single "toolchain.zip" package [on the Google Drive](https://drive.google.com/file/d/1bYFQPA6Cd6zoyujSbzcGzjMOZFkS-vox/view?usp=sharing). Once downloaded, the "bin" directory should be put on your PATH variable. This can be done either within your IDE or on a system-wide basis.

> **_WARNING:_** This toolchain does not automaticlly update. As such, this toolchain may contain older verisons of the required software. This should not cause any major problems, but may require the use of older versions of extensions and other tools. For example, the Visual Studio Code extensions may need to be reverted to an older version.


### MacOS
On MacOS, all of these programs are available through `brew`:
```
brew install --cask gcc-arm-embedded
brew install cmake
brew install ninja
brew install open-ocd
```

### Linux
On Linux, most distros have all of these packages available through your package manager.

For Debian/Ubuntu/etc:
```
sudo apt install gcc-arm-none-eabi binutils-arm-none-eabi openocd cmake ninja-build
```

For Arch-Based Systems:
```
sudo pacman -Syu arm-none-eabi-gcc arm-none-eabi-binutils openocd cmake ninja
```

For other Linux distributions, these packages should be named similarily.

## Setting up your IDE

Finally, your IDE must be set up to use the toolchain. This is typically done through extensions. Specific instructions for certain editors are included below:

### Visual Studio Code
To set-up the toolchain for visual studio code, follow these steps:

- Install Visual Studio Code
- Open up Visual Studio Code and under the "Extensions" tab install "C/C++ Extension Pack" and "Cortex-Debug"
> **_Warning:_** If you used the Windows Toolchain, you must revert the Cortex-Debug VS Code extension to Version 1.4.4. If you do not revert to this version, the debugger will fail.
- Under the "Explorer" tab, click on "Open Folder" and navigate to the downloaded repo
- Click on "Yes, I Trust the authors"
> **_Note:_** Ensure you have the Arduino connected or else the build will fail.
- Press "f7" to do an inital build. It will ask which kit to use, select "[Unspecified]"

### CLion
*TODO:* CLion Instructions

# Digging into the code

Following are some notes on how the code is developed.

## Source Code Structure

The code has the following structure:

| Path     | Description
|---|---|
| .vscode  | Visual Studio Code Project Settings     |
| Prototypes | Arduino IDE prototypes |
| Config   | Configuration for third-party libraries |
| cmake    | Cmake Helper Scripts                    |
| contrib  | Third-party libraries                   |
| src      | Source code                             |
| src/watermonitor.c | Program entry-point           |
| src/comm | AWS Communications                      |
| src/comm/lora | LoRaWAN-specific communications    |
| src/comm/nb-iot | NB-IoT-specific communications   |
| src/hal  | Hardware Abstraction Layer              |
| src/sensor | Sensor Formatting Code                | 
| startup    | Low-Level board startup               |
| CMakeLists.txt | Base CMake build file             |

## Third-Party Libraries

The firmware relies on several third-party libraries. Some are included directly within the source, and some others are included as git submodules. In `contrib/CMakeLists.txt` the source files and include directories of these libraries are specified. See [Adding New Source Files and Include Paths to the Build](#adding-new-source-files-and-include-paths-to-the-build) for more information on this.

|Path     | Description
|---|---|
| contrib/arduino-lmic | LMIC Library for LoraWAN |
| contrib/backoffAlgorithm | Backoff Algorithm for NB-IoT |
| contrib/cellular | FreeRTOS Cellular library for NB-IoT |
| contrib/CMSIS | *Common Microcontroller Software Interface Standard*: ARM General |
| contrib/CMSIS-Atmel | *Common Microcontroller Software Interface Standard*: Atmel-Specific |
| contrib/coreMQTT | MQTT Library |
| contrib/FreeRTOS | FreeRTOS (See [FreeRTOS](#freertos))|
| contrib/pcg_basic | PCG Random Number Generator |

## FreeRTOS

The firmware for this project is based around [FreeRTOS](https://freertos.org/). In main, board initialization functions are called (see startup directory) then FreeRTOS is launched with a startup task. It is within this task that the bulk of the program is run. Within this task, all FreeRTOS features are supported such as memory allocation, multitasking, buffers and more. Run-time information about FreeRTOS can also be found while debugging through the Cortex-Debug extension for VSCode. For more information on Available FreeRTOS APIs, see [https://freertos.org/features.html](https://freertos.org/features.html)

## HAL Development

Within the "src" directory is a "hal" directory which contains low-level drivers for smart sensors and hardware interfaces. The code within this directory interfaces with the SAMD21 peripherals directly through registers. Detailed explanations of how to use these peripherals through the registers can be found in the SAMD21 [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/SAM-D21DA1-Family-Data-Sheet-DS40001882G.pdf). 

By including the file "sam.h" within your code, you can also gain access to the CMSIS headers which makes these registers easier to access and control. You can look through some of the HAL code that is already made to get acquainted on how to use these.

## Adding New Source files and include paths to the build

A common operation is the creation of new C files and directories in the source tree. After making these you need to tell CMake where they are. There are two aspects which are in play here, _Include directories_ and _source files_. _Include directories_ are directories where the C compiler will search for header files whenever you use `#include "..."`. Generally whenever you create a new source directory you add it as an include directory. _Source Files_ are the ".c" files which the C compiler will directly process. Note the distinction between _Header Files_ and _Source Files_, ".h" files are not source files!!!

When making an executable, CMake takes a list of source files to build and assigns them to a target. Include directories can then be attached to that target. In this project we build everything into a single target called "ema_yvr_comm.elf", so we need to supply our list of source files all at once. This is done through CMake variables.

A CMake variable is created using the [set()](https://cmake.org/cmake/help/latest/command/set.html) function within "CMakeLists.txt" files. The main task of the CMakeLists.txt files through the project is to eventually build a `SRCS` variable to be passed into [add_executable()](https://cmake.org/cmake/help/latest/command/add_executable.html). This is done through a cascade, where various CMakeLists.txt files defining parts of the `SRCS` variable throughout the project are included from the root using [add_subdirectory()](https://cmake.org/cmake/help/latest/command/add_subdirectory.html). To make variables defined in these sub-files available to the file above, calls to _set()_ must have the `PARENT_SCOPE` parameter included at the end before the last bracket, otherwise they will not be accessible. Once these variables are passed to the parent scope, they may be used through the syntax `${VARIABLE_NAME}`. If parts of this paragraph seems confusing, take a look at some of the linked documentation as well as some of the working code within the firmware repository.
