---
layout: default
title: Liquid Level
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/liq-lev
---

# Liquid Level Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Non-Contact Liquid Level sensor. This sensor detects whether liquid is present or not. 

Name: Gravity: Non-contact Digital Water / Liquid Level Sensor For Arduino

Link: https://www.dfrobot.com/product-1493.html

Type: Analog 

Operational Range: 0 to 105 degrees C

Unit: 1/0


---
## Notes
The sensor needs to be placed on a dry side. 

![Diagram](/sensors/assests/liquid_level_diagrama.jpg)

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "liqlev",      # string
  data_type: "boolean",    # string
  data_value:       # boolean -- liquid detected
}
```
</div>