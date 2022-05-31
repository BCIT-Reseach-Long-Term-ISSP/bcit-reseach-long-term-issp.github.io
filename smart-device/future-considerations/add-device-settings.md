---
layout: default
title: Add Device Settings
permalink: /docs/smart-device/future-considerations/add-device-settings/
parent: Future Considerations
grand_parent: Smart Device
---

# Add Device Settings

Implementing MQTT subscriptions in a future iteration would provide the device with the ability to store configuration information on the cloud and allow the users to remotely view and modify the device settings though the dashboard.

## Problem Statement

<p>Currently to change publish timing or any other device settings, a user would need to update the code and manually reflash the device. This would be time consuming for a technician and may lead to unforeseen complications if code is improperly modified.</p>

## Suggested Solution

<p>The MQTT communication protocol includes the functionality for devices to subscribe to topics and receive messages published to it. For example, this can be used for receiving updated device settings from the dashboard.</p>

## Microcontroller Complexities

<p>The smart-device goes into a sleep mode when not collecting or publishing data, so messages sent to the device cannot be read until it awakens. It is recommended that the device awakens for a short period of time before taking measurements, so that the device can receive and react to messages.</p>
