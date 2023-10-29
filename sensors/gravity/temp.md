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

A digital waterproof temperature sensor that provides 9-bit to 12-bit Celsicus temperature measurements. This thermometer uses a 1-wire bues to communited. Because this sensor is digital, there would be any signal degration over long distance. 

Name: Gravity: Waterproof DS18B20 Sensor Kit 

Link: https://www.dfrobot.com/product-1354.html 

Type: Digital 

Operating Temperature: -55 ~ 100

Range of measurement: -10 ~ 85

Precision: +/- 0.5

Unit: Degrees Celsius 

Description: Waterproof temperature sensor. 

---

## JSON 
Publish Topic: device/reading/sensor/tmp
<div class="code-example" markdown="1">

```json
{
  value:        # float -- Celsius
}
```
</div>

Subscribe Topic: device/config/sensor/tmp
<div class="code-example" markdown="1">

```json
{
  state:          # binary
}
```
</div>