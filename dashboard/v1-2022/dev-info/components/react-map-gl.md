---  
layout: default  
title: react-map-gl  
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/v2-2022/react-map-gl
---  

# react-map-gl
{: .no_toc }

react-map-gl is a suite of components which are geared towards Mapbox in React. The website for it can be found [here](https://visgl.github.io/react-map-gl/).

Below are components which are used within the dashboard. Please note that some components may take props which are unlisted here; the props listed here are merely the ones used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
   
---

## Map

Map is a component which renders a Mapbox map.

**Props used:**
- *initialViewState*: An object containing a "longitude", "latitude", and "zoom" key/value pair.
    - Longitude and latitude correspond to coordinates, and zoom defines how zoomed in the map view is by default.
    - *Example*: { longitude: -123.17557, latitude: 49.195007, zoom: 13.35 }
- *mapStyle*: A string which corresponds to a Mapbox style's URL.
    - A list of Mapbox styles can be found [here](https://docs.mapbox.com/api/maps/styles/).
    - The maps on the dashboard currently use "mapbox://styles/mapbox/streets-v9".


## Marker

Marker is a component which renders a marker within a Map component. Marker components are nestled within a Map component, like so: <Map><Marker/></Map>.

Additionally, the contents of a Marker component create the visual for the marker; there is no inherent visual for the Marker component. For example, a Marker component which shows as the word "Hello" could be created like so: <Marker><p>Hello</p></Marker>.

Both examples above have omitted the props which Map and Marker take for simplicity.

**Props used:**
- *latitude*: A number; the latitude at which the marker will display on the map.
- *longitude*: A number; the longitude at which the marker will display on the map.
- *draggable*: A boolean; determines whether the marker can be dragged.


## Extra Notes

When building the React project, certain versions of Mapbox can have issues with certain versions of React, which causes the map to fail to render.

This issue was affecting the dashboard, and the console.log was revealing that it was an issue with the transpiler when building. The solution we used, found [here](https://stackoverflow.com/a/69489231), involves exempting it from processes of transpilation.

In files where react-map-gl's Map is used, such as mapPage.jsx, you'll notice these 4 lines:

```js
import mapboxgl from 'mapbox-gl';
// @ts-ignore
// eslint-disable-next-line import/no-webpack-loader-syntax, import/no-unresolved
mapboxgl.workerClass = require('worker-loader!mapbox-gl/dist/mapbox-gl-csp-worker').default;
```

Without these lines, the map will fail to render. The comments are also part of this, and should not be removed, nor modified.

It's possible that this doesn't need to be present in every instance where the Map is used, but we included it in all just to be safe.

{: .fs-6 .fw-300 }