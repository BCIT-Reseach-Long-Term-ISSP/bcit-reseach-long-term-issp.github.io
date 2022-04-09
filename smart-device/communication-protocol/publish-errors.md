---
layout: default
title: Publish Errors
parent: MQTT Protocol
grand_parent: Smart Device
nav_order: 2
---

# Publish Errors

This section provides an overview of how device / sensor errors are sent to the AWS Broker.
{: .fs-6 .fw-300 }

## Broker Namespace Topic - Errors

All errors are sent to the error subtopic of a designated Buoy ID. This conveniently identifies the erroring buoy and allows the dashboard to interpret the data easily, translating it onto their interface. 

<div class="code-example" markdown="1">
```
$aws/<version#>/<buoy_id>/error/
```
</div>

For example (data for Buoy ID = 1, version 0 of this project):

<div class="code-example" markdown="1">
```
$aws/0/1/error/
```
</div>

## MQTT Packet Payload

The payload that will be published to the error topic is a JSON message.
This message will include a timestamp key representing time of error and a variable number of other keys which will represent the error type. Each of these keys will be paired with an object value. This object contains two keys:  code is an error identifier and message explains the error generally.

For example (Buoy with connectivity error):

<div class="code-example" markdown="1">
```json
{
    “timestamp”: 10032,
    “connectivity-error”: {
        code: 1,
        message: “bad connection”
    },
}
```
</div>

For example (Buoy with all the errors):

<div class="code-example" markdown="1">
```json
{
    “timestamp”: 10032,
    “fatal-error”: {
        code: 1,
        message: “arduino crashed”
    },
    “connectivity-error”: {
        code: 1,
        message: “bad connection”
    },
    “sensor-error”: {
        code: 1,
        message: “PH sensor values out of range”
    },
}
```
</div>

For specific error breakdown please refer to the relevant pages (under construction).
<!-- [error docs pages](https://github.com/just-the-docs/just-the-docs/tree/main/docs/CODE_OF_CONDUCT.md). -->