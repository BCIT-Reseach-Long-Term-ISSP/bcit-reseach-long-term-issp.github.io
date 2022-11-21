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
{: .fs-6 .fw-300 }

## Overview

This section will cover the sensors used in the December 2022 deliverable. It is a record of the sensors scrapped or are currently being used for future teams.

Each subsection will provide an overview of the sensor, whether it has been scrapped, and the reasons for why it has been scrapped.

We initially started off with 5 sensors, 4 of which is scrapped, and only 1 is in use.



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

[Datasheet](https://sensirion.com/media/documents/4EAF6AF8/61652C3C/Sensirion_CO2_Sensors_SCD30_Datasheet.pdf)


### Sensirion Gas Platform (SGP30)

**Status: Scrapped**

This CO2 sensor has been scrapped as it is redundant, and uses I2C communication which has not been implemented.

[Datasheet](https://files.seeedstudio.com/wiki/Grove-VOC_and_eCO2_Gas_Sensor-SGP30/res/Sensirion_Gas_Sensors_SGP30_Datasheet_EN.pdf)
