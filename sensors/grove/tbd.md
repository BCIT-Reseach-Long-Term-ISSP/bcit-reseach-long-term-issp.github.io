---
layout: default
title: Turbidity
parent: Grove
grand_parent: Sensors
permalink: /docs/sensors/grove/tbd/
---

# Turbidity Sensor
{: .no_toc }
## Grove
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A Turbidity sensor.

Name: Grove - Turbidity Sensor (Meter) for Arduino V1.0

Link: https://www.seeedstudio.com/Grove-Turbidity-Sensor-p-4399.html

Calibration: No calibration for analogm, digital calibrated with the potentiometer.

Type: Analog/Digital 

Unit: NTU

---

## Calibration 

### Analog
No calibration can be done for analog setting

### Digital 
Adjust the potentiometer up and down. The voltage for clear tap water should be approx 4.200V.

## Notes
Only the clear part of the sensor is waterproof. Do NOT get the black part wet. 

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "tbd",      # string
  data_type: "V",   # string
  data_value:       # float
}
```
</div>