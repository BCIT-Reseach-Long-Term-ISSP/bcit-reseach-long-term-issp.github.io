---  
layout: default  
title: Map Page Components
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/map-page
---  

# Map Page Components
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## MapPage

MapPage is a component which renders the entirety of the map page.

**Props used:**
- *selectedDevices*: A list of IDs corresponding to devices which the user has selected.
    - Example: ["1", "9", "3"]
- *updateSelectedDevices*: A function which can be used to overwrite the selectedDevices list.
    - This function is used in another function, *condUpdateSelDevices*, which either adds or removes a given device from the list depending on whether it's already present.
- *deviceList*: A list of all devices in the system.
    - These devices should have an "id", "longitude", "latitude", and "name" value.

**Functions implemented:**
- *getSelected*: Takes a device as an argument and returns a green colour or a black colour value depending on whether that device's id is in selectedDevices.
    - This is used in the MapMarker component to determine the colour.
- *condUpdateSelDevices*: Takes a device as an argument and adds or removes that device from the selectedDevices list depending on whether it's already present.
    - This is used in the MapMarker component so that a MapMarker can be clicked on to select/deselect a device.

**Noteworthy components used:**
- *Map*: A component from react-map-gl which renders a Mapbox map. More information [here](/docs/dashboard/react/react-map-gl).
- *MapMarker*: A component which renders a marker on the map. More information in the MapMarker section of this page.
- *MapSelectedDevices*: A component which renders a list of selected devices on the map page. More information in the MapSelectedDevices section of this page.


## MapMarker

MapMarker is a component which renders a pin marker on the map for a device's location. 

Its color is black if the device is not selected, and green if selected. It has a red circle in the top left corner if the device has a notification.

MapMarkers should be nestled within the Map component, like so: <Map><MapMarker /></Map>. The props given to Map and MapMarker in that example have been omitted for simplicity.

**Props used:**
- *device*: An object representing a device. This device object should have an "id", "longitude", "latitude" value.
- *getSelected*: A function which takes a device object as an argument and returns a colour value for the device. More information under MapPage's "functions implemented" section.
- *condUpdateSelDevices*: A function which takes a device object as an argument and selects/deselects the device. More information under MapPage's "functions implemented" section.

**Functions implemented:**
- *getNotification*: Takes a device as an argument and returns either a red CircleFill component (representing a notification badge) or undefined.
    - getNotification's functionality is not currently implemented, and so it always returns a notification badge for devices with id 3 or 9, and no other device.

**Noteworthy components used:**
- Marker: A component from react-map-gl which renders a marker on the map. More information [here](/docs/dashboard/react/react-map-gl).
- CircleFill: A component from react-bootstrap-icons which renders a filled circle. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- GeoAltFill: A component from react-bootstrap-icons which renders a map pin. More information [here](/docs/dashboard/react/react-bootstrap-icons).

{: .fs-6 .fw-300 }