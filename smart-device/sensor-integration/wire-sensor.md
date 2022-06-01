---
layout: default
title: Smart Device Wiring
parent: Sensor Integration
grand_parent: Smart Device
---

# Smart Device Wiring
{: .no_toc }

This section provides an overview of how to wire a new sensor to the smart device and wiring considerations that should be taken into account.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Arduino Board

The buoy device uses an Arduino Zero board as the brain of the device.
This Arduino Zero performs all processing and sensor mesaurements.

We will not go into the specifics of the Arduino Zero in this documentation as there are sources online.
However, there are some important points that should be noted.

- <p style="color:red;">The Arduino Zero can only handle voltages of 3.3 volts and lower, any voltage greater than this will fry the board.</p>

- The Arduino Zero does not have persistant memory, unlike the Arduino Uno.

## NB-IoT Shield

The module that allows the buoy device to send signals and communicate with the cloud is the NB-IoT shield.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/NB-IoT_shield.jpg?raw=true)

This shield rests on top of the Arduino Zero as a standard shield, connected by the pins sticking out the bottom of the shield.

This shield uses some of the pins on the Arduino Zero to function.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/NB-IoT_shield_diagram.jpg?raw=true)

<p style="color:red;">These pins cannot be used for any other purpose and attempting to do so will likely fry the board.</p>

With regards to wiring the sensors, the particular pins that care should be taken to avoid are the Digital 0, 10, and 11 pins.

## PERF Shield

To orgnaize the wiring and create the appropriate sensor circuits, an Arduino PERF shield is used.

## Taking Sensor Readings

The Arduino Zero has 6 built-in analog ports that can be used to take analog sensor measurements directly.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/analog_ports_highlight.jpg?raw=true)

Most sensors have 3 wires, the power wire (red), the ground wire (black), and the reading wire (other colour), that need to be connected to take these measurements.

### Single Sensor Reading

To take a single sensor's measuremnt, you can directly wire the sensor to the pins on the board.

For example, below is a diagram displaying a single sensor, with reading being taken on Analog Pin 0.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/single_sensor_reading_diagram.jpg?raw=true)

<i>Note: the Arduino board dispalyed in the diagram is an Arduino Uno, not an Arduino Zero. However, regarding the wiring configuration, the Arduino Uno and Zero are the same.</i>

As you can see the sensor is powered by the 3.3 Volt pin and connected to the ground pin. The 3.3V pin is used as the 5V pin would fry an Arduino Zero.

### Multiple Sensor Reading

To measure multiple sensors, you will need to create a simple circuit, using a breadbaord during development or a perf board for the actual device.

For example, below is a diagram displaying two sensors connected to a breadbaord, with reading being taken on Analog Pin 0 and 5.

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/multiple_sensor_reading_diagram.jpg?raw=true)

<i>Note: the Arduino board dispalyed in the diagram is an Arduino Uno, not an Arduino Zero. However, regarding the wiring configuration, the Arduino Uno and Zero are the same.</i>

As you can see power is being supplied to the breadbaord by the 3.3 Volt pin, with the second line grounded. The two sensors then branch off those lines, with their respective reading lines connected to the Arduino analog pins.
