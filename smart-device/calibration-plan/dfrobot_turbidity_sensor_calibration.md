---
layout: default
title: DFRobot Turbidity Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/dfrobot-turbidity-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# DFRobot Turbidity Sensor Calibration

A walkthrough of the DFRobot Turbidity Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

To be filled in

## Procedure Bare Metal Arduino Zero

1. Grab the Arduino Zero that you're deploying to the field

2. Connect the sensor to the Arduino board

3. Verify that measurements are being received

    - It is recommended that you create a new task that only takes a measurement for the turbidity sensor continuously

4. Place the sensor "probe" into the water

  - Make sure not to put it in too far, it is only waterproof on the bottom, clear, plastic part of the probe

  - It is assumed normal tap water will be close enough to 0 NTU to be considered accurate, but in the future, it may be good to get an actual buffer solution.

5. Wait a few minutes for the measurement to stabilize

6. Debug the program and view the result of each measurement

7. If the measurement voltage is not 4.2 V, rotate the potentiometer until it is.

  - Refer to this article for more information: https://how2electronics.com/diy-turbidity-meter-using-turbidity-sensor-arduino/
  
## Procedure Arduino Uno

1. Grab the Arduino Uno that you're deploying to the field

2. Connect the sensor to the Arduino board

3. Verify that measurements are being received

    - It is recommended that you create a new task that only takes a measurement for the turbidity sensor continuously

4. Place the sensor "probe" into the water

  - Make sure not to put it in too far, it is only waterproof on the bottom, clear, plastic part of the probe

  - It is assumed normal tap water will be close enough to 0 NTU to be considered accurate, but in the future, it may be good to get an actual buffer solution.

5. Wait a few minutes for the measurement to stabilize

6. Debug the program and view the result of each measurement

7. If the measurement voltage is not 4.2 V, rotate the potentiometer until it is.

  - Refer to this article for more information: https://how2electronics.com/diy-turbidity-meter-using-turbidity-sensor-arduino/
