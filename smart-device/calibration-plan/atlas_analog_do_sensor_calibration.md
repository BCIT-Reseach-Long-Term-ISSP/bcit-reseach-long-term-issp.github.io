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
1x USB to micro-USB cable
3x M-F Jumper Wires
1x Arduino Micro Jumper
1x Bottle of Atlas Science Electrolyte Solution
1x Bowl of Tap Water

## Calibration Procedure

1. Grab the Arduino Zero that's being deployed in the field

2. Attach the micro jumper to the debugger chip enable wires

3. If the dissolved oxygen sensor has not been serviced in over a month, replace / fill the Electrolyte solution in the sensor membrane

4. Wire the dissolved oxygen sensor to the Arduino Zero board

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/do_sensor_calibration/do_sensor_connection_zero.jpg?raw=true)

5. Connect the laptop to the Arduino Zero using a USB - micro-USB cable.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/do_sensor_calibration/do_sensor_full_setup_zero.jpg?raw=true)

6. Open the Visual Studio Code IDE

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/do_sensor_calibration/visual_studio_code_icon.png?raw=true)

7. Open the device-firmware project

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_open_device-firmware_project_highlight.jpg?raw=true)

8. Open the Command Palette

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_open_command_palette.png?raw=true)

9. Open the CMake Cache Editor by entering the command "CMake: Edit CMake Cahce (UI)" into the Command Palett

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_open_cmake_cache_editor.png?raw=true)

10. Check the EMA_BUILD_TESTS to ON, to set the program to run the test tasks

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_ema_build_tests_field_highlight.jpg?raw=true)

11. Enter CALIBRATE_DO_SENSOR into the EMA_TEST field to set the conditional compilation for the ifdef CALIBRATE_DO_SENSOR task

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_ema_test_field_highlight.jpg?raw=true)

12. Click the <b>Save</b> button to save the updates to the CMake Cache Editor

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/visual_studio_code_cmake_cache_editor_save_button_highlight.jpg?raw=true)

13. Press "F7" to flash the device with the new code

14. Run the program in debug mode

15. Add a debug point to the vtask delay after the sensor measure command

16. Verify that measurements are being received

17. If successfully receiving measurements, continue, else check the sensor wiring

18. Dip the probe into water

19. Remove the probe from the water and twirl it around in the air

20. Twirl the probe for a few minutes and start debugging the program

21. Once the sensor measurements have stabilized, record the millivoltage of the measurement

22. Edit the calibration variable to successfully calibrate the sensor

23. Repeat steps 14 - 16

24. If successfully calibrated the sensor should show the dissolved oxygen percentage of around 100%
