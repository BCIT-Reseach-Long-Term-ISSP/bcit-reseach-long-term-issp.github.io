---
layout: default
title: Weather & Tide /api/weather
parent: API Endpoints
grand_parent: Dashboard
permalink: /docs/dashboard/api/weatherTide
nav_order: 9
---

# Weather & Tide
{: .no_toc }
**Base route**: `/api/weather`
{: .fs-6 .fw-300 }

| 📚 Read more about how Weather and Tide in [Back-end Server Architecture Weather & Tide documentation](/docs/dashboard/backend/weather-tide).|

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# /getWeather

| <b>Description</b>    | Get today’s weather and the upcoming weather 3-day weather forecast. |
| <b>HTTP Verb</b>      | GET |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 server error |
| <b>Request Schema</b> | Endpoint does not expect a request body or parameters. |
| <b>Sample Request</b> | Endpoint does not expect a request body or parameters. |

### Response Schema
```
{
    currWeather: string;
    temp: number;
    iconURL: string;
    windSpeed: number;
    windDir: string;
    windDeg: number;
    windPressure: number;
    forecast: {
            weekday: string;
            iconURL: string;
            high: number;
            low: number;
              }[];
}
```

### Sample Success Response
```
{
    "message": "Sucessfully fetched weather data.",
    "data": {
        "currWeather": "Partly cloudy",
        "temp": 12,
        "iconURL": "//cdn.weatherapi.com/weather/64x64/day/116.png",
        "windSpeed": 15.1,
        "windDir": "E",
        "windDeg": 100,
        "windPressure": 1023,
        "forecast": [
            {
                "weekday": "Wednesday",
                "iconURL": "//cdn.weatherapi.com/weather/64x64/day/176.png",
                "high": 12,
                "low": 8.5
            },
            {
                "weekday": "Thursday",
                "iconURL": "//cdn.weatherapi.com/weather/64x64/day/113.png",
                "high": 13.4,
                "low": 8.3
            },
            {
                "weekday": "Friday",
                "iconURL": "//cdn.weatherapi.com/weather/64x64/day/113.png",
                "high": 18.6,
                "low": 10.2
            }
        ]
    }
}
```

### Fail Response
```
{ message: 'There was a problem fetching the weather data.' }
```

# /getTide

| <b>Description</b>    | Get today’s tidal high and low predictions. |
| <b>HTTP Verb</b>      | GET |
| <b>Success Codes</b>  | 200 |
| <b>Failure Codes</b>  | 500 server error |
| <b>Request Schema</b> | Endpoint does not expect a request body or parameters. |
| <b>Sample Request</b> | Endpoint does not expect a request body or parameters. |

### Response Schema
```
{
    high: {
        height: number;
        time: string;
        type: string;
          }[];
    low: {
        height: number;
        time: string;
        type: string;
          }[];
    allData: {
        height: number;
        time: string;
             }[];
};
```

### Sample Success Response
```
{
    "message": "Sucessfully fetched tide data.",
    "data": {
        "high": [
            {
                "height": 0.6293349237164408,
                "time": "2023-04-26T01:13:00+00:00",
                "type": "high"
            },
            {
                "height": 0.9620231448684503,
                "time": "2023-04-26T14:15:00+00:00",
                "type": "high"
            }
        ],
        "low": [
            {
                "height": -0.9752238359409716,
                "time": "2023-04-26T07:43:00+00:00",
                "type": "low"
            },
            {
                "height": -0.35151374311279826,
                "time": "2023-04-26T20:57:00+00:00",
                "type": "low"
            }
        ],
        "allData": [
            {
                "height": 0.46,
                "time": "2023-04-26T00:00:00+00:00"
            },
            {
                "height": 0.62,
                "time": "2023-04-26T01:00:00+00:00"
            },
            {
                "height": 0.56,
                "time": "2023-04-26T02:00:00+00:00"
            },
            ...
        ]
    }
}
```

### Fail Response

| 💡 Generally, this is caused by going over the free rate limit. |

```
{ message: 'There was a problem fetching the tide data.' }
```
