---
layout: default
title: Arduino Zero + Sara R4 10M 02B Setup (Communication Device)
parent: Device Firmware Refactor
grand_parent: Smart Device
---

This README provides instructions for setting up and using the Arduino Zero with the SaraR4 NB-IoT Shield. This guide assumes that you have the necessary dependencies installed, including Git, the Arduino IDE, VSCode, Python, and Bash.

## Dependencies

- Git
- Repository
- Arduino IDE
- VSCode
- Python
- Bash
- Arduino CLi (https://arduino.github.io/arduino-cli/0.21/installation/)

## Hardware

- Arduino Zero
- SaraR4 NB-IoT Shield


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
4. **Connect Arduino Zero and SaraR4 NB-IoT Shield:**<br>
   Ensure that the shield is mounted on top of the Arduino Zero, and HardwareSerial serial1 is used for communication.

5. **Setup NB-IoT Shield:**<br>
   - Set switches on the shield to HardwareSerial and ArduinoPower.
   - Connect your laptop to the Arduino Zero via the programmer's port.
   - Open a serial monitor in the IDE with "Both NL & CR" and baudrate 115200.
   - Run the following Arduino sketches:
      - zero/setup/register_operator/register_operator.ino
      - zero/setup/serial_passthrough/serial_passthrough.ino
6. **Setup Shield Certificates:**<br>
   - Navigate to AWS IoT: AWS IoT → Manage → All devices → Things
   - If the thing already exists, create a new certificate and download all the generated certificates. Otherwise, go to `Create Thing` and create a new thing.
   - For Configure device certificate, choose Auto-generate a new certificate (recommended)
   - Download the certificates and keys, move them to the **zero/setup/certificates** folder, and rename as follows:
      * Device certificate: `certificate.pem.crt`
      * Public key file: `public.pem.key`
      * Private key file: `private.pem.key`
      * AmazonRootCA1.pem
      * AmazonRootCA3.pem
   - setup Virtual Environment:
      * Open a terminal window
      * `cd zero/setup/certificates`
      * Depending on how your python executable is set up, run one of the following commands:
         ```bash
            python -m venv venv
         ```
         or
         ```bash
            python3 -m venv venv
         ```
         or
         ```bash
            python3.11 -m venv venv
         ```
      * Activate virtual environment <br>
         Windows:
         ```bash 
            .\venv\Scripts\activate
         ```
         For macOS and Linux:
         ```bash
            source venv/bin/activate
         ```
      * Install dependecies:
         ```bash
            pip install -r requirements.txt
         ```
   - Close Arduino IDE before you run this command:
      ```bash
         python nbiot_cert_upload.py --port [port number of Arduino] --cert-dir [directory to your certificates]
      ```
      Example:
      ```bash
         python nbiot_cert_upload.py --port /dev/ttyACM0
      ```
6. **Upload Code:**<br>
   - Please use git bash for this.
   - cd zero/
   - ```bash
         chmod +x arduino_upload.sh
      ```
   - For help:
      ```bash
         ./arduino_uplaod.sh -h
      ```
   - To install core, burn bootloader, compile and upload code:
      ```bash
         ./arduino_upload.sh -i -b -c -u PORT=[Arduino port]
      ```
      Example:
      ```bash
         ./arduino_upload.sh -i -b -c -u PORT="dev/ttyACM0"
      ```

Now your Arduino Zero with SaraR4 NB-IoT Shield is set up and ready for NB-IoT communication.