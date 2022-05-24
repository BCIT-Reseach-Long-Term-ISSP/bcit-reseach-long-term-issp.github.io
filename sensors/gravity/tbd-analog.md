---
layout: default
title: Turbidity
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/tbd
---

# Turbidity Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

Detects water quality by measuring the turbidity/opaqueness. Uses light to detect suspended particles in water by measuring light transmittance and scattering rate. 

Name: Gravity: Analog Turbidity Sensor for Arduino 

Link: https://www.dfrobot.com/product-1394.html 

Type: Analog 

Operational temperature range: 5 – 90 degrees C

Output range: 0-4.5V

Unit: NTU 

## Note 
The top (black part) of the probe is not waterproof. 


---

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "tbd",      # string
  data_type: "NTU", # string -- nephelometric turbidity units
  data_value:       # float
}
```
</div>