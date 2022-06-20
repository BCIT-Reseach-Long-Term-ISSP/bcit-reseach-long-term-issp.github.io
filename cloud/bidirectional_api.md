---
layout: default
title: Cloud API
has_children: false
permalink: /docs/cloud/bidirectional_communication/api
grand_parent: Cloud
parent: Bi-directional Communication
has_toc: false
---

# Cloud API

## _/config_

The **_`/config`_** endpoint is a `POST` request. It takes sensor/device, buoy details, and sensor config as stated in the [Subscribe Config](/smart-device/communication-protocol/subscribe-config.html) detailed by device team in its body. It also needs a firebase signed ID token in its header that authorizes a firebase user to use the HTTP method.

**Headers taken:**

- `authorizationToken` (REQUIRED): Authorization JWT token assigned by firebase client when a user signs in to verify that an authorized user has sent a request to set configurations to a device.

Example Headers:
`authorizationToken: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

**Request Body taken:**

- `version` (REQUIRED): Version number of topic that will be sent to. 
- `buoy_id` (REQUIRED): Buoy id that configuration payload will be sent to.
- `payload` (REQUIRED): Configuration payload that will be published to the IoT network that end devices/sensors will be subscribed to.

Example Body:
```json
{
    "version": 0,
    "buoy_id": 1,
    "payload": {
        "ph": {
            "time-interval": 6000,
            "unit": null,
            "average-value": true,
            "average-time-interval": 60,
            "disable": false
        }
    }
}
```

**Output formats:**

_Valid JWT:_
```json
{
    "statusCode": 200,
    "body": "\"Successfully published configuration to devices\"",
    "configuration": {
        "ph": {
            "time-interval": 6000,
            "unit": null,
            "average-value": true,
            "average-time-interval": 60,
            "disable": false
        }
    }
}
```

_Invalid JWT:_
```json
{
    "Message": "User is not authorized to access this resource with an explicit deny"
}
```

_Missing requirements:_
```json
{
    "statusCode": 400,
    "body": "\"must provide a buoy id in body\""
}
```
