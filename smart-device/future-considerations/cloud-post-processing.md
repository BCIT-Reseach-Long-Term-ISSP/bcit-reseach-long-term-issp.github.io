---
layout: default
title: Cloud Post-Processing
permalink: /docs/smart-device/future-considerations/cloud-post-processing/
parent: Future Considerations
grand_parent: Smart Device
---

# Cloud Post-Processing

## Problem Statement

Calibration is to check, adjust, or determine by comparison with a standard value. Sensor calibration adjustment is necessary for the Dissolved Oxygen, Turbidity, and TDS sensors. Introducing this adjustment introduces out of scope complexities to the microcontroller (Arduino Zero).

## Suggested Solution

Considering the scope of the current project, our solution involves post-processing raw sensor values on the cloud. The microcontroller would send raw values from the sensors and the cloud would post-process those values.

## Microcontroller Complexities

To detail the aforementioned complexities, the smart device team has strived to create a uniform, reusable C environment. In C, we have created a sensor object that encapsulates all sensors.

<div class="code-example" markdown="1">
```
struct sensor
{
    int pin;
    float value_adc;
    unsigned int type;
    float value_output;
    float * temperature;

    Measure measure;
    Convert convert;
};
```
</div>

<p> Introducing unique calibration functions expands the code base by file size and required understanding by future teams. Furthermore, if YVR intends to add a greenhouse gas sensor, we have decided adding a sensor would be easier by separating the sensor's microcontroller implementation and the post-processing.</p>

## Action Items
<ul>
<li>Pass on post-processing functions to cloud team from current microcontroller C environment.</li>
<li>Implement post-processing for AWS.</li>
</ul>
