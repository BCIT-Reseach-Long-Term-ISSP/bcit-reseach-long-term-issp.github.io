---
layout: default
title: Device API Endpoint
has_children: false
permalink: /docs/cloud/bidirectional_communication/api_endpoints/device_api_endpoint
grand_parent: Bi-directional Communication
parent: API Endpoints
has_toc: false
---

# Device API Endpoint

The purpose of this endpoint is to send the configuration data to IoT devecies, save configuration data for callibration logic and notification thresholds.

The configuration data is sent to IoT devices via MQTT topics with [update](#update-old-configuration-data) operation.

Note: Authorization (JWT token) is required for all endpoints

## Add new configuration data
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "add",
        "id": 26,
        "Name": "Device name",
        "Description": "Device description",
        "Device status": true,
        "location": {
            "latitude": 40.7128,
            "longitude": -74.0060
        },
        "sensors": "sensors": [
            {
                "id": 2,
                "measurement": "do",
                "power": true,
                "min": 1,
                "max": 100,
                "units": "%",
                "alerts": true,
                "calibration": {
                    "dateLastCalibrated": "2023-11-04",
                    "physicalValue": [
                        1.3,
                        5.2
                    ],
                    "digitalValue": [
                        4.3,
                        6.3
                    ]
                }
            }
        ]
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "msg": "Successfully added new id data."
        }
        ```
    - if the given body was invalid:
        ```json
        {
            "msg": "Body should include values for all parameters."
        }
        ```
    - if the given entry already exists
        ```json
        {
            "msg": "Failed to add new user data. 26 already exists in database."
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Body should have id."
        }
        ```


    

## <a name="update-old-configuration-data"></a>Update old configuration data
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "update",
        "id": 26,
        "Name": "Device name",
        "Description": "Device description",
        "Device status": false,
        "location": {
            "latitude": 36.7128,
            "longitude": -78.0060
        },
        "sensors": "sensors": [
            {
                "id": 2,
                "measurement": "do",
                "power": false,
                "min": 1,
                "max": 100,
                "units": "%",
                "alerts": true,
                "calibration": {
                    "dateLastCalibrated": "2023-11-04",
                    "physicalValue": [
                        2.3,
                        4.2
                    ],
                    "digitalValue": [
                        3.3,
                        5.3
                    ]
                }
            }
        ]
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "msg": "Successfully updated device data."
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Body should have id."
        }
        ```
    - if the given body was invalid:
        ```json
        {
            "msg": "Body should include values for all new parameters."
        }
        ```
    - if the given entry does not exist
        ```json
        {
            "msg": "Failed to update device data. 26 does not exist in database."
        }
        ```
    
## Delete old configuration data
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "delete",
        "id": 26,
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "msg": "Successfully deleted following id:",
            "deleted_id": 26,
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Missing id in request body."
        }
        ```

## Scan existing configuration data
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "scan",
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "devices": [
                {
                    "location": {
                        "latitude": 40.7128,
                        "longitude": -74.006
                    },
                    "sensors": [
                        1,
                        2,
                        3
                    ],
                    "operation": "update",
                    "id": 26,
                    "Name": "Device name",
                    "Description": "Device description",
                    "Device status": false
                }
            ]
        }
        ```

## Scan existing configuration data for sensors
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "scan_sensors",
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "devices": [
                {
                    "id": "26",
                    "sensors": [
                        {
                            "id": 2,
                            "measurement": "do",
                            "power": false,
                            "min": 1,
                            "max": 100,
                            "units": "%",
                            "alerts": false,
                            "calibration": {
                                "dateLastCalibrated": "2023-11-04",
                                "physicalValue": [
                                    1.3,
                                    5.2
                                ],
                                "digitalValue": [
                                    4.31,
                                    6.3
                                ]
                            }
                        }
                    ]
                }
            ]
        }
        ```

## Scan existing configuration data for the given device
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "scan_device",
        "id": 26
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "location": {},
            "sensors": [
                {
                    "id": 2,
                    "measurement": "do",
                    "power": false,
                    "min": 1,
                    "max": 100,
                    "units": "%",
                    "alerts": false,
                    "calibration": {
                        "dateLastCalibrated": "2023-11-04",
                        "physicalValue": [
                            1.3,
                            5.2
                        ],
                        "digitalValue": [
                            4.31,
                            6.3
                        ]
                    }
                }
            ],
            "operation": "update",
            "id": 26,
            "Name": "Device name",
            "Description": "Device description",
            "Device status": false
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Missing id in request body."
        }
        ```
    - if no item was found
        ```json
        {
            "msg": "Device not found."
        }
        ```

## Scan existing configuration data for the given device and sensor
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "scan_device",
        "id": 26,
        "sensor_id": 2
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "id": 2,
            "measurement": "do",
            "power": false,
            "min": 1,
            "max": 100,
            "units": "%",
            "alerts": false,
            "calibration": {
                "dateLastCalibrated": "2023-11-04",
                "physicalValue": [
                    1.3,
                    5.2
                ],
                "digitalValue": [
                    4.31,
                    6.3
                ]
            }
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Missing id in request body."
        }
        ```
    - if no sensor id was given
        ```json
        {
            "msg": "Missing sensor_id in request body."
        }
        ```
    - if no device was found
        ```json
        {
            "msg": "Device not found."
        }
        ```
    - if no sensor was found
        ```json
        {
            "msg": "Sensor not found."
        }
        ```

## Delete existing configuration data for the given device and sensor
-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/device
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body required
- Body format example:
    ```json
    {
        "operation": "delete_sensor",
        "id": 26,
        "sensor_id": 2
    }
    ```
-   Response:
    - if the call was successful:
        ```json
        {
            "msg": "Sensor 2 has been deleted from device 26."
        }
        ```
    - if no id was given
        ```json
        {
            "msg": "Missing id in request body."
        }
        ```
    - if no sensor id was given
        ```json
        {
            "msg": "Missing sensor_id in request body."
        }
        ```
    - if no device was found
        ```json
        {
            "msg": "Device not found."
        }
        ```
    - if no sensor was found
        ```json
        {
            "msg": "Sensor not found."
        }
        ```
