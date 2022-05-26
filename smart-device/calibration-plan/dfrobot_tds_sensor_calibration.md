---
layout: default
title: DFRobot TDS Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/dfrobot-tds-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# DFRobot TDS Sensor Calibration

A walkthrough of the DFRobot TDS Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

Arduino Board
Laptop 
Wires

Solution of known TDS value or electrical conductivity value 

## Procedure Bare Metal Arduino Zero

1. Grab the Arduino Zero that you're deploying to the field

2. Connect the sensor to the Arduino board

3. Verify that measurements are being received

    - It is recommended that you create a new task that only takes a measurement for the turbidity sensor continuously

4. Place the sensor "probe" into the buffer solution of known TDS

5. Wait a few minutes for the measurement to stabilize

6. Debug the program and view the result of each measurement

7. Once the values have stabilized, record that measurement

8. Calculate the factor to get the current measurement to the know measurement: k-value = known / measured

9. Write that factor into the k-value of the TDS conversion function code

  - Refer to this article for more information: https://how2electronics.com/diy-turbidity-meter-using-turbidity-sensor-arduino/
  
## Procedure Arduino Uno

1. Grab the Arduino Uno that you're deploying to the field

2. Connect the sensor to the Arduino board

3. Follow the instructions in this article: https://wiki.dfrobot.com/Gravity__Analog_TDS_Sensor___Meter_For_Arduino_SKU__SEN0244


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