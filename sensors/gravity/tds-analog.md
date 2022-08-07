---
layout: default
title: Total Dissolved Solids
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/tds/
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

Total dissolved solids indicates how many milligrams of soluable solids is dissolved in one leter of water. TDS value of water is used to reflect the cleanliness of water. 

Name: Gravity: Analog TDS Sensor/ Meter for Arduino

Link: https://www.dfrobot.com/product-1662.html

Type: Analog 

Operational temperature range: 0 – 55 degrees C

Output range: 0 to 2.3V

Unit: ppm


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
