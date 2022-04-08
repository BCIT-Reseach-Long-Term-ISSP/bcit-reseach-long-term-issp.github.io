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
    - These devices should have an "id", "longitude", "latitude", and "name" field.

**Functions implemented:**
- *getSelected*: Takes a device as an argument and returns a green colour or a black colour value depending on whether that device's id is in selectedDevices.
    - This is used in the MapMarker component to determine the colour.
- *condUpdateSelDevices*: Takes a device as an argument and adds or removes that device from the selectedDevices list depending on whether it's already present.
    - This is used in the MapMarker component so that a MapMarker can be clicked on to select/deselect a device.

**Noteworthy components used:**
- *Map*: A component from react-map-gl which renders a Mapbox map. More information [here](/docs/dashboard/react/react-map-gl).
- *MapMarker*: A component which renders a marker on the map. More information in the MapMarker section of this page.
- *MapSelectedDevices*: A component which renders a list of selected devices on the map page. More information in the MapSelectedDevices section of this page.


{: .fs-6 .fw-300 }