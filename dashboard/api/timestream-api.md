---
layout: default
title: Timestream /api/ts
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/ts
nav_order: 1
---

# Timestream
{: .no_toc }
**Base route**: `/api/ts`
{: .fs-6 .fw-300 }
The Timestream API utilizes AWS Timestream to retrieve real-time device sensor data.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

|💡 To set up the testing environment using Postman, refer to the [Setting up testing section](/docs/dashboard/backend/aws-timestream#setting-up-testing-with-postman) of the back-end documentation.|



# /getAllBuoyIds

| <b>Description</b>    | Get all device ids that exist on the table. |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 404, 500 |
| <b>Request Schema</b> | N/A |
| <b>Sample Request</b> | N/A |

### Response Schema
```
{ 
    "data": 
    [{
        "“buoy_id”": string,
    }]
}
```
### Sample Success Response

```
{ 
    "data": 
    [
        {"buoy_id":"0"},
        {"buoy_id":"1"},
        {"buoy_id":"100"}
    ]
}
``` 
### Fail Response 
```
{ 
    "error": 
    { 
        "message": "queryString is null or empty" 
    }
}
```

# /getCurrentBuoyData

| <b>Description</b>    | Get all data from specified list of buoy ids (query string). |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 404, 500 |
| <b>Request Schema</b> | `buoyIdList: string` |
| <b>Sample Request</b> | `buoyIdList: 1,2,3,4,5,12` |

### Response Schema 
```
{
    data: [
        {
             “buoy_id”: string,
             "measure_name": string,
             "time": from_iso8601_timestamp,
             "measure_value::double": double,
             "measure_value::boolean": boolean,
             "measure_value::varchar": boolean,
        },
    ]
}
```

### Sample Success Response
```
{
    data: [
        {
             “buoy_id”: 1,
             "measure_name": "do",
             "time": "2023-02-18 01:38:08.480000000",
             "measure_value::double": "80.3",
             "measure_value::boolean": null,
             "measure_value::varchar": null,
        },
    ]
}
```

If no match with query parameters:

```
{
    data: [ ]
}
```

### Fail Response
If the query is empty:
```
{
    "error": 
    { 
        "message": "queryString is null or empty" 
    }
}
```


# /getBuoyHistory

| <b>Description</b>    | Get historical data from buoys |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 404, 500 |
| <b>Request Schema</b> | `{ “userId”: string, “deviceId”: number }` |
| <b>Sample Request</b> | `{ buoyIdList:1,12,8, measureName:ph, start:2021-03-30T03:42:32.000Z, end:2022-03-30T03:42:32.000Z }` |


### Response Schema
```
{
    "data": [
        {
            "buoy_id": string,
            "measure_name": string,
            "time": from_iso8601_timestamp,
            "measure_value::double": typeof measure_value,
            "measure_value::boolean": boolean,
            "measure_value::varchar": boolean
        }
    ]
}
```

### Sample Success Response
```
{
    "data": [
        {
            "buoy_id": "1",
            "measure_name": "ph",
            "time": "2022-03-25 04:45:06.865000000",
            "measure_value::double": "7.03",
            "measure_value::boolean": null,
            "measure_value::varchar": null
        },
        {
            "buoy_id": "12",
            "measure_name": "ph",
            "time": "2022-03-25 04:45:40.124000000",
            "measure_value::double": "7.03",
            "measure_value::boolean": null,
            "measure_value::varchar": null
        },
        {
            "buoy_id": "8",
            "measure_name": "ph",
            "time": "2022-03-25 04:45:44.780000000",
            "measure_value::double": "7.03",
            "measure_value::boolean": null,
            "measure_value::varchar": null
        }
    ]
}
```

### Fail Response
If the query is empty:
```
{
    "error":
    {
        "message":"queryString is null or empty"
    }
}
```

# /getBuoyThreshold

| <b>Description</b>    | Get information on whether any of the specified devices have metrics that have passed a threshold. |
| <b>HTTP Verb</b>      | GET       |
| <b>Success Codes</b>  | 200       |
| <b>Failure Codes</b>  | 404, 500  |

### Request Schema
```
{
    buoyIdList:  string
    measureName:  string
    start: from_iso8601_timestamp
    end:  from_iso8601_timestamp
    measureValueType:  typeof measure_value
    threshold:  Number 
}
```
Note: in typescript a comparator and number combined is of type Number

### Sample Request
```
{
    buoyIdList:  1,8   
    measureName:  ph
    start:  2021-03-30T03:42:32.000Z
    end:  2022-03-30T03:42:32.000Z
    measureValueType:  measure_value::double
    threshold:  >5 
}
```

### Response Schema
```
{
    "data": [
        {
            "buoy_id": string,
            "measure_name": string,
            "time": string,
            "measure_value::double": double,
            "measure_value::boolean": boolean,
            "measure_value::varchar": boolean
        }
    ]
}
```
### Sample Success Response
```
{
    "data": [
        {
            "buoy_id": "1",
            "measure_name": "ph",
            "time": "2022-03-25 04:45:06.865000000",
            "measure_value::double": "7.03",
            "measure_value::boolean": null,
            "measure_value::varchar": null
        },
        {
            "buoy_id": "8",
            "measure_name": "ph",
            "time": "2022-03-25 04:45:44.780000000",
            "measure_value::double": "7.03",
            "measure_value::boolean": null,
            "measure_value::varchar": null
        }
    ]
}
```

If no match with query parameters:

```
{
    data: [ ]
}
```

### Fail Response
If the query is empty:
```
{
    "error":
    {
        "message": "queryString is null or empty"
    }
}
```
