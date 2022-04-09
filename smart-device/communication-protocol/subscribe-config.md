---
layout: default
title: Subscribe Config
parent: MQTT Protocol
grand_parent: Smart Device
nav_order: 1
---

# Subscribe Config

This section provides an overview of how we expect to recieve device config messages, to modify device settings, from the AWS Broker.
Each buoy device will be subscribed to two endpoints, one related to sensors configurations and one related to global device settings.
{: .fs-6 .fw-300 }

## Sensor Configurations

The 
<div class="code-example" markdown="1">
```
config/sensor/
```
</div>
 endpoint is used when sensor specific configurations are changed. Such as specifying sensor measurment method, as point measurement or averaged measurement.

### Broker Namespace Topic

The topic hierarchy that a buoy will subscribe to, to recieve it's sensor specific configurations is:

<div class="code-example" markdown="1">
```
$aws/<version#>/<buoy_id>/config/sensor/
```
</div>

For example if a user wanted to specify some sensor specific configurations for Buoy ID = 1, for version 0 of this project, they would publish a message to the following topic:

<div class="code-example" markdown="1">
```
$aws/0/1/config/sensor/
```
</div>

The buoy with buoy ID = 1 would then receive this message, since it's subscribed to that topic.

### MQTT Packet Payload

The packet payload that the buoy will be expecting from a sensor configuration message is a JSON string with the following key-value pairs.

<p style="color:green;">3- Sensor Config Topic Payload :</p>

````json
{
    "ph": {
        "time-interval": 6000,
        "unit": null,
        "average-value": true,
        "average-time-interval": 60,
        "disable": false
    },
    "tds": {
        "time-interval": 6000,
        "unit": "ppm",
        "average-value": false,
        "average-time-interval": 0,
        "disable": false
    },
    "pressure": {
        "time-interval": 6000,
        "unit": "kpa",
        "average-value": false,
        "average-time-interval": 0,
        "disable": false
    }

    ...
}
````

The key used to identify the specific sensor is the same string used to identify the data type used when sending the data payloads.

The sensor configuration options are:

"time-interval": The interval between sensor measurements being taken, this does not determine when the measuremnts are sent to the cloud. The data type for this value is seconds.

"unit": The units that measuremnts should be sent in.

"average-value": A boolean for whether measurments should be averaged before publishing.

"average-time-interval": The interval between sensor measurements being taken, for creating the average measurment. The data type for this value is seconds, but if the "average-value" boolean is false, it will be ignored.

"disable": A boolean for whether the sensor should take measurments.

## Global Device Configurations

The 
<div class="code-example" markdown="1">
```
config/global/
```
</div>
 endpoint is used when general device configuratings are changed. Such as the data publishing time interval for the device.

### Broker Namespace Topic

The topic hierarchy that a buoy will subscribe to, to recieve it's general device configuratings is:

<div class="code-example" markdown="1">
```
$aws/<version#>/<buoy_id>/config/global/
```
</div>

For example if a user wanted to specify that the buoy, with Buoy ID = 1, should publish data every 15 minutes. They would publish a message to the following topic:

<div class="code-example" markdown="1">
```
$aws/0/1/config/global/
```
</div>

The buoy with buoy ID = 1 would then receive this message, since it's subscribed to that topic.

### MQTT Packet Payload

The packet payload that the buoy will be expecting from a general device configurating message is a JSON string with the following key-value pairs.

<p style="color:green;">4- Global Config Topic Payload</p>

````json
{
    "publish-time-interval": 900,
    "use-low-power-mode": true,
    "reset": false,
    "shutdown": false
}
````

The general device configuration options are:

"publish-time-interval": The interval between the buoy publishing data to the cloud. The data type for this value is seconds.

"use-low-power-mode": A boolean for whether the device should use low power mode. 
If the device is in low power mode it will use less energy and will last longer, however if the device is not in low power mode it will stay connected to the Cloud and cna recieve messages at any time.

"reset": A boolean for whether the device should reset. If this is true, the device will reset and should start the startup process again.

"shutdown": A boolean for whether the device should shutdown completely. If the device is shutdown, it will no longer be able to recieve messages or publish data.
