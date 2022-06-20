---
layout: default
title: MQTT Protocol
has_children: false
permalink: /docs/smart-device/communication-protocol/mqtt
parent: Communication Protocols
grand_parent: Smart Device
---

# MQTT Protocol

The communication protocol used to send data between the smart device and the AWS broker.
{: .fs-6 .fw-300 }

## Broker Namespace Topics

The MQTT protocal uses a form of addressing called <b>MQTT Topics</b> to allow MQTT clients to share information.
These topics are structured as a hierarchy, similair to a file directory or web endpoints, with the forward slash ( / ) as the delimiter.

All communication between the buoy devices (MQTT client) and the AWS broker will follow the following conventions for topic hierarchy.

<div class="code-example" markdown="1">
```
$aws/<version#>/<buoy_id>/<specific_endpoint>
```
</div>

The MQTT topics are case-sensitive, so convention is that all topics are lower-case.

A diagram of the broker namespace topics can be found below:

![Untitled](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/smart-device/assets/broker_namespace_topics.jpg?raw=true)

The interactions between the Buoy Device (MQTT client) and the Dashboard (MQTT client) can be seen through the publish and subscription links.

## MQTT Packet Payload

All MQTT message payloads will be in JSON form.
The specific structure, key-value pairs, for these payloads can be found in the relevant subsections for the different message types.

{: .no_toc }
