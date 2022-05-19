---
layout: default
title: Atlas Analog Dissolved Oxygen Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/atlas-analog-dissolved-oxygen-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# Atlas Analog Dissolved Oxygen Sensor Calibration

A walkthrough of the Atlas Analog Dissolved Oxygen Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

To be filled in

## Proedure Bare Metal Arduino Zero

1. a

## Procedure Arduino Uno

1. 

<!--
# Publish Data

In this section, the following table is provided  regarding 
publishing of data to the MQTT broker namespace. Additionally,
examples for the payload of the MQTT packet are provided for further
clarity.

## Publish Topic Table

| **Topic**               | **Purpose**                                      |
| ----------------------  | ------------------------------------------------ |
| *$aws/<buoy_id>/data/*  | Destination of raw collected client sensor data. |
| *$aws/<buoy_id>/error/* | Reserved for logging of errors                   |


### JSON Shorthand Abbreviations

The packet payload is published as a serialized JSON string. The values
of the aforementioned string correspond to the particular sensor from which
the data has been collected. A breakdown of the expanded meaning of the shorthand
abbreviations is presented below:

#### **$aws/<buoy_id>/data/**

| **Shorthand**               | **Expanded**                            | **Units**         |
| --------------------------- | --------------------------------------  | ----------------- |
| do                          | Dissolved Oxygen Sensor                 | *mg/L*            |
| ec                          | Electrical Conductivity Sensor          | *ms/cm*           |
| liqlev                      | Liquid Level Sensor                     | *bool*            |
| ph                          | PH Sensor                               | *pH*              |
| tds                         | Total Dissolved Solids Sensor           | *ppm*             |
| tbd                         | Turbidity Sensor                        | *NTU*             |
| wf                          | Water Flow Sensor                       | *L/s*             |
| wp                          | Water Pressure Sensor                   | *kpa*             |
| temp                        | Temperature Sensor                      | *Degrees Celsius* |


### Payload: *$aws/<buoy_id>/error/*

```json
{
  "do": 80.3,      
  "ec": 250.21,    
  "liqlev": true,  
  "ph": 7.03,      
  "tds": 550.96,   
  "tbd": 0.8,      
  "wf": 1.904,     
  "wp": 9.81,      
  "temp" : 20.34   
}
```

### Payload: *$aws/<buoy_id>/error/*
```json
{
  "errno": 4,
  "errmsg": "Failed to collect data from pH sensor"
}
```


 *For more specific sensor information breakdown (name, data type, and data value) please refer to the relevant [sensors docs pages](https://github.com/just-the-docs/just-the-docs/tree/main/docs/CODE_OF_CONDUCT.md).*
 -->