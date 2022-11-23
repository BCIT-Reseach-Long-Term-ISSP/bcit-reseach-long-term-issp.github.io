---
layout: default
title: Arduino Troubleshooting
has_children: false
permalink: /docs/firmware/arduino-troubleshooting
parent: Smart Device
nav_order: 1
---

# Troubleshooting

This section includes potential issues future Smart Device Teams may run into with the Arduinos and how to address them.

## Arduino Zero

### Blank serial monitor when running in Arduino IDE

This happens when the Arduino is flashed with different IDEs. When returning to the Arduino IDE, the Arduino will seem to flash but print statements will not print anything in the Serial Monitor. If this happens, you will need to restore the bootloader. 

In the Arduino IDE:
1. Select Tools > Programmer > "Atmel DBDG"
2. Select Tools > Burn Bootloader
3. Try uploading the code again and the Serial Monitor should begin printing as normal.
