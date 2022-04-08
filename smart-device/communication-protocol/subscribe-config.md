---
layout: default
title: Subscribe Config
parent: MQTT Protocol
grand_parent: Smart Device
nav_order: 1
---

# Subscribe Config

This section provides an overview of how we expect to recieve device config messages, to modify device settings, from the AWS Broker.
{: .fs-6 .fw-300 }

## Broker Namespace Topic

All data is sent to the data subtopic of a designated Buoy ID.

<div class="code-example" markdown="1">

$aws/&lt;buoy_id&gt;/config/sensor/

$aws/&lt;buoy_id&gt;/config/global/

$aws/&lt;buoy_id&gt;/data/

$aws/&lt;buoy_id&gt;/error/

</div>

```
For example (data for Buoy ID = 1, version 0 of this project):

$aws/0/1/data/

```

## MQTT Packet Payload

The packet payload that will be published to the data topic is a JSON message.
This message will include key/value pairs with the key identifying the type of sensor and the value representing the data value that was measured.
Only the key/value pairs for the sensors on a buoy will be included in the message.

<p style="color:green;">1- Data Topic Payload :</p>

```
json
{
  "timestamp": 100132,
  "ph": 7.03,      # PH Sensor
  "tds": 10041,
  "pressure": 4.5,
}
```
<p style="color:green;">2- Errors Topic Payload :</p>

````
json
{
  "timestamp": 100132,
  "fatal-error": {
        code: 1,
        message: "arduino crashed"  
  },
  "connectivity-error": {
        code: 1,
        message: "bad connection" 
  },
   "sensor-error": {
        code: 1,
        message: "PH sensor value out of range" 
  },                                                                                            
}

````

<p style="color:green;">3- Sensor Config Topic Payload :</p>

````
json
{
    "ph": {
        "time-interval": 6000,
        "unit": null,
        "average-value": true,
        "average-time-interval": 60,
    },
    "tds": {
        "time-interval": 6000,
        "unit": ppm,
        "average-value": false,
        "average-time-interval": 0,
    },
    "pressure": {
        "time-interval": 6000,
        "unit": kpa,
        "average-value": false,
        "average-time-interval": 0,
    },
}
````
<p style="color:green;">4- Global Config Topic Payload</p>

````
json
{
    "overage-time-interval": 900,
    "use-low-power-mode": true,
    "reset": false,
    "shutdown": false,
}
````
For specific sensor information breakdown (name, data type, and data value) please refer to the relevant [sensors docs pages](https://github.com/just-the-docs/just-the-docs/tree/main/docs/CODE_OF_CONDUCT.md).