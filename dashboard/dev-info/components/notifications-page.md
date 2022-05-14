---  
layout: default  
title: Notifications Page Components
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/notifications-page
---  

# Notifications Page Components
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Notification Page

Notifications Page is a component that contains sub-components that display device data, gives users ability to adjust thresholds, and alerts the user for any spikes or dips in the data collected by the devices.

**Props used:**
No props are being currently used as the component isn't fully functional yet.

**Functions implemented:**
- *fetchAllSensorIds*:Takes no arguments. Calls the API responsible for getting Ids of all the active devices. 
    - This function is used in useEffect and in the current layout, it helps set up a hook(allSensorIds) which is used in other functions.
- *fetchSensorCurrentDetails*: Takes sensor Id as an argument, makes API call for that particular device and gets all the data that was collected by it. 
    - This function will be used to update device details in the Sensor Details Tab (currently not fully functional).
- *fetchAllSensorsCurrentDetails*: Similar to fetchSensorCurrentDetails, but gets data for all the devices all at once. The reason for having this function is that it might be beneficial to grab all the data in one go, so tests can be performed using this function.  
    - Currently, this function is not being used.
- *sensorDetails*: Takes the hook(allSensorIds) as an argument. displays data for each device in the Sensor Details tab. fetchSensorCurrentDetails gets called within this function but the function call is currently not working.
    - This is used to generate sub-components to populate the Sensor Details tab.
- *assignedThresholds*: Takes the hook(allSensorIds) as an argument. Currently, only the devices dropdown is being populated dynamically, and the rest is hardcoded. However, once fully functional, this tab will help users adjust thresholds for all the active devices.

{: .fs-6 .fw-300 }"