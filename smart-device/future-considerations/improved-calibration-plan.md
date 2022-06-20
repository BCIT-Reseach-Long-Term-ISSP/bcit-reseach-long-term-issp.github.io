---
layout: default
title: Improved Calibration Plan
permalink: /docs/smart-device/future-considerations/improved-calibration-plan/
parent: Future Considerations
grand_parent: Smart Device
---

# Improved Calibration Plan

An improved calibration plan should be able to be performed in the field, providing more accurate measurements by using more appropriate buffer solutions, and with the functionality to calibrate the sensors without manually changing the code.

## Problem Statement

Currently there is insufficient buffer solutions to properly calibrate the sensors, which has led to less accurate sensor measurements. Currently some sensors, such as the TDS and turbidity sensor, are being calibrated using distilled water, when it should be calibrated with a buffer solutions of known measurement values.

Additionally, for the analog sensors (turbidity, total dissolved solids, and dissolved oxygen), calibration currently requires a user to manually debug the code and update calibration variables in the code. They would then need to reflash the device with this updated code. This can lead to unforeseen problems, as code is improperly modified, and the calibration method of debugging the code to see the measurements makes it difficult to see when values stabilize or to get an overall picture of the sensors current function.

## Suggested Solution

At a minimum it is recommended that appropriate buffer solutions be purchased for every sensor being used. This would allow for more accurate calibration and therefore more accurate measurements.

The following two suggestion are only theoretical and may add significant complexities. Only one would probably be needed, but both could be deployed at once. The features behind both suggestions are used by other future considerations.

1. USB Communication + Calibration Mode: If USB communication is implemented, as mentioned in the [Integrate USB Debugging and Communication Future Consideration Section](https://bcit-reseach-long-term-issp.github.io/docs/smart-device/future-considerations/integrate-usb-debugging-and-communication/), a user could input a command to enter the device into calibration mode, where they could calibrate the sensors without needing to manually modify the code.

2. Cloud Calibration: Most analog sensors use only one or two k-values for calibration, which could be stored on the AWS Cloud. Using a calibration mode on the dashboard, a user could input the buffer solution parameters into the dashboard, which the cloud would use in conjunction with the actual values being measured by the device to modify the k-values (calibrate the sensors). This method would work particularly well if implemented with the [Cloud Post-Processing Future Consideration](https://bcit-reseach-long-term-issp.github.io/docs/smart-device/future-considerations/cloud-post-processing/), but would require significant changes to the Cloud and Dashboard architecture.

## Complexities

Both theoretical suggestions for improving the calibration plan will require the integration and testing of new features that each bring their own complexities. Additionally implementing calibration using each of these features may require modifying the main device loop, as both methods will likely be unusable in the current configuration where the device cannot receive message when it's in sleep mode.

An alterative, but not recommended solution, would be to use only high-quality Atlas EZO Sensors that can be calibrated on any device and store their calibration settings on built-in sensor chips. However, this is not recommended as these sensors are extremely expensive and this device should have the functionality to utilize lower quality sensors as well.
