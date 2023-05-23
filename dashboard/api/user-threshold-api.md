---
layout: default
title: User Threshold /api/userThreshold
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/userThreshold
nav_order: 3
---

# User Thresholds
{: .no_toc }
**Base route**: `/api/userThreshold`
{: .fs-6 .fw-300 }

| 📚 Read more about how User Thresholds and Default Thresholds are used in the [Back-end Server Architecture Thresholds](/docs/dashboard/backend/thresholds) documentation.|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /getUserThresholdsByDevice/:userId/:deviceId

| <b>Description</b>   | Create a user threshold document in the database. |
| <b>HTTP Verb</b>     | GET |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |
| <b>Request Params</b>| { userId: string, deviceId: number } |
| <b>Sample Params </b>| { userId: '1234eigh89b02749e3a41c34', deviceId: 23 } |
| <b>Request Schema</b>| N/A    |
| <b>Sample Request</b>| N/A    |

### Response Schema
A list of [UserThreshold](/docs/dashboard/backend/thresholds#user-thresholds) entries for the user and the specified device is returned.
```
[
    {
        userId: string,
        sensorId: number,
        deviceId: number,
        minVal: number,
        maxVal: number,
        alert: boolean
    }
]
```

### Sample Response
```
[
    {
        userId: '1234eigh89b02749e3a41c34',
        sensorId: 14,
        deviceId: 23,
        minVal: 5,
        maxVal: 12,
        alert: boolean
    },
    {
        userId: '1234eigh89b02749e3a41c34',
        sensorId: 14,
        deviceId: 23,
        minVal: 32,
        maxVal: 80,
        alert: boolean
    },
    {
        userId: '1234eigh89b02749e3a41c34',
        sensorId: 14,
        deviceId: 23,
        minVal: -0.05,
        maxVal: 10,
        alert: boolean
    }
]
```

# /updateUserThreshold

| <b>Description</b>   | Update a user threshold document stored in the database. |
| <b>HTTP Verb</b>     | PUT |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema

A UserThreshold object's new values.
```
{
    userId: string,
    sensorId: number,
    deviceId: number,
    minVal: number,
    maxVal: number,
    alert: boolean
}
```

### Sample Request
```
{
    userId: '1234eigh89b02749e3a41c34',
    sensorId: 89,
    deviceId: 43,
    minVal: 3,
    maxVal: 7,
    alert: boolean
}
```

### Response Schema

Returns the updated document data.
```
{
    userId: string,
    sensorId: number,
    deviceId: number,
    minVal: number,
    maxVal: number,
    alert: boolean
}
```

### Sample Success Response
```
{
    userId: '1234eigh89b02749e3a41c34',
    sensorId: 89,
    deviceId: 43,
    minVal: 3,
    maxVal: 7,
    alert: boolean
}
```

### Fail Response

Failure Code 400:
```
{message: "Invalid request: user ID, device ID and metrics to update are required."}
```

Failure Code 500:
```
{ message: "There was an error with the request." } 
```

# /createUserThreshold

**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>   | Get a user's sensor thresholds for a given device. |
| <b>HTTP Verb</b>     | POST |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema

For metricList every metric device is capable of measuring can be added. If metrics device can measure are not added, if default threshold minimum and maximum values exist they are stored in the relevant fields. If default threshold values do not exist these fields which are not specified by user in request and can be measured by the device are recorded as “null”.
```
{
    "userId":"string,
    "deviceId": number,
    "sensorId": number,
    "min": number,
    "max": number,
    "alert": boolean
}
```

### Sample Request
```
{
    "userId": "63f2d25da584566f7ca037bf",
    "sensorId": 13,
    "deviceId": 26,
    "min": 131.23,
    "max": -900,
    "alert": true
}
```

### Response Schema
```
{
    "userId":"string,
    "deviceId": number,
    "sensorId": number,
    "min": number,
    "max": number,
    "alert": boolean
}
```

### Sample Success Response
```
{
    "userId": "63f2d25da584566f7ca037bf",
    "sensorId": 13,
    "deviceId": 26,
    "min": 131.23,
    "max": -900,
    "alert": true
}
```

### Fail Response
Failure Code 400:
```
{message: "Invalid request: user ID, and device ID are required."}
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```

# /deleteUserThreshold

**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b> | Delete a user threshold document stored in the database |
| <b>HTTP Verb</b> | DELETE |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |


### Request Schema
```
{
    "userId": string,
    "deviceId": number
}
```

### Sample Request
```
{
    "userId": "63f2d25da584566f7ca037bf",
    "deviceId": 17
}
```

### Response Schema
```
{
    “_id”: string,
    "userId": string,
    "deviceId": number,
    "metricList": {
        "dissolvedOxygen": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "temperature": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "turbidity": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "electricalConductivity": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "liquidLevel": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "ph": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "totalDissolvedSolids": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterFlow": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterLevel": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterPressure": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "co2Level": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "ch4Level": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "metricList": {
            "dissolvedOxygen": {
                "customMin": 397,
                "customMax": 797,
                "isWarning": false
            },
            "electricalConductivity": {
                "customMin": 23,
                "customMax": 57,
                "isWarning": true
            },
            "liquidLevel": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "ph": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "temperature": {
                "customMin": 23,
                "customMax": 57,
                "isWarning": false
            },
            "totalDissolvedSolids": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "turbidity": {
                "customMin": 159,
                "customMax": 387,
                "isWarning": true
            },
            "waterFlow": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "waterLevel": {
                "customMin": 112,
                "customMax": 350,
                "isWarning": true
            },
            "waterPressure": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "co2Level": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "ch4Level": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            }
        },
        "_id": "644b339935869a94d14ea5eb",
        "userId": "63f2d25da584566f7ca037bf",
        "deviceId": 26,
        "__v": 0
    }
}
```

### Fail Response

Failure Code 400:
```
{message: "Invalid request: user ID, and device ID are required."}
```

Failure Code 500
```
{ message: "There was an error with the request." }
```

# /getUserThresholdList

**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>   | Get a user threshold document stored in the database |
| <b>HTTP Verb</b>     | GET |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |


### Request Schema
```
{
    "userId": string,
    "deviceId": number
}
```

### Sample Request
```
{
    "userId": "63f2d25da584566f7ca037bf",
    "deviceId": 26
}
```

### Response Schema
```
{
    “_id”: string,
    "userId": string,
    "deviceId": number,
    "metricList": {
        "dissolvedOxygen": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "temperature": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "turbidity": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "electricalConductivity": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "liquidLevel": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "ph": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "totalDissolvedSolids": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterFlow": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterLevel": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "waterPressure": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "co2Level": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        },
        "ch4Level": {
              "customMin": number,
              "customMax": number,
              "isWarning": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "metricList": {
            "dissolvedOxygen": {
                "customMin": 37,
                "customMax": 89,
                "isWarning": false
            },
            "electricalConductivity": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "liquidLevel": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "ph": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "temperature": {
                "customMin": 23,
                "customMax": 57,
                "isWarning": false
            },
            "totalDissolvedSolids": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "turbidity": {
                "customMin": null,
                "customMax": null,
                "isWarning": false
            },
            "waterFlow": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "waterLevel": {
                "customMin": 112,
                "customMax": 350,
                "isWarning": true
            },
            "waterPressure": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "co2Level": {
                "customMin": null,
                "customMax": null,
                "isWarning": true
            },
            "ch4Level": {
                "customMin": null,
                "customMax": l,
                "isWarning": true
            }
        },
        "_id": "644b4e931fc20b032db20395",
        "userId": "63f2d25da584566f7ca037bf",
        "deviceId": 26,
        "__v": 0
    }
}
```

### Fail Response

Failure Code 400:
```
{message: "Invalid request: user ID, and device ID are required."}
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```

### /getSingleMetricUserThreshold

**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>   | Get single metric threshold for specified user and device |
| <b>HTTP Verb</b>     | GET |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema
```
{
    "userId": string,
    "deviceId": number,
    "metric": string
}
```

### Sample Request
```
{
    "userId": "63f2d25da584566f7ca037bf",
    "deviceId": 26,
    "metric": "dissolvedOxygen"
}
```

### Response Schema
```
{
    "metricList": {
                "dissolvedOxygen": {
                    "customMin": number,
                    "customMax": number,
                    "isWarning": boolean
                }
            },
            "_id": string,
            "userId": string,
            "deviceId": number
}
```

### Sample Success Response
```
{
    "text": {
        "metricList": {
            "dissolvedOxygen": {
                "customMin": 37,
                "customMax": 89,
                "isWarning": false
            }
        },
        "_id": "644b4e931fc20b032db20395",
        "userId": "63f2d25da584566f7ca037bf",
        "deviceId": 26
    }
}
```

### Fail Response

Failure Code 400:
```
{message: "Invalid request: user ID, and device ID are required."}
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```
