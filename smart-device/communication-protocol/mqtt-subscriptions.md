---
layout: default
title: Subscription Data
parent: MQTT Protocol
grand_parent: Smart Device
nav_order: 1
---

# Subscription Data

In this section, the following table is provided  regarding
subscription of data from the MQTT broker namespace. Additionally,
examples for the payload of the MQTT packet are provided for further
clarity.

## Publish Topic Table

| **Topic**                        | **Purpose**                                      |
| -------------------------------  | ------------------------------------------------ |
| *$aws/<buoy_id>/config/sensor/*  | Global client node configuration and properties. |
| *$aws/<buoy_id>/config/global/*  | Sensor specific configuration options.           |


### JSON Shorthand Abbreviations

The packet payload is published as a serialized JSON string. The values
of the aforementioned string correspond to the particular sensor from which
the data has been collected. A breakdown of the expanded meaning of the shorthand
abbreviations is presented below:

#### **$aws/<buoy_id>/config/global/**

| **Shorthand**               | **Expanded**                            | **Units/type**    |
| --------------------------- | --------------------------------------  | ----------------- |
| id                          | Globally unique buoy ID                 | *int*             |
| freq                        | Default measurement frequency           | *seconds*         |
| on                          | Power on/off status                     | *bool*            |

#### **$aws/<buoy_id>/config/sensor/**

| **Shorthand**               | **Expanded**                            | **Units/type**    |
| --------------------------- | --------------------------------------  | ----------------- |
| id                          | Globally unique buoy ID                 | *int*             |
| freq                        | Default measurement frequency           | *seconds*         |
| on                          | Power on/off status                     | *bool*            |

### Payload: *$aws/<buoy_id>/config/global/*

```json
{
  "id": 1,
  "freq": 3600,      
  "on": true,    
  "tbd": true
}
```

### Payload: *$aws/<buoy_id>/config/sensor/*
```json
{
  "id": 1,
  "freq": 3600,
  "on": true,
  "tbd": true
}
```


*For more specific sensor information breakdown (name, data type, and data value) please refer to the relevant [sensors docs pages](https://github.com/just-the-docs/just-the-docs/tree/main/docs/CODE_OF_CONDUCT.md).*