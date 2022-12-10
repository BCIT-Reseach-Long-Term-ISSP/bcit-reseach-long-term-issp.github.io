---
layout: default
title: December 2022 Devices
has_children: false
permalink: /docs/firmware/dec-2022-devices
parent: Smart Device
nav_order: 1
---

# December 2022 Devices

A record of the devices that have been scrapped or are currently being used for the December 2022 deliverable.
Some arduino code can be found here: [Datasheet](https://github.com/BCIT-Reseach-Long-Term-ISSP/sensor-investigation-and-testing)

{: .fs-6 .fw-300 }

## Overview

This section will cover the sensors used in the December 2022 deliverable. It is a record of the sensors scrapped or are currently being used for future teams.

We initially started off with 5 sensors, 4 of which is scrapped, and only 1 (CO2 sensor - SCD30) is in use.

The SCD30 will include a quick setup guide.


## Water Pressure Sensor

### DFRobot Gravity Water Pressure Sensor (SEN0257)

**Status: Scrapped**

This water pressure sensor has been scrapped due to the impractical calibration requirements. It must be calibrated at ~100m depth in water.

[Datasheet](https://wiki.dfrobot.com/Gravity__Water_Pressure_Sensor_SKU__SEN0257)



## Methane Sensors

### Winsen Flammable Gas Sensor (MQ-4)

**Status: Scrapped**

Initially purchased to measure methane, this sensor has been scrapped due to its impractical preheat time of 48 hours.

[Datasheet](https://cdn.sparkfun.com/datasheets/Sensors/Biometric/MQ-4%20Ver1.3%20-%20Manual.pdf)


### Winsen Toxic Gas Sensor (MQ-9B)

**Status: Scrapped**

Scrapped for the same reasons above.

[Datasheet](https://cdn.sparkfun.com/assets/d/f/5/e/2/MQ-9B_Ver1.4__-_Manual.pdf)


## Recommended Replacements for Methane Sensors

As both methane sensors have been scrapped due to the impractical preheating requirements, we have recommended 2 additional methane sensors.

### DFRobot: Fermion: MEMS Gas Sensor (MiCS-5524)

This sensor detects a variety of gases including methane. However, please note that it only detects methane levels above 1000PPM. It also requires a filtered enclosure to protect it from water and dust, but it only has a 3 minute warmup time.

[Link](https://www.dfrobot.com/product-2419.html)


### Winsen NDIR Infrared CH4 Sensor C3H8 Sensor (MH-440D)

This sensor detects methane and propane, and has a detection range of 0~10% vol. It only has a 3 minute warmup time as well.

[Link](https://shop.winsen-sensor.com/products/mh-440d-ndir-infrared-ch4-sensor-c3h8-sensor?variant=42124558860480)



## CO2 Sensors

### Sensirion CO2, Humidity, and Temperature Sensor (SCD30)

**Status: In Use**

We decided to keep this sensor over the Sensirion SGP30, as it uses UART communication, which is already present in the codebase.

CO2 measurement range: 0 - 40,000PPM
> **_NOTE:_** We have been using the 3.3V supply from the Arduino. We are unsure if using differing voltages may affect value readings.
DC Supply Voltage: 3.3V (minimum) - 5.5V (maximum)
Communication: I2C, UART

Connecting this sensor to the Arduino is relatively straightforward:
- Connect VDD and SEL to 3.3V
- Connect GND to GND
> **_NOTE:_** when creating the sensor in the code, you will need to set the ports in code
- Connect TX/SCL to any numbered port
- Connect RX/SDA to any numbered port 
- The 3.3V power can be split in a breadboard to get 3.3V to both the SEL and the VDD ports as seen below.
![Diagram](/assets/wiring.png)

[Datasheet](https://sensirion.com/media/documents/4EAF6AF8/61652C3C/Sensirion_CO2_Sensors_SCD30_Datasheet.pdf)


### Sensirion Gas Platform (SGP30)

**Status: Scrapped**

This CO2 sensor has been scrapped as it is redundant, and uses I2C communication which has not been implemented.

[Datasheet](https://files.seeedstudio.com/wiki/Grove-VOC_and_eCO2_Gas_Sensor-SGP30/res/Sensirion_Gas_Sensors_SGP30_Datasheet_EN.pdf)
