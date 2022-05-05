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

- Install Visual Studio Code
- Clone the repo by running `git clone --recursive git@github.com:BCIT-Reseach-Long-Term-ISSP/device-firmware.git`
- Download the "toolchain.zip" care package from google drive. Extract it into "capstone-water-monitor-comm". There should now be a folder in there called "toolchain". This zip file contains Windows binaries for everything and development headers. For just the development headers instead dowload the "toolchain_sourceonly.zip" file. The programs included in the toolchain are listed below.
- Add the "bin" folder within the toolchain to your system PATH variable
- Open up Visual Studio Code and under the "Extensions" tab install "C/C++ Extension Pack" and "Cortex-Debug"
- Under the "Explorer" tab, click on "Open Folder" and navigate to the "firmware" folder inside of the repo
- Click on "Yes, I Trust the authors"
- Press "f7" to do an inital build. It will ask which kit to use, select "[Unspecified]"

# Software Included
These are the programs included with the toolchain. These can either be installed induvidually or through your Operating Systems' package manager.
- [Cmake](https://cmake.org/download/)
- [Ninja Build](https://ninja-build.org/)
- [ARM GNU toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
- [openocd](https://openocd.org/pages/getting-openocd.html)

{: .fs-6 .fw-300 }
