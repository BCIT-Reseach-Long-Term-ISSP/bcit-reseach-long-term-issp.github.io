---
layout: default
title: Arduino Mega Setup (Sensor Reading Device)
parent: Device Firmware Refactor
grand_parent: Smart Device
---

# Arduino Mega (Sensor Reading Device)

This page provides instructions for setting up and using the Arduino Mega.

## Dependencies

- Git
- Repository
- Arduino IDE
- VSCode
- Bash
- Arduino CLi

## Hardware

- Arduino Mega

## Setup Steps

1. **Clone the Repository:**
   ```bash
   git clone `git@github.com:BCIT-Reseach-Long-Term-ISSP/device-firmware-refactor.git`
   ```

2. **Install Arduino CLI:**<br>
   Refrence: [Official Arduino CLI Installation Docuemnt](https://arduino.github.io/arduino-cli/0.21/installation/)

3. **Update Arduino Core:**
   ```bash
   arduino-cli core update-index --additional-urls https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```
4. **Connect Arduino Mega:**<br>
    - Connect Arduino Mega yo your laptop and open Arduino IDE Make sure your IDE is able to recognize the device.
    - If and when you try to upload any code to the mega, it just stops responsing sometimes. Mega would still be working but you'll see some sort of `timeout` when uploading code.
    Example:
        ```
        Device or resource busy
        ioctl("TIOCMGET"): Inappropriate ioctl for device
        ```
    - There are other kind of timeour erros as well. Usually restarting the Arduino IDE helps. I know it's very annoying.
    - If that doesn't work, after closing the IDE, try to find the process that is maybe still using the port that the mega is connected on. Sometimes the Arduino IDE's serial monitor doesn't detatch itself. So, for example, on linux, I usually do this:
        ```bash
            kill -9 $(lsof -t <PORT>)
        ```
        Example:
        ```bash
            kill -9 $(lsof -t /dev/ttyACM1)
        ```

5. **Upload Code:**<br>
   - Please use git bash for this.
   - cd mega/
   - ```bash
         chmod +x arduino_upload.sh
      ```
   - For help:
      ```bash
         ./arduino_uplaod.sh -h
      ```
   - To install core, compile and upload code:
      ```bash
         ./arduino_upload.sh -i -c -u PORT=[Arduino port]
      ```
      Example:
      ```bash
         ./arduino_upload.sh -i -c -u PORT="dev/ttyACM1"
      ```

Now your Arduino Mega should be ready to read sensor data.