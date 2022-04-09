---
layout: default
title: Publish Data
parent: MQTT Protocol
grand_parent: Smart Device
nav_order: 1
---

# Publish Data

This section provides an overview of how sensor data is sent to the AWS Broker.
{: .fs-6 .fw-300 }

## Broker Namespace Topic - Data

All data is sent to the data subtopic of a designated Buoy ID.

<div class="code-example" markdown="1">
```
$aws/<version#>/<buoy_id>/data/
```
</div>

For example (data for Buoy ID = 1, version 0 of this project):

<div class="code-example" markdown="1">
```
$aws/0/1/data/
```
</div>

## MQTT Packet Payload

The packet payload that will be published to the data topic is a JSON message.
This message will include key/value pairs with the key identifying the type of sensor and the value representing the data value that was measured.
Only the key/value pairs for the sensors on a buoy will be included in the message.

For example (Buoy with 1 PH sensor):

<div class="code-example" markdown="1">
```json
{
  "ph": 7.03,      # PH Sensor
}
```
</div>

For example (Buoy with all sensors):

<div class="code-example" markdown="1">
```json
{
  "do": 80.3,      # Dissolved Oxygen Sensor (%Sat)
  "ec": 250.21,    # Electrical Conductivity Sensor (ms/cm)
  "liqlev": true,  # Liquid Level Sensor (boolean)
  "ph": 7.03,      # PH Sensor
  "tds": 550.96,   # Total Dissolved Solids Sensor (ppm)
  "tbd": 0.8,      # Turbidity Sensor (NTU)
  "wf": 1.904,     # Water Flow Sensor (L/s)
  "wp": 9.81,      # Water Pressure Sensor (kpa)
  "temp" : 20.34   # Temperature Sensor (Degree C)
}
```
</div>

For specific sensor information breakdown (name, data type, and data value) please refer to the relevant [sensor pages](https://bcit-reseach-long-term-issp.github.io/docs/smart-device/sensors/sensors.md).