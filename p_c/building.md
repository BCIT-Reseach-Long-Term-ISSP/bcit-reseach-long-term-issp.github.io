---
layout: default
title: Building, Flashing, and Debugging the Firmware
has_children: false
permalink: /docs/power-comm/building
parent: Power and Communication
has_toc: false
nav_order: 3
---

# Building, Flashing, and Debugging the Firmware

These are directions on how to set up your development environment for the code located at <https://github.com/BCIT-Reseach-Long-Term-ISSP/capstone-water-monitor-comm>.

## Pre-requisites
1. Install Arduino IDE
2. Enter Tools->Board->Boards Manager
3. From the window, install "Arduino SAMD Boards", version 1.8.12
4. Install cmake and ninja build system then make sure executables for both are in your PATH
5. Install [Eclipse IDE for Embedded C/C++ Developers](https://www.eclipse.org/downloads/packages/release/2021-12/r/eclipse-ide-embedded-cc-developers)
6. Install [cmake4eclipse](https://github.com/15knots/cmake4eclipse#installation) plugin to the freshly installed eclipse IDE.
7. In a new eclipse workspace, enter File->New->Project..." then in the new window go "C/C++ -> C Project"
8. Under "Project Type" select "cmake4eclipse -> Empty Project" 
9. Uncheck "Use default location" and select the "firmware" folder within this repository.
10. Name the new project then press "Finish"
11. The new project is created.

## Setting up debug
You need to find your arduino base directory...

On windows it is located in **%appdata%\Arduino15**

On linux it is located in **~/.arduino15**

For the remainder of this guide this folder will be referred to as "\<arduinodir\>"

Create a new debug configuration...

1. From the main menu select "Run->Debug Configurations"
2. Under "GDB OpenOCD Debugging" create a new launch configuration,
3. Select your created project under "Project"
4. Under "C/C++ Application" click "Search Project". Make sure you have built the project at least once so then it finds the correct file. A ".elf" file should be in the list. Select it.
5. In the "Debugger" tab, ensure "Start openOCD locally" is checked. 
6. In "Executable Path" choose \<arduinodir\>/packages/arduino/tools/openocd/0.10.0-arduino7/bin/openocd".
7. In "Config Options" enter "-f\<arduinodir\>/packages/arduino/hardware/samd/1.8.12/variants/arduino_zero/openocd_scripts/arduino_zero.cfg". 
8. Under "GDB Client Setup" check "Start GDB Session".
9. In "Executable Name" enter "\<arduinodir\>/packages/arduino/tools/arm-none-eabi-gcc/7-2017q4/bin/arm-none-eabi-gdb". If on windows add ".exe" to the end.
10. Click apply and debugging should now be set up.

{: .fs-6 .fw-300 }
