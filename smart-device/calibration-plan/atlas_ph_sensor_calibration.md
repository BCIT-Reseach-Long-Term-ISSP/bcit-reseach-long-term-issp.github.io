---
layout: default
title: Atlas EZO pH Sensor Calibration
has_children: false
permalink: /docs/smart-device/calibration-plan/atlas-ezo-ph-sensor-calibration
parent: Calibration Plan
grand_parent: Smart Device
---

# Atlas EZO pH Sensor Calibration

A walkthrough of the Atlas EZO pH Sensor calibration procedure
{: .fs-6 .fw-300 }

## Materials

To be filled in

## Proedure Bare Metal Arduino Zero

Same procedure as the proedure for a Bare Metal Arduino Uno.

## Procedure Arduino Uno

1. Grab an Arduino Uno

2. Plug in the sensor into the Arduin Uno

  A) Sensor chip's VCC pin to the 3.3V pin on the Arduino

  B) Sensor chip's GND to a GND pin on the Arduino

  C) Sensor chip's RX pin to this Arduino's TX pin, determined by the above code, in this case digital pin 9
  
  D) Sensor chip's TX pin to this Arduino's RX pin, determined by the above code, in this case digital pin 8

3. Flash the following program to the Arduino Uno using the Arduino IDE


```c++
#include <SoftwareSerial.h>
#define rxPin 8
#define txPin 9

SoftwareSerial mySerial(8, 9); 

void setup() {
  Serial.begin(9600);
  while (!Serial) {
  }
  Serial.println("UART Communication Program for Working with Sensors");
  mySerial.begin(9600);
}

void loop() { 
  if (mySerial.available()) {
    Serial.write(mySerial.read());
  }
  if (Serial.available()) {
    mySerial.write(Serial.read());
  }
}
```

4. The software serial library should come pre-installed, but if it does not, install it.

5. Open the Serial Monitor

6. If you start seeing measurements value coming into the serial monitor, the sensor is connected correctly.

7. If you do not see anything in the serial monitor, type in "i" into the serial monitor and press enter.

You should see a response on the serial monitor, this means that sensor is properly connected.

8. Once properly connected, if you don't see measurements constantly coming into the serial monitor, type in "C,1" into the serial monitor and press enter.

9. Follow the remaining calibration instructions from the formal documentation, starting at page 11: https://files.atlas-scientific.com/pH_EZO_Datasheet.pdf

10. After calibration is complete, type in "C,0" into the serial monitor and press enter.

This will stop the sensor from sending continuous measurements.

11. Calibration is now complete

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