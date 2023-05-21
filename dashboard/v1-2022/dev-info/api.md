---  
layout: default  
title: Dashboard API  
has_children: false  
permalink: /docs/dashboard/api
parent: Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
---  

# Dashboard API
{: .no_toc }

An API which the dashboard uses for grabbing data from the cloud can be found in the timestreamDB folder of the dashboard repository, in the server.js file.
Below are the endpoints which the API implements.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
   
---

## /id-list

The /id-list endpoint is a GET request. It simply returns a list of the device ids which are in the cloud. It does not take anything in the body, nor any parameters.

**Output format:**
- `[{"buoy_id": "string"}]`

**Example results:**
- `[{"buoy_id":"1"}, {"buoy_id":"12"}, {"buoy_id":"2"}, {"buoy_id":"3"}, {"buoy_id":"8"}]`


## /current

The /current endpoint is a GET request. It returns the most current readings for given devices for all device measures.

**Parameters taken:**
- *buoyId*: Comma separated device ids. The device ids provided determine which devices' readings are grabbed.
    - Example: 2,3

**Output format:**
- `[{"buoy_id": "string", "measure_name": "string", "time": "string", "measure_value::double": "string", "measure_value::boolean": "string"}]`

**Example results:**
- /current/?buoyId=1
    - `[{"buoy_id":"1","measure_name":"do","time":"2022-04-08 04:54:02.650000000","measure_value::double":"74.61","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"ec","time":"2022-04-08 04:54:02.650000000","measure_value::double":"260.0","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"liqlev","time":"2022-04-08 04:54:02.650000000","measure_value::double":null,"measure_value::boolean":"true"},
      {"buoy_id":"1","measure_name":"ph","time":"2022-04-08 04:54:02.650000000","measure_value::double":"7.96","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"tbd","time":"2022-04-08 04:54:02.650000000","measure_value::double":"0.81","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"tds","time":"2022-04-08 04:54:02.650000000","measure_value::double":"590.71","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"temp","time":"2022-04-08 04:54:02.650000000","measure_value::double":"17.7","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"wf","time":"2022-04-08 04:54:02.650000000","measure_value::double":"2.01","measure_value::boolean":null},
      {"buoy_id":"1","measure_name":"wp","time":"2022-04-08 04:54:02.650000000","measure_value::double":"8.58","measure_value::boolean":null}]`
- /current/?buoyId=2,3
    - `[{"buoy_id":"2","measure_name":"do","time":"2022-04-08 04:57:05.785000000","measure_value::double":"78.78","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"ec","time":"2022-04-08 04:57:05.785000000","measure_value::double":"271.86","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"liqlev","time":"2022-04-08 04:57:05.785000000","measure_value::double":null,"measure_value::boolean":"true"},
      {"buoy_id":"2","measure_name":"ph","time":"2022-04-08 04:57:05.785000000","measure_value::double":"7.45","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"tbd","time":"2022-04-08 04:57:05.785000000","measure_value::double":"0.75","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"tds","time":"2022-04-08 04:57:05.785000000","measure_value::double":"596.87","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"temp","time":"2022-04-08 04:57:05.785000000","measure_value::double":"23.02","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"wf","time":"2022-04-08 04:57:05.785000000","measure_value::double":"2.09","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"wp","time":"2022-04-08 04:57:05.785000000","measure_value::double":"11.14","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"do","time":"2022-03-25 04:45:52.011000000","measure_value::double":"80.3","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"ec","time":"2022-03-25 04:45:52.011000000","measure_value::double":"250.21","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"liqlev","time":"2022-03-25 04:45:52.011000000","measure_value::double":null,"measure_value::boolean":"true"},
      {"buoy_id":"3","measure_name":"ph","time":"2022-03-25 04:45:52.011000000","measure_value::double":"7.03","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"tbd","time":"2022-03-25 04:45:52.011000000","measure_value::double":"0.8","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"tds","time":"2022-03-25 04:45:52.011000000","measure_value::double":"550.96","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"temp","time":"2022-03-25 04:45:52.011000000","measure_value::double":"20.34","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"wf","time":"2022-03-25 04:45:52.011000000","measure_value::double":"1.904","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"wp","time":"2022-03-25 04:45:52.011000000","measure_value::double":"9.81","measure_value::boolean":null}]`


## /historical

The /historical endpoint is a GET request. It returns historical data for given devices between a start and end date for a given device measure.

**Parameters taken:**
- *buoyId*: Comma separated device ids. The device ids provided determine which devices' readings are grabbed.
    - Example: 2,3
- *measureName*: The name of the measure for which readings are grabbed.
    - Example: ph
- *start*: The start date and time in ISO 8601 format.
    - Example: 2022-03-30T03:42:32.000Z
- *end*: The end date and time in ISO 8601 format.

**Output format:**
- `[{"buoy_id": "string", "measure_name": "string", "time": "string", "measure_value::double": "string", "measure_value::boolean": "string"}]`

**Example results:**
- /historical/?buoyId=1&measureName=ph&start=2021-03-30T03:42:32.000Z&end=2022-03-30T03:42:32.000Z
    - `[{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null}]`
- /historical/?buoyId=2,3&measureName=ph&start=2021-03-30T03:42:32.000Z&end=2022-03-30T03:42:32.000Z
    - `[{"buoy_id":"2","measure_name":"ph","time":"2022-03-25 04:45:49.319000000","measure_value::double":"7.03","measure_value::boolean":null},
      {"buoy_id":"3","measure_name":"ph","time":"2022-03-25 04:45:52.011000000","measure_value::double":"7.03","measure_value::boolean":null},
      {"buoy_id":"2","measure_name":"ph","time":"2022-03-25 04:46:58.025000000","measure_value::double":"7.03","measure_value::boolean":null}]`


## /threshold

The /threshold endpoint is a GET request. It returns data for given devices between a start and end date for a given device measure, but only data points that meet a given "threshold."

**Parameters taken:**
- *buoyId*: Comma separated device ids. The device ids provided determine which devices' readings are grabbed.
    - Example: 2,3
- *measureName*: The name of the measure for which readings are grabbed.
    - Example: ph
- *start*: The start date and time in ISO 8601 format.
    - Example: 2022-03-30T03:42:32.000Z
- *end*: The end date and time in ISO 8601 format.
- *measureValueType*: The measure value type for a given metric.
    - This will always either be measure_value::double or measure_value::boolean.
- *threshold*: A comparator and a number.
    - The measure values will only be grabbed if they meet the threshold set by the comparator.
    - Example: If the threshold is set to >5, the only data points which will be retrieved will be those which have a measure_value greater than 5.

**Output format:**
- `[{"buoy_id": "string", "measure_name": "string", "time": "string", "measure_value::double": "string", "measure_value::boolean": "string"}]`

**Example results:**
- /threshold/?buoyId=1,8&measureName=ph&start=2021-03-30T03:42:32.000Z&end=2022-03-30T03:42:32.000Z&measureValueType=measure_value::double&threshold=>5
    - `[{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null},
      {"buoy_id":"8","measure_name":"ph","time":"2022-03-25 04:45:44.780000000","measure_value::double":"7.03","measure_value::boolean":null}]`

{: .fs-6 .fw-300 }