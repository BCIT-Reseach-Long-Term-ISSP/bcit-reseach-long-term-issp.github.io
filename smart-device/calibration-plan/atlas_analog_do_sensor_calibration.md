---
layout: default
title: Atlas Analog Dissolved Oxygen Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/atlas-analog-dissolved-oxygen-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# Atlas Analog Dissolved Oxygen Sensor Calibration

A walkthrough of the Atlas Analog Dissolved Oxygen Sensor calibration procedure.
{: .fs-6 .fw-300 }

## Materials

1x Arduino Zero
1x Laptop
1x USB to micro-usb cable
3x M-F Jumper Wires
1x Arduino Micro Jumper
1x Bottle of Atlas Science Electrolye Solution
1x Bowl of Tap Water

## Calibration Procedure

1. Grab the Arduino Zero that's being deployed in the field

2. If the dissolved oxygen sensor has not been serviced in over a month, replace / fill the Electrolyte solution in the sensor membrane

3. Wire the dissolved oxygen sensor to the Arduino Zero board

4. Open the Visual Studio Code IDE

5. Open the device-firmware project

6. Set the program to run the test tasks

7. Set the test task to the CALIBRATE_DO_SENSOR task

8. Plug the laptop into the Arduino Zero programming port

9. Attach the micro jumper to the debugger chip enable wires

10. Run the program in debug mode

11. Add a debug point to the vtask delay after the sensor measure command

12. Verify that measurements are being received

13. If successfully recieiving emasurmenets, contine, else check the sensor wiring

14. Dip the probe into water

15. Remove the probe from the water and twirl it around in the air

16. Twirl the probe for a few minutes and start debigging teh program

17. Once the sensor measurments have stabilized, record the milivoltage of the measurement

18. Edit the calibration variable to succesfully claibrate the sensor

19. Repeat steps 14 - 16

20. If successfully calibrated the sensor should show the dissolved oxygen percentage of around 100%
