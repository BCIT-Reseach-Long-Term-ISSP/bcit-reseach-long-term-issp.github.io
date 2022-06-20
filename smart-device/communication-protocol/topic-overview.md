---
layout: default
title: Topic Overview
has_children: false
permalink: /docs/smart-device/communication-protocol/overview
parent: Communication Protocols
grand_parent: Smart Device
nav_order: 1
---

# Overview

## Topic Table

This table provides every namespace topic and a description of its purpose.

| Relative        | Absolute Path                 | Description |
|:-----------|:----------------------|:------|
| $aws /           | $aws / | MQTT Broker root path.  |
| *buoy_id* <sup>1</sup> / | $aws / *buoy_id* /   | The  buoy identifier. Used to uniquely identify  a client node in the MQTT ecosystem  |
| data /           | $aws / *buoy_id* / data /      | Designated for <span style="text-decoration: underline;">subscription</span> and <span style="text-decoration: underline;">publishing</span> of client node data. |
| error /           | $aws / *buoy_id* / error / | Designated for <span style="text-decoration: underline;">publishing</span> of error messages from client nodes. |
| config /           | $aws / *buoy_id* / config / | The configuration namespace path. Used for topic organisation only.  |
| sensor /           | $aws / *buoy_id* / config / sensor / | Designated for <span style="text-decoration: underline;">subscription</span> and <span style="text-decoration: underline;">publishing</span> of sensor specific configuration options.  |
| global /           | $aws / *buoy_id* / config / global / | Designated for <span style="text-decoration: underline;">subscription</span> and <span style="text-decoration: underline;">publishing</span> of global client node properties and configuration options. <br/><br/> <span style="text-decoration: underline;">NOTE: Access to this topic should be restricted to admin privileges only.</span> |

<sup>1</sup> All *italicized text* denote topic strings that are dynamic in nature (i.e. it’s value will change depending on the particular client node it is referencing).
{: .fs-2 .fw-300 }

## Topic Subscription and Publishing Tables

In this section, two tables are provided for further clarity regarding MQTT subscriptions and publishing to the broker namespace for the different project components.

### Subscription

| Client Node        | Subscription Topic                  | Purpose |
|:-----------|:----------------------|:------|
| Buoy           | $aws / *buoy_id* / config / sensor / | Sensor specific configuration options.  |
| Buoy           | $aws / *buoy_id* / config / global / | Global client node configuration and properties.  |
| Dashboard           | $aws / *buoy_id* / data / | Collection of published sensor data.  |
| Dashboard           | $aws / *buoy_id* / error / | Collection of published client node errors.  |

### Publishing

| Client Node        | Publishing Topic                  | Purpose |
|:-----------|:----------------------|:------|
| Buoy           | $aws / *buoy_id* / data / sensor / | Destination of raw collected client node sensor data.  |
| Buoy           | $aws / *buoy_id* / error / | Logging of client node errors.  |
| Dashboard           | $aws / *buoy_id* / config / global / | Remote setting of global configuration options.  |
| Dashboard           | $aws / *buoy_id* / config / sensor / | Remote setting of sensor specific configuration options.  |
| Dashboard           | $aws / *buoy_id* / error / | Remote detection and correction of client node errors.  |

{: .no_toc }
