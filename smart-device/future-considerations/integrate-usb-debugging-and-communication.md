---
layout: default
title: Integrate USB Debugging and Communication
permalink: /docs/smart-device/future-considerations/integrate-usb-debugging-and-communication/
parent: Future Considerations
grand_parent: Smart Device
---

# Integrate USB Debugging and Communication

Integration of USB communication would allow technicians in the field to directly communicate wit the devices, seeing sensor measurements, entering calibration modes, etc. Using this functionality, many different features could be developed depending on future needs.

## Problem Statement

<p>There is no way for a technician to interact with the device while in use. Currently, the only way to modify the device is to change the code and reflash the device.</p>

## Suggested Solution

<p>The USB driver already exists, but it is not integrated into the main loop. A new task will need to be created to manage it's communication.</p>

## Complexities

<p>You get a read and write function that both come from buffers. There is a library that handles this, but all the commands and responses will need to be programmed.</p>
