---
layout: default
title: Throw-in Type Liquid Level Transmitter 
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/throw-in-liquid-level/
---

# Throw-in Type Liquid Level Transmitter 
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Documentation
The document contains an overview and the code for the sensor
https://media.digikey.com/pdf/Data%20Sheets/DFRobot%20PDFs/KIT0139_Web.pdf

Excel doc (temporary)
Gravity Sensor Calibration Sheet

Product link
https://www.dfrobot.com/product-1863.html

## Summary

Cable Length: 5m  
Measuring Range: 0-5m  
Overall Accuracy: 0.5% 
Output Signal: 4-20mA  
Operating Voltage: 12-36V  
Operating Temperature: -20-70  
Overload Capacity: 300%  
Service Life: 1*10^8 
Pressure Circulation (25)  
Material: 316L stainless steel  
Protection Class: IP68 

---
## Important notes

The formula that is used in the documentation does not work correctly. 
We had to come up with our own way of measuring the depth based on the converted ADC voltage, using a linear equation. 
The sensor’s baseline measurement is 0.48v at 0m depth, and the first measurement is registered at 6cm deep.
For the initial purpose of testing, we had no access to a depth greater than 70cm. 
However, the rate of change was consistent from 6.00 cm to 70.00 cm. 
The sensor requires an external 12-36v power supply (refer to schematics below)
![Diagram](/sensors/assests/throw_in_liquid_level_diagram.png)
Based on the reading, we extrapolated the data using the following two formulas (where x is the ADC voltage):
```
  float adc_voltage = (float)adc_value / max_adc_value * v_ref_millivolts / 1000; 
  float depth = (35 * adc_voltage) + (-12.8); // inch // Replace with your own depth conversion equation
  float depthMM = depth * 2.54; // mm
```

The sensor requires a converter
![Converter](/sensors/assests/throw_in_liquid_level_converter.png)

---

## JSON 
#### Publish Topic: device/reading/sensor/lvl
<div class="code-example" markdown="1">

```json
{
  value:        # float
}
```
</div>

#### Subscribe Topic: device/config/sensor/lvl
<div class="code-example" markdown="1">

```json
{
  state:          # binary
}
```
</div>