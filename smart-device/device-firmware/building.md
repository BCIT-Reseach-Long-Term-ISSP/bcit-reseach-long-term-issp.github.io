---
layout: default
title: Building, Flashing, and Debugging the Firmware
has_children: false
permalink: /docs/firmware/building
parent: Device Firmware
grand_parent: Smart Device
has_toc: false
---

# Building, Flashing, and Debugging the Firmware using Visual Studio Code

- Install Visual Studio Code
- Clone the repo by running `git clone --recursive git@github.com:BCIT-Reseach-Long-Term-ISSP/device-firmware.git`
- **Windows Users**: Download the "toolchain.zip" care package from google drive. Extract it somewhere, then add the "bin" folder within to your system PATH variable. This zip file contains Windows binaries for all the tools required to build the project. For non-windows users, the programs included in the toolchain are listed below.
- Open up Visual Studio Code and under the "Extensions" tab install "C/C++ Extension Pack" and "Cortex-Debug"
- Under the "Explorer" tab, click on "Open Folder" and navigate to the "firmware" folder inside of the repo
- Click on "Yes, I Trust the authors"
- Press "f7" to do an inital build. It will ask which kit to use, select "[Unspecified]"

# Software Required
These are the programs required for build. These can either be installed induvidually or through your Operating Systems' package manager.
- [Cmake](https://cmake.org/download/)
- [Ninja Build](https://ninja-build.org/)
- [ARM GNU toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
- [openocd](https://openocd.org/pages/getting-openocd.html)

{: .fs-6 .fw-300 }
