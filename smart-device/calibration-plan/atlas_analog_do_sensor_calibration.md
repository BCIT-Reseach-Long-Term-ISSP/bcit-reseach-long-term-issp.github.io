---
layout: default
title: Atlas Analog Dissolved Oxygen Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/atlas-analog-dissolved-oxygen-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# Atlas Analog Dissolved Oxygen Sensor Calibration

A walkthrough of the Atlas Analog Dissolved Oxygen Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

To be filled in

## Procedure Bare Metal Arduino Zero

1. Grab the Arduino Zero that you're deploying to the field

2. Connect the sensor to the Arduino board

3. Verify that measurements are being received

    - It is recommended that you create a new task that only takes a measurement for the DO sensor continuously

4. Dip the probe into water

5. Wave the sensor probe in the air for a few minutes

6. Debug the program and view the result of each measurement

7. Once the values have stabilized, record that measurement

8. Insert that value into the DO conversion function code in the fraction - ask Brittany for specific location

## Procedure Arduino Uno

1. Grab the Arduino Uno that you're deploying

2. Follow the process to download and run the sample code: https://www.atlas-scientific.com/files/gravity-DO-ardunio-code.pdf

3. Connect the DO sensor to the board

4. Flash the sample code to the Arduino Uno

5. Open the serial monitor

6. Wave the sensor probe in the air for a few minutes

7. Type "CAL" into the serial monitor and press enter.

8. You should receive a response on the serial monitor once complete.
