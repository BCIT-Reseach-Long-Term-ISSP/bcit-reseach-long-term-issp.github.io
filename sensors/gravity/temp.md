---
layout: default
title: Temperature
parent: Gravity
grand_parent: Sensors
permalink: /docs/sensors/gravity/temp/
---

# Temperature Sensor
{: .no_toc }
## Gravity
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Temperature sensor.

Name: Gravity: Waterproof DS18B20 Sensor Kit 

Link: https://www.dfrobot.com/product-1354.html 

Type: Digital 

Operating Temperature: -55 ~ 125

Range of measurement: -10 ~ 85

Precision: +/- 0.5

Unit: Degrees Celsius 

Description: Waterproof temperature sensor. 

---

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "temp",      # string
  data_type: "C",    # string
  data_value:        # float -- Celsius
}
```
</div>