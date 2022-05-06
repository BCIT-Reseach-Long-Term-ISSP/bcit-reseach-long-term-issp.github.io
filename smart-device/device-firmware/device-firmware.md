---
layout: default
title: Device Firmware
has_children: true
permalink: /docs/firmware
parent: Smart Device
has_toc: true
---

# Device Firmware

The firmware for the smart device is written in Bare-metal C using CMake for its build system and runs on the Arduino Zero board. Cross-platform directions on how to set up the toolchain can be found under [Building, Flashing, and Debugging the firmware](building).

Once set up, you should have the source code building. The code has the following structure:

| firmware   | Source code root       |
| Prototypes | Arduino IDE prototypes |

The code within firmware has the following structure:

| .vscode  | Visual Studio Code Project Settings     |
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

# How the code is built

This project uses CMake for building the firmware. Once the tool chain has been successfully set up, Visual Studio Code will automatically discover the CMakeLists.txt file within the firmware directory. Building of the firmware is done in several steps. Firstly, the configure stage is run by [CMake](https://cmake.org/) to generate the build scripts. These are placed within a "build" directory inside of firmware. Secondly, Visual Studio Code calls [Ninja](https://ninja-build.org/) to run the build scripts. In the build script, a device image is built using GCC, then flashed to the board using OpenOCD. Once flashed, OpenOCD runs a GDB Server which uses the built files in conjunction with the live device to provide utilities such as single stepping or viewing memory.

![Build Steps](/docs/assets/buildsteps.svg)

# FreeRTOS

The firmware for this project is based around [FreeRTOS](https://freertos.org/). In main, board initialization functions are called (see startup directory) then FreeRTOS is launched with a startup task. It is within this task that the bulk of the program is run. Within this task, all FreeRTOS features are supported such as memory allocation, multitasking, buffers and more. Run-time information about FreeRTOS can also be found while debugging through the Cortex-Debug extension for VSCode. For more information on Available FreeRTOS APIs, see [https://freertos.org/features.html](https://freertos.org/features.html)

# HAL Development

Within the "src" directory is a "hal" directory which contains low-level drivers for smart sensors and hardware interfaces. The code within this directory interfaces with the SAMD21 peripherals directly through registers. Detailed explanations of how to use these peripherals through the registers can be found in the SAMD21 [Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/SAM-D21DA1-Family-Data-Sheet-DS40001882G.pdf). 

By including the file "sam.h" within your code, you can also gain access to the CMSIS headers which makes these registers easier to access and control. You can look through some of the HAL code that is already made to get acquainted on how to use these.

# Adding New Source files and include paths to the build

A common operation is the creation of new C files and directories in the source tree. After making these you need to tell CMake where they are. There are two aspects which are in play here, _Include directories_ and _source files_. _Include directories_ are directories where the C compiler will search for header files whenever you use `#include "..."`. Generally whenever you create a new source directory you add it as an include directory. _Source Files_ are the ".c" files which the C compiler will directly process. Note the distinction between _Header Files_ and _Source Files_, ".h" files are not source files!!!

When making an executable, CMake takes a list of source files to build and assigns them to a target. Include directories can then be attached to that target. In this project we build everything into a single target called "ema_yvr_comm.elf", so we need to supply our list of source files all at once. This is done through CMake variables.

A CMake variable is created using the [set()](https://cmake.org/cmake/help/latest/command/set.html) function within "CMakeLists.txt" files. The main task of the CMakeLists.txt files through the project is to eventually build a `SRCS` variable to be passed into [add_executable()](https://cmake.org/cmake/help/latest/command/add_executable.html). This is done through a cascade, where various CMakeLists.txt files defining parts of the `SRCS` variable throughout the project are included from the root using [add_subdirectory()](https://cmake.org/cmake/help/latest/command/add_subdirectory.html). To make variables defined in these sub-files available to the file above, calls to _set()_ must have the `PARENT_SCOPE` parameter included at the end before the last bracket, otherwise they will not be accessible. Once these variables are passed to the parent scope, they may be used through the syntax `${VARIABLE_NAME}`. If parts of this paragraph seems confusing, take a look at some of the linked documentation as well as some of the working code within the firmware repository.
