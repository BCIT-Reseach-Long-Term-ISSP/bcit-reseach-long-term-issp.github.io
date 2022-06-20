---
layout: default
title: Protype 0
has_children: false
permalink: /docs/prototype-0/
---

# Smart Device Prototype 0

This prototype was designed to provide a simple device to take measurements and send data to the cloud.

This prototype requires two Arduino Uno WiFi Rev 2 boards, the sensors, and an NBIoT Shield.

A single Arduino Uno WiFi Rev 2 does not have sufficient memory to both take sensor measurements and send data to the cloud. As such, this prototype uses two devices communicating over serial communication.

One device, the sensor device, collects all data, packages it into a JSON string, and sends the JSON string to the Comm Device.

The second, Comm Device, is constantly waiting for data to come in from the Sensor Device over serial communication. The Comm Device will continue to receive data until a carriage return ('\r') is received. Once it sees this carriage return, the device will transmit the payload to the cloud over narrowband cellular using the MQTT protocol.

These devices do not have any power or performance management features currently implemented.
