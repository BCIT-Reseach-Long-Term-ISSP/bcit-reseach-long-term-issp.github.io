---  
layout: default  
title: Other APIs  
has_children: false  
permalink: /docs/dashboard/v2-2022/api-other
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
---  

# Other APIs
{: .no_toc }

Other public APIs used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
   
---

## Weather API

An API which returns the current weather information used on the dashboard. More information can be found [here](https://www.weatherapi.com/).

**Limitations**

- The API can only be accessed through a key, which one may obtain by signing up.
- The dashboard is currently using a free plan, which allows for up to 1,000,000 calls per month for real-time weather data.
- The location currently being used is the neighbourhood of Steveston. Using exact coordinates of YVR will default the location to Vancouver.

**Example results:**
- http://api.weatherapi.com/v1/current.json?key=[YOUR_KEY_HERE]&q=steveston&aqi=yes
    - `{"location":{"name":"Steveston","region":"British Columbia","country":"Canada","lat":49.13,"lon":-123.18,"tz_id":"America/Los_Angeles","localtime_epoch":1653538108,"localtime":"2022-05-25 21:08"},"current":{"last_updated_epoch":1653534000,"last_updated":"2022-05-25 20:00","temp_c":17.0,"temp_f":62.6,"is_day":1,"condition":{"text":"Partly cloudy","icon":"//cdn.weatherapi.com/weather/64x64/day/116.png","code":1003},"wind_mph":6.9,"wind_kph":11.2,"wind_degree":150,"wind_dir":"SSE","pressure_mb":1015.0,"pressure_in":29.96,"precip_mm":0.0,"precip_in":0.0,"humidity":59,"cloud":75,"feelslike_c":17.0,"feelslike_f":62.6,"vis_km":48.0,"vis_miles":29.0,"uv":5.0,"gust_mph":13.0,"gust_kph":20.9,"air_quality":{"co":400.5,"no2":27.799999237060547,"o3":65.80000305175781,"so2":6.400000095367432,"pm2_5":9.899999618530273,"pm10":13.699999809265137,"us-epa-index":1,"gb-defra-index":1}}}`

## API for the Integrated Water Level System

The official API for the Integrated Water Level System by the government of Canada, used to obtain tide data for the dashboard. More information can be found [here](https://tides.gc.ca/en/stations/07607) and [here](https://api-iwls.dfo-mpo.gc.ca/swagger-ui/index.html?configUrl=/v3/api-docs/swagger-config#/stations/getStation).

**Limitations**

- The location currently being used is the neighbourhood of Steveston, which is the closest tide station to YVR. The id for Steveton's tide station is 5cebf1e13d0f4a073c4bbf8c.

**Example results:**
- https://api-iwls.dfo-mpo.gc.ca/api/v1/stations/5cebf1e13d0f4a073c4bbf8c/data?time-series-code=wlp-hilo&from=2022-05-26T04:15:00.000Z&to=2022-05-27T04:15:41.540Z
    - `[{"eventDate":"2022-05-26T10:22:00Z","qcFlagCode":"2","value":3.658,"timeSeriesId":"5d9dd7cf33a9f593161c404a"},{"eventDate":"2022-05-26T17:33:00Z","qcFlagCode":"2","value":1.116,"timeSeriesId":"5d9dd7cf33a9f593161c404a"},{"eventDate":"2022-05-26T23:49:00Z","qcFlagCode":"2","value":3.026,"timeSeriesId":"5d9dd7cf33a9f593161c404a"}]`

{: .fs-6 .fw-300 }