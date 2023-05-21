---  
layout: default  
title: Map Page Components
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/v2-2022/map-page
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

**States implemented:**
- *mapRef*: Holds a reference of the map. Used in the MapSelection component.
- *hasLoaded*: Indicates if the map has finished loading.
- *deviceList*: A list of all devices in the system. This is set by the useEffect inside this component, based on data grabbed from the Firestore.
    - These devices should have an "id", "longitude", "latitude", and "name" value.
- *noticeElement*: Holds the notice element which is displayed on the map. This value is null if there is no notice to be displayed.
- *areaSelectActive*: Indicates if the area select is currently enabled.
- *areaSelectDevices*: A list of all devices within the selection area.

**Props used:**
- *selectedDevices*: A list of IDs corresponding to devices which the user has selected.
    - Example: ["1", "9", "3"]
- *updateSelectedDevices*: A function which can be used to overwrite the selectedDevices list.
    - This function is used in another function, *condUpdateSelDevices*, which either adds or removes a given device from the list depending on whether it's already present.

**Functions implemented:**
- *getColouring*: Takes a device as an argument and returns a green colour, a black colour, or a blue colour value depending on whether that device's id is in selectedDevices, or whether that device is in the selection area.
    - This is used in the MapMarker component to determine the colour.
- *condUpdateSelDevices*: Takes a device as an argument and adds or removes that device from the selectedDevices list depending on whether it's already present.
    - This is used in the MapMarker component so that a MapMarker can be clicked on to select/deselect a device.

**Noteworthy components used:**
- *Map*: A component from react-map-gl which renders a Mapbox map. More information [here](/docs/dashboard/react/react-map-gl#map).
- *MapMarker*: A component which renders a marker on the map. More information in the MapMarker section of this page.
- *MapSelectedDevices*: A component which renders a list of selected devices on the map page. More information in the MapSelectedDevices section of this page.
- *MapNoticeElement*: A component which displays a status notice overtop of the map. More information in the MapNoticeElement section of this page.
- *MapSelection*: A component which allows the user to select devices by area on the map. More information in the MapSelection section of this page.


## MapMarker

MapMarker is a component which renders a pin marker on the map for a device's location. 

Its colour is black if the device is not selected, green if selected, and blue if highlighted within a selection area. It has a red circle in the top left corner if the device has a notification.

MapMarkers should be nestled within the Map component, like so: <Map><MapMarker /></Map>. The props given to Map and MapMarker in that example have been omitted for simplicity.

**Props used:**
- *device*: An object representing a device. This device object should have an "id", "longitude", "latitude" value.
- *getColouring*: A function which takes a device object as an argument and returns a colour value for the device. More information under MapPage's "functions implemented" section.
- *condUpdateSelDevices*: A function which takes a device object as an argument and selects/deselects the device. More information under MapPage's "functions implemented" section.

**Functions implemented:**
- *getNotification*: Takes a device as an argument and returns either a red CircleFill component (representing a notification badge) or undefined.
    - getNotification's functionality is not currently implemented, and so it always returns a notification badge for devices with id 3 or 9, and no other device.

**Noteworthy components used:**
- Marker: A component from react-map-gl which renders a marker on the map. More information [here](/docs/dashboard/react/react-map-gl#marker).
- CircleFill: A component from react-bootstrap-icons which renders a filled circle. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- GeoAltFill: A component from react-bootstrap-icons which renders a map pin. More information [here](/docs/dashboard/react/react-bootstrap-icons).


## MapSelectedDevices

MapSelectedDevices is a component which renders a list of the components which are currently selected. The list can be collapsed by clicking on the header. Devices can be deselected by pressing the red - button next to the device's name.

**States implemented:**
- *listOpen*: A boolean dictating whether the list is expanded or collapsed.

**Props used:**
- *selectedDevices*: A list of IDs corresponding to devices which the user has selected.
- *removeDevice*: A function which takes a device as an argument and removes said device from the selectedDevices list.
- *deviceList*: A list of all devices in the system.
- *selectOrDeselectAll*: A function which selects or deselects all devices in the system (depending on whether the devices are currently all selected).
- *areAllDevicesSelected*: Indicates whether all devices are selected or not.
- *areaSelectActive*: Indicates whether area select is active or not.
- *flipAreaSelectActive*: Inverts the current state of areaSelectActive.
- *confirmSelection*: Adds any devices within the selected area to the selectedDevices list of IDs, and turns off area select.
- *cancelSelection*: Wipes the areaSelectDevices value (stored in MapPage), and turns off area select.

**Functions implemented:**
- *collapseListStyle*: Returns an object with a style which differs depending on whether listOpen is true or false.
    - The style object returned by this function is applied to the div which holds the list of devices itself.
    - If listOpen is false, { height: 0 } will be returned, collapsing the list.
    - If listOpen is true, {} will be returned, expanding the list to its default height.
- *collapseSectionStyle*: Returns an object with a style which differs depending on whether listOpen is true or false.
    - The style object returned by this function is applied to the div which holds the entire section, including both the header and list.
    - If listOpen is false, { height: "52px" } will be returned, collapsing the section to be the size of just the header.
    - If listOpen is true, {} will be returned, expanding the section to its default height.
- *getDeviceFromId*: Takes a device id as an argument and returns the device from the deviceList which has that id.

**Noteworthy components used:**
- *MapSelectedDeviceElement*: A component which is used to render a single device's list element in the selected device list. More information in the MapSelectedDeviceElement section of this page.
- *MapSelectedDevicesFooter*: A component which renders the footer of this component. More information in the MapSelectedDevicesFooter section of this page.


## MapSelectedDeviceElement

MapSelectedDeviceElement is a component which renders a single device's list element in the list of selected devices found in MapSelectedDevices.

This element displays as a red - button, which can be used to remove the given device from the selectedDevices list, and the name of the device.

**Props used:**
- *device*: An object representing a device.
- *removeDevice*: A function which takes a device as an argument and removes said device from the selectedDevices list.

**Noteworthy components used:**
- *DashCircleFill*: A component from react-bootstrap-icons which renders a filled circle with a dash inside of it. More information [here](/docs/dashboard/react/react-bootstrap-icons).


## MapSelectedDevicesFooter

MapSelectedDevicesFooter is a component which is used to be a footer for the MapSelectedDevices component. 

It contains two options for selecting devices en masse: a select/deselect all devices button, and a button that enables a mode where the user may select devices by an area.

**Props used:**
- *selectOrDeselectAll*: A function which selects or deselects all devices in the system (depending on whether the devices are currently all selected).
- *areAllDevicesSelected*: Indicates whether all devices are selected or not.
- *areaSelectActive*: Indicates whether area select is active or not.
- *flipAreaSelectActive*: Inverts the current state of areaSelectActive.
- *confirmSelection*: Adds any devices within the selected area to the selectedDevices list of IDs, and turns off area select.
- *cancelSelection*: Wipes the areaSelectDevices value (stored in MapPage), and turns off area select.

**Noteworthy components used:**
- *BoundingBoxCircles*: A component from react-map-gl which renders a bounding box with circles in the corner. More information [here](/docs/dashboard/react/react-map-gl#marker).
- *Check2All*: A component from react-bootstrap-icons which renders two check marks. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *CheckSquare*: A component from react-bootstrap-icons which renders a check mark in a box. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *XLg*: A component from react-bootstrap-icons which renders an X. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *XSquare*: A component from react-bootstrap-icons which renders an X in a box. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *MapSelectedDevicesFooterElement*: Renders an element in the footer, with a click function. There is not anything more to this component, so it will not get its own section.


## MapSelection

MapSelection is a component which is rendered on the map, and handles the display and functionality of the area select tool, which allows users to select devices by an area.

**States implemented:**
- *markerACoords*: Holds the coords for one corner of the selection area.
- *markerBCoords*: Holds the coords for the other corner of the selection area.
- *boxCoordinateList*: Holds the coordinates required to make the lines for the selection area's box.

**Props used:**
- *mapRef*: A reference to the map. This is used to get the current longitude/latitude borders of the current map view, which is used for the starting position of the two selection markers.
- *deviceList*: A list of all devices in the system.
- *setAreaSelectDevices*: A function which sets the areaSelectDevices value (from the MapPage).

**Noteworthy components used:**
- *Source*: A react-map-gl component which renders a MapBox feature. More information [here](/docs/dashboard/react/react-map-gl)
- *Layer*: A react-map-gl component which determines the style that is used to render a source. More information [here](/docs/dashboard/react/react-map-gl#marker).
- *MapSelectionMarker*: A marker which can be dragged, and will set coordinates to its new location as it is being dragged. More information in the MapSelectionMarker section of this page.


## MapSelectionMarker

MapSelectionMarker is a component which is rendered on the map, and is displayed as a + sign. It's used to denote a corner of the map selection. 

It can be dragged, and it will call a function to update coordinates based on its new location.

**Props used:**
- *latitude*: The latitude at which the marker is displayed.
- *longitude*: The longitude at which the marker is displayed.
- *setCoords*: A function which is called to update the longitude and latitude of the marker, based on the new location of the marker upon being dragged.
    - Its argument is taken like so: setCoords({latitude: 20.324212, longitude: 57.781236})

{: .fs-6 .fw-300 }