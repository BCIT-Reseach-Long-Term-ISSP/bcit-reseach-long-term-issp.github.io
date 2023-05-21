---
layout: default
title: Device /api/device
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/device
nav_order: 2
---

# Device
{: .no_toc }
**Base route**: `/api/device`
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Outdated Endpoints

|**🚧 <span style="color:orange">The following endpoints are not updated and must be modified in collaboration with the Cloud team to utilize the AWS RDS: `/createDevice`, `/updateDevice`, `/deleteDevice`, `/getAllDevices`, `/getSingleDevice`, `/getDevicesWithinRadius`</span>**|

At the end of the sprint in the Spring of 2023, the project has been directed to have Device Settings, Sensor Details, and Calibration details to be pulled from Cloud team's AWS RDS.

The only endpoints at this time that are doing so are `/getAllDevicesSettings` and `/updateDeviceSettings`. The remaining, as listed above, are pulling from the Dashboard MongoDB database, which is not what the client would prefer.



# /getAllDeviceSettings

| <b>Description</b>    | Retrieves all valid devices and their sensor configurations. |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |
| <b>Request Schema</b> | N/A |
| <b>Sample Request</b> | N/A |

### Response Schema
```
[
    {
        id: number,
        name: string,
        description: string,
        locationX: number,
        locationY: number,
        active: boolean,
        timeInterval: int,
        sensors: [
            {
                id: number,
                deviceId: number,
                lastCalibrationDate: string,
                minCalibrationPts: number,
                metric: string,
                defaultUnit: string,
                calibrated: boolean,
                enabled: boolean,
                minVal: number,
                maxVal: number,
            }, ...
        ]
    }
]
```

### Sample Response
```
[
    {
        "id": 0,
        "name": "Guichon",
        "description": "Device in Guichon",
        "locationX": -123.1495,
        "locationY": 49.1999,
        "active": true,
        "timeInterval": null,
        "sensors": [
            {
                "id": 10,
                "deviceId": 0,
                "lastCalibrationDate": "",
                "minCalibrationPts": 2,
                "metric": "ph",
                "defaultUnit": "pH",
                "calibrated": true,
                "enabled": true,
                "minVal": 0,
                "maxVal": 13
            },
            {
                "id": 11,
                "deviceId": 0,
                "lastCalibrationDate": "2023-05-10T04:18:23.545772",
                "minCalibrationPts": 2,
                "metric": "tds",
                "defaultUnit": "ppm",
                "calibrated": true,
                "enabled": true,
                "minVal": 2,
                "maxVal": 5
            }, ...
        ]
    },
    {
        "id": 1,
        "name": "Expo",
        "description": "Device in Expo",
        "locationX": -123.205,
        "locationY": 49.19,
        "active": true,
        "timeInterval": null,
        "sensors": [ ... ]
    }
]
```

# /updateDeviceSettings

| <b>Description</b>    | Updates a device's settings with the given body. |
| <b>HTTP Verb</b>      | PUT |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema
```
{
    device_id: number,
    device_name: string,
    device_description: string,
    location_x: number,
    location_y: number,
    time_interval: number,
    active: boolean
}
```

### Sample Request
```
{
    "device_id": 1006,
    "device_name": "Device A",
    "device_description": "A device description here!",
    "location_x": 48.123,
    "location_y": -129.746,
    "time_interval": 60,
    "active": true
}
```

### Response Schema
```
{
    message: string
}
```

### Sample Success Response
```
{
    "message": "Successfully updated the device"
}
```

### Sample Fail Response
```
{
    "message": "No device found with the given device_id"
}
```



# /createDevice
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>   | Create a device document in the database |
| <b>HTTP Verb</b>     | POST |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema
```
{
    "deviceId": number,
    "coordinates": [number, number],
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Request
```
{
    "deviceId": 26,
    "coordinates": [-123.264137, 49.205469],
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": true
        },
        "electricalConductivity": {
            "isAvailable": false
        },
        "liquidLevel": {
            "isAvailable": true
        },
        "ph": {
            "isAvailable": true
        },
        "temperature": {
            "isAvailable": true
        },
        "totalDissolvedSolids": {
            "isAvailable": true
        },
        "turbidity": {
            "isAvailable": false
        },
        "waterFlow": {
            "isAvailable": true
        },
        "waterLevel": {
            "isAvailable": true
        },
        "waterPressure": {
            "isAvailable": true
        },
        "co2Level": {
            "isAvailable": true
        },
        "ch4Level": {
            "isAvailable": true
        }
    }
}
```

### Response Schema
```
{
    "_id": string,
    "deviceId": number,
    "location": {
        "type": "Point",
        "coordinates": [number, number]
    },
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "deviceId": 26,
        "location": {
            "type": "Point",
            "coordinates": [
                -123.264137,
                49.205469
            ]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": true
            },
            "electricalConductivity": {
                "isAvailable": false
            },
            "liquidLevel": {
                "isAvailable": true
            },
            "ph": {
                "isAvailable": true
            },
            "temperature": {
                "isAvailable": true
            },
            "totalDissolvedSolids": {
                "isAvailable": true
            },
            "turbidity": {
                "isAvailable": false
            },
            "waterFlow": {
                "isAvailable": true
            },
            "waterLevel": {
                "isAvailable": true
            },
            "waterPressure": {
                "isAvailable": true
            },
            "co2Level": {
                "isAvailable": true
            },
            "ch4Level": {
                "isAvailable": true
            }
        },
        "_id": "644a9fdd004bc38959451326",
        "__v": 0
    }
}
```
### Fail Response
```
{ 
    "message": "There was an error with the request." 
}
```

# /updateDevice
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>   | Update a device document stored in the database |
| <b>HTTP Verb</b>     | PUT |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema
“deviceId” should exist in the request body to find the document to be updated. For “coordinates” and metrics within “metricList”, sending only the data wanted to be updated by following nested json format below would be sufficient. E.g., if only “dissolvedOxygen” wanted to be updated sending only “dissolvedOxygen” within “metricList” would be enough.
```
{
    "deviceId": number,
    "coordinates": [number, number],
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Request
```
{
    "deviceId": 25,
    "coordinates": [-123, 49.177414],
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": true
        },
        "electricalConductivity": {
            "isAvailable": true
        },
        "liquidLevel": {
            "isAvailable": false
        },
        "ph": {
            "isAvailable": false
        },
        "temperature": {
            "isAvailable": true
        },
        "totalDissolvedSolids": {
            "isAvailable": true
        },
        "turbidity": {
            "isAvailable": false
        },
        "waterFlow": {
            "isAvailable": true
        },
        "waterLevel": {
            "isAvailable": true
        },
        "waterPressure": {
            "isAvailable": true
        },
        "co2Level": {
            "isAvailable": true
        },
        "ch4Level": {
            "isAvailable": true
        }
    }
}
```

### Response Schema
```
{
    "deviceId": number,
    "location": {
        "type": "Point",
        "coordinates": [number, number]
    },
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "location": {
            "coordinates": [
                -123,
                49.177414
            ]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": true
            },
            "electricalConductivity": {
                "isAvailable": true
            },
            "liquidLevel": {
                "isAvailable": false
            },
            "ph": {
                "isAvailable": false
            },
            "temperature": {
                "isAvailable": true
            },
            "totalDissolvedSolids": {
                "isAvailable": true
            },
            "turbidity": {
                "isAvailable": false
            },
            "waterFlow": {
                "isAvailable": true
            },
            "waterLevel": {
                "isAvailable": true
            },
            "waterPressure": {
                "isAvailable": true
            },
            "co2Level": {
                "isAvailable": true
            },
            "ch4Level": {
                "isAvailable": true
            }
         },
         "deviceId": 25
    }
}
```

### Fail Response
Failure Code 400:
```
{ 
    "message": 
    "Invalid request: id, and device information to be updated (location [longitude, latitude], metric name) is required." 
} 
```
Failure Code 500:
```
{ 
    "message": "There was an error with the request." 
}
```

# /deleteDevice
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>    | Delete a device document in the database |
| <b>HTTP Verb</b>      | DELETE |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |
| <b>Request Schema</b> | `{ "deviceId": number }` |
| <b>Sample Request</b> | `{ "deviceId": 25 }` |

### Response Schema
```
{
    "deviceId": number,
    "location": {
        "type": "Point",
        "coordinates": [number, number]
    },
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "location": {
            "coordinates": [
                -123,
                49.177414
            ]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": true
            },
            "electricalConductivity": {
                "isAvailable": true
            },
            "liquidLevel": {
                "isAvailable": false
            },
            "ph": {
                "isAvailable": false
            },
            "temperature": {
                "isAvailable": true
            },
            "totalDissolvedSolids": {
                "isAvailable": true
            },
            "turbidity": {
                "isAvailable": false
            },
            "waterFlow": {
                "isAvailable": true
            },
            "waterLevel": {
                "isAvailable": true
            },
            "waterPressure": {
                "isAvailable": true
            },
            "co2Level": {
                "isAvailable": true
            },
            "ch4Level": {
                "isAvailable": true
            }
        },
        "deviceId": 25
     }
}
```

### Fail Response
Failure Code 400:
```
{ message: "Invalid request: device id is required." }
```
Failure Code 500:
```
{ "message": "There was an error with the request." }
```

# /getAllDevices
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b> | Get all device documents stored in the database |
| <b>HTTP Verb</b> | GET |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 500 |
| <b>Request Schema</b> | N/A |
| <b>Sample Request</b> | N/A |

### Response Schema

Response is array of device documents stored in the database.
```
[
    {
        "deviceId": number,
        "location": {
            "coordinates": [number, number]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": boolean
            },
            "electricalConductivity": {
                "isAvailable": boolean
            },
            "liquidLevel": {
                "isAvailable": boolean
            },
            "ph": {
                "isAvailable": boolean
            },
            "temperature": {
                "isAvailable": boolean
            },
            "totalDissolvedSolids": {
                "isAvailable": boolean
            },
            "turbidity": {
                "isAvailable": boolean
            },
            "waterFlow": {
                "isAvailable": boolean
            },
            "waterLevel": {
                "isAvailable": boolean
            },
            "waterPressure": {
                "isAvailable": boolean
            },
            "co2Level": {
                "isAvailable": boolean
            },
            "ch4Level": {
                "isAvailable": boolean
            }
        }
    },
    {
        "deviceId": number,
        "location": {
            "coordinates": [number, number]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": boolean
            },
            "electricalConductivity": {
                "isAvailable": boolean
            },
            "liquidLevel": {
                "isAvailable": boolean
            },
            "ph": {
                "isAvailable": boolean
            },
            "temperature": {
                "isAvailable": boolean
            },
            "totalDissolvedSolids": {
                "isAvailable": boolean
            },
            "turbidity": {
                "isAvailable": boolean
            },
            "waterFlow": {
                "isAvailable": boolean
            },
            "waterLevel": {
                "isAvailable": boolean
            },
            "waterPressure": {
                "isAvailable": boolean
            },
            "co2Level": {
                "isAvailable": boolean
            },
            "ch4Level": {
                "isAvailable": boolean
            }
        }
    },
]
```

### Sample Success Response
```
{
    "text": [
        {
            "location": {
                "coordinates": [
                    -123.264137,
                    49.205469
                ]
            },
            "metricList": {
                "dissolvedOxygen": {
                    "isAvailable": true
                },
                "electricalConductivity": {
                    "isAvailable": false
                },
                "liquidLevel": {
                    "isAvailable": true
                },
                "ph": {
                    "isAvailable": true
                },
                "temperature": {
                    "isAvailable": true
                },
                "totalDissolvedSolids": {
                    "isAvailable": true
                },
                "turbidity": {
                    "isAvailable": false
                },
                "waterFlow": {
                    "isAvailable": true
                },
                "waterLevel": {
                    "isAvailable": true
                },
                "waterPressure": {
                    "isAvailable": true
                },
                "co2Level": {
                    "isAvailable": true
                },
                "ch4Level": {
                    "isAvailable": true
                }
            },
            "deviceId": 26
        },
        {
            "location": {
                "coordinates": [
                    -123,
                    49.177414
                ]
            },
            "metricList": {
                "dissolvedOxygen": {
                    "isAvailable": true
                },
                "electricalConductivity": {
                    "isAvailable": true
                },
                "liquidLevel": {
                    "isAvailable": false
                },
                "ph": {
                    "isAvailable": false
                },
                "temperature": {
                    "isAvailable": true
                },
                "totalDissolvedSolids": {
                    "isAvailable": true
                },
                "turbidity": {
                    "isAvailable": false
                },
                "waterFlow": {
                    "isAvailable": true
                },
                "waterLevel": {
                    "isAvailable": true
                },
                "waterPressure": {
                    "isAvailable": true
                },
                "co2Level": {
                    "isAvailable": true
                },
                "ch4Level": {
                    "isAvailable": true
                }
             },
             "deviceId": 25
         }
    }
}
``` 

### Fail Response
```
{ "message": "There was an error with the request." }
```

# /getSingleDevice
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b>    | Get a device document stored in the database |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |
| <b>Request Schema</b> | `{ "deviceId": number }` |
| <b>Sample Request</b> | `{ "deviceId": 25 }` |

### Response Schema
```
{
    "deviceId": number,
    "location": {
        "coordinates": [number, number]
    },
    "metricList": {
        "dissolvedOxygen": {
            "isAvailable": boolean
        },
        "electricalConductivity": {
            "isAvailable": boolean
        },
        "liquidLevel": {
            "isAvailable": boolean
        },
        "ph": {
            "isAvailable": boolean
        },
        "temperature": {
            "isAvailable": boolean
        },
        "totalDissolvedSolids": {
            "isAvailable": boolean
        },
        "turbidity": {
            "isAvailable": boolean
        },
        "waterFlow": {
            "isAvailable": boolean
        },
        "waterLevel": {
            "isAvailable": boolean
        },
        "waterPressure": {
            "isAvailable": boolean
        },
        "co2Level": {
            "isAvailable": boolean
        },
        "ch4Level": {
            "isAvailable": boolean
        }
    }
}
```

### Sample Success Response
```
{
    "text": {
        "location": {
            "coordinates": [
                -123,
                49.177414
            ]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": true
            },
            "electricalConductivity": {
                "isAvailable": true
            },
            "liquidLevel": {
                "isAvailable": false
            },
            "ph": {
                "isAvailable": false
            },
            "temperature": {
                "isAvailable": true
            },
            "totalDissolvedSolids": {
                "isAvailable": true
            },
            "turbidity": {
                "isAvailable": false
            },
            "waterFlow": {
                "isAvailable": true
            },
            "waterLevel": {
                "isAvailable": true
            },
            "waterPressure": {
                "isAvailable": true
            },
            "co2Level": {
                "isAvailable": true
            },
            "ch4Level": {
                "isAvailable": true
            }
        },
        "deviceId": 25
    }
}
```

### Fail Response
Failure Code 400
```
{ message: "Invalid request: device id is required." }
```

Failure Code 500
```
{ "message": "There was an error with the request." }
```

# /getDevicesWithinRadius
**🚧<span style="color:orange"> This endpoint is using MongoDB and must be updated to use AWS RDS</span>**

| <b>Description</b> | Gets devices within the specified radius (meter) of a chosen coordinate (point) |
| <b>HTTP Verb</b> | GET |
| <b>Success Codes</b> | 200 |
| <b>Failure Codes</b> | 400, 500 |

### Request Schema
```
{
    "coordinates": [number, number],
    "radius": number
}
```
### Sample Request
```
{
    "coordinates": [-123.161585, 49.178428],
    "radius": 15000
}
```

### Response Schema
Response is array of device documents stored in the database.
```
[
    {
        "deviceId": number,
        "location": {
            "coordinates": [number, number]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": boolean
            },
            "electricalConductivity": {
                "isAvailable": boolean
            },
            "liquidLevel": {
                "isAvailable": boolean
            },
            "ph": {
                "isAvailable": boolean
            },
            "temperature": {
                "isAvailable": boolean
            },
            "totalDissolvedSolids": {
                "isAvailable": boolean
            },
            "turbidity": {
                "isAvailable": boolean
            },
            "waterFlow": {
                "isAvailable": boolean
            },
            "waterLevel": {
                "isAvailable": boolean
            },
            "waterPressure": {
                "isAvailable": boolean
            },
            "co2Level": {
                "isAvailable": boolean
            },
            "ch4Level": {
                "isAvailable": boolean
            }
        }
    },
    {
        "deviceId": number,
        "location": {
            "coordinates": [number, number]
        },
        "metricList": {
            "dissolvedOxygen": {
                "isAvailable": boolean
            },
            "electricalConductivity": {
                "isAvailable": boolean
            },
            "liquidLevel": {
                "isAvailable": boolean
            },
            "ph": {
                "isAvailable": boolean
            },
            "temperature": {
                "isAvailable": boolean
            },
            "totalDissolvedSolids": {
                "isAvailable": boolean
            },
            "turbidity": {
                "isAvailable": boolean
            },
            "waterFlow": {
                "isAvailable": boolean
            },
            "waterLevel": {
                "isAvailable": boolean
            },
            "waterPressure": {
                "isAvailable": boolean
            },
            "co2Level": {
                "isAvailable": boolean
            },
            "ch4Level": {
                "isAvailable": boolean
            }
        }
    },
]
```

### Sample Success Response
```
{
    "text": [
        {
            "location": {
                "coordinates": [
                    -123.264137,
                    49.205469
                ]
            },
            "metricList": {
                "dissolvedOxygen": {
                    "isAvailable": true
                },
                "electricalConductivity": {
                    "isAvailable": false
                },
                "liquidLevel": {
                    "isAvailable": true
                },
                "ph": {
                    "isAvailable": true
                },
                "temperature": {
                    "isAvailable": true
                },
                "totalDissolvedSolids": {
                    "isAvailable": true
                },
                "turbidity": {
                    "isAvailable": false
                },
                "waterFlow": {
                    "isAvailable": true
                },
                "waterLevel": {
                    "isAvailable": true
                },
                "waterPressure": {
                    "isAvailable": true
                },
                "co2Level": {
                    "isAvailable": true
                },
                "ch4Level": {
                    "isAvailable": true
                }
            },
            "deviceId": 26
        },
        {
            "location": {
                "coordinates": [
                    -123,
                    49.177414
                ]
            },
            "metricList": {
                "dissolvedOxygen": {
                    "isAvailable": true
                },
                "electricalConductivity": {
                    "isAvailable": true
                },
                "liquidLevel": {
                    "isAvailable": false
                },
                "ph": {
                    "isAvailable": false
                },
                "temperature": {
                    "isAvailable": true
                },
                "totalDissolvedSolids": {
                    "isAvailable": true
                },
                "turbidity": {
                    "isAvailable": false
                },
                "waterFlow": {
                    "isAvailable": true
                },
                "waterLevel": {
                    "isAvailable": true
                },
                "waterPressure": {
                    "isAvailable": true
                },
                "co2Level": {
                    "isAvailable": true
                },
                "ch4Level": {
                    "isAvailable": true
                }
             },
             "deviceId": 25
         }
    }
}
```

### Fail Response
Failure Code 400
```
{ 
    message: "Invalid request: location coordinates (longitude, latitude) and radius information are required." 
}
```
Failure Code 500
```
{ "message": "There was an error with the request." }
```
