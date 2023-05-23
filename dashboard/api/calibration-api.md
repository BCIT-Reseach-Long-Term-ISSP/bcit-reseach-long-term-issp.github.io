---
layout: default
title: Calibration /api/calibration
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/calibration
nav_order: 7
---

# Calibration
{: .no_toc }
**Base route**: `/api/calibration`
{: .fs-6 .fw-300 }

| 📚 Read more about Calibration in [Back-end Server Architecture Weather & Tide documentation](/docs/dashboard/backend/weather-tide).|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /getSensorCalibrationPoints/:sensorId

| <b>Description</b>     | Gets all the calibration points for a given sensor. |
| <b>HTTP Verb</b>       | GET |
| <b>Success Codes</b>   | 200 |
| <b>Failure Codes</b>   | 500 server error |
| <b>Request Params</b>  | `{ sensorId: number }` |
| <b>Sample Params</b>   | `{ sensorId: 12 }` |
| <b>Request Schema</b>  | Request body is not applicable to this endpoint. |
| <b>Sample Request</b>  | Request body is not applicable to this endpoint. |

# Response Schema
A list of calibration points.
```
{
    "data": {
            "id": number,
            "digital_value": number,
            "physical_value": number,
            "sensor_id": number
        }[]
}
```

# Sample Response
```
{
    "data": [
        {
            "id": 1,
            "digital_value": 5.0,
            "physical_value": 1.3,
            "sensor_id": 1001
        },
        {
            "id": 2,
            "digital_value": 5.9,
            "physical_value": 1.4,
            "sensor_id": 1001
        },
        {
            "id": 5,
            "digital_value": 8.0,
            "physical_value": 7.0,
            "sensor_id": 1001
        }
    ]
}
```