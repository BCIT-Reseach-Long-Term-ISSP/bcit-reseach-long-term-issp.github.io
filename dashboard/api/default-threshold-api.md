---
layout: default
title: Default Threshold /api/defaultThreshold
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/defaultThreshold
nav_order: 4
---

# Default Thresholds
{: .no_toc }
**Base route**: `/api/defaultThreshold`
{: .fs-6 .fw-300 }

| 📚 Read more about how User Thresholds and Default Thresholds are used in the [Back-end Server Architecture Thresholds](/docs/dashboard/backend/thresholds) documentation.|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /createDefaultThreshold

| <b>Description</b>    | Create a default threshold document in the database. |
| <b>HTTP Verb</b>      | POST |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema
```
{
    "metric": string (a valid metric code),
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Request
```
{
    "metric": "do",
    "defaultMin": 60,
    "defaultMax": 70
}
```

### Response Schema
```
{
    "_id": string,
    "metric": string,
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Success Response
```
{
    "text": {
        "metric": "dissolvedOxygen",
        "defaultMin": 60,
        "defaultMax": 70,
        "_id": "644b12f36f6b221f921ba2c7",
        "__v": 0
    }
}
```

### Fail Response

Failure Code 400:
```
{ message: "Invalid request: metric, default minimum and default maximum values are required." }
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```

### /updateDefaultThreshold

| <b>Description</b>    | Update a default threshold document stored in the database. |
| <b>HTTP Verb</b>      | PUT |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema
```
{
    "metric": string,
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Request
```
{
    "metric": "do",
    "defaultMin": 900,
    "defaultMax": 1000
}
```

### Response Schema
```
{
    "_id": string,
    "metric": string,
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Success Response
```
{
    "text": {
        "_id": "644b12f36f6b221f921ba2c7",
        "metric": "dissolvedOxygen",
        "defaultMin": 900,
        "defaultMax": 1000,
        "__v": 0
    }
}
```

### Fail Response
Failure Code 400:
```
{ 
    message: "Invalid request: metric value and at least one of default minimum, default maximum values (defaultMax > defaultMin) are required." 
}
```
Failure Code 500:
```
{ message: "There was an error with the request." }
```

# /deleteDefaultThreshold

| <b>Description</b>    | Delete a default threshold document stored in the database. |
| <b>HTTP Verb</b>      | DELETE |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |

### Request Schema
```
{
    "metric": string
}
```

### Sample Request
```
{
    "metric": "dissolvedOxygen"
}
```

### Response Schema

Return deleted document.
```
{
    "_id": string,
    "metric": string,
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Success Response
```
{
    "text": {
        "_id": "644b12f36f6b221f921ba2c7",
        "metric": "dissolvedOxygen",
        "defaultMin": 900,
        "defaultMax": 1000,
        "__v": 0
    }
}
```

### Fail Response
Failure Code 400:
```
{ message: "Invalid request: metric is required." }
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```

# /getAllDefaultThresholds

| <b>Description</b>    | Get all default threshold documents stored in the database. |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 |
| <b>Request Schema</b> | Endpoint does not expect a request body or parameters. |
| <b>Sample Request</b> | Endpoint does not expect a request body or parameters. |

### Response Schema 

Response is array of default threshold documents stored in the database.
```
[
    {
        "_id": string,
        "metric": string,
        "defaultMin": number,
        "defaultMax": number
   },
    {
        "_id": string,
        "metric": string,
        "defaultMin": number,
        "defaultMax": number
   }
]
```

### Sample Success Response
```
{
    "text": [
        {
            "_id": "6418eabe22a59781f4a36c76",
            "metric": "waterLevel",
            "defaultMin": 112,
            "defaultMax": 350,
            "__v": 0
        },
        {
            "_id": "6418ead722a59781f4a36c78",
            "metric": "electricalConductivity",
            "defaultMin": 5,
            "defaultMax": 10,
            "__v": 0
        }
    ]
}
```

### Fail Response

Failure Code 500
```
{ message: "There was an error with the request." }
```

### /getSingleDefaultThreshold

| <b>Description</b>    | Get a default threshold document stored in the database. |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 400, 500 |
| <b>Request Schema</b> | Endpoint does not expect a request body or parameters. |
| <b>Sample Request</b> | Endpoint does not expect a request body or parameters. |

### Request Schema
```
{
    "metric": string
}
```

### Sample Request
```
{
    "metric": "do"
}
```

### Response Schema
```
{
    "_id": string,
    "metric": string,
    "defaultMin": number,
    "defaultMax": number
}
```

### Sample Success Response
```
{
    "text": {
        "_id": "644b277a35869a94d14ea5e5",
        "metric": "dissolvedOxygen",
        "defaultMin": 60,
        "defaultMax": 70,
        "__v": 0
    }
}
```

### Fail Response
Failure Code 400:
```
{ message: "Invalid request: metric is required." }
```

Failure Code 500:
```
{ message: "There was an error with the request." }
```