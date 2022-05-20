---
layout: default
title: Total Dissolved Solids
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/tds
---

# Total Dissolved Solids Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Total Dissolved Solids sensor.

Detects water quality by measuring the turbidity/opaqueness. Uses light to detect suspended particles in water by measuring light transmittance and scattering rate. 

Name: Gravity: Analog Turbidity Sensor for Arduino 

Link: https://www.dfrobot.com/product-1394.html 

Type: Digital and Analog 

Operational temperature range: 5 – 90 degrees C

Output range: 0-4.5V

Unit: NTU 


---

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "tds",        # string
  data_type: "ppm",  # string -- parts per million
  data_value:        # float
}
```
</div>

<!-- ### Convert units

<div class="code-example" markdown="1">
The adc to raw value can  be converted into two datatypes:

ADC Voltage: ADC_Raw
</div> -->
