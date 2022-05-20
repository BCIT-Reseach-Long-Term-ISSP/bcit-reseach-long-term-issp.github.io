---
layout: default
title: Total Dissolved Solids
parent: Grove
grand_parent: Sensors
permalink: /docs/sensors/grove/tds
---

# Total Dissolved Solids Sensor
{: .no_toc }
## Grove
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Summary

A sesnor for mearuring total dissolved solids in water. 

Name: Grove - TDS Sensor/Meter For Water Quality (Total Dissolved Solids)

Link: https://www.seeedstudio.com/Grove-TDS-Sensor-p-4400.html

Calibration: No calibration for analogm, digital calibrated with the potentiometer.

Type: Analog

Operational Range: 0 to 60 degrees C

Unit: ppm (parts per million)

Range: 0 to 1000ppm

---

## Notes
Do not use in water above 70 degrees celcius.
This sensor will not work in flowing water

## JSON 

<div class="code-example" markdown="1">
```json
{
  name: "tds",       # string
  data_type: "ppm",  # string -- parts per million
  data_value:        # float
}
```
</div>
