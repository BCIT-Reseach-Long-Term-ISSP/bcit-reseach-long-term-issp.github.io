---
layout: default
title: Water Pressure
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/water-pressure
---

# Water Pressure Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Water Pressure sensor that will sense whether there is water and how strong the water pressure is. 

Name: Gravity: Analog Water Pressure Sensor

Link: https://www.dfrobot.com/product-1517.html

Type: Analog 

Operational Range: -20 to 85 degrees C

Unit: mPa

---

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "wp",        # string
  data_type: "kpa",  # string -- kilopascal
  data_value:        # float
}
```
</div>