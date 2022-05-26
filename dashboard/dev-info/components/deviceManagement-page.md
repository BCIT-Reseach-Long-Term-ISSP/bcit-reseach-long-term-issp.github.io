---  
layout: default  
title: Device Management Page Components
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/device-management-page
---  

# Device Management Page Components
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Device Management Page

Device Management page contains components that helps the user to edit device name, thresholds for entities measured by buoys, buoy name, and buoy location.

**Props used:**
- *latitude*: The latitude of the selected device.
- *longitude*:The longitude of the selected device. 
- *name*: The name of the buoy selected.
- *colour*: The selected colour for the buoy selected.
- *threshold*: The threshold for the selected entity of the buoy.
- *value*: The threshold value.
- *updateDevice*: Saves the changes made for the selected device.

**Functions implemented:**

## DeviceManageEditSection
DeviceManageEditSection is a component that displays the available buoys that are transmitting data.

**Props used:**
- *device*: Contains information of the selected buoy that contains information such as device id, latitude, longitude, colour assigned to the buoy etc.
- *db*: The database object.
- *children*: The different options provided for the user to edit in a device.  

## DeviceManagePanel
DeviceManagePanel is a component helps change the name, colour, latitude, longitude, threshold, and the message that is being sent in by the devices.

**Props used:**
- *device*: Contains information of the selected buoy that contains information such as device id, latitude, longitude, colour assigned to the buoy etc.
- *children*: The different options provided for the user to edit in a device.  
  
## EditLocation
EditLocation is a component that gets used in deviceManagePanel. This component helps in setting the latitude and longitude for the selected buoy.

**Props used:**
- *latitude*: The latitude of the selected device.
- *longitude*:The longitude of the selected device. 

## EditName
EditName is a component that gets used in deviceManagePanel. This component helps in changing the assigned name for a buoy.

**Props used:**
- *name*: the name assigned to the selected device.

## EditThresholds
EditThresholds is a component that gets used in deviceManagePanel. This component helps in changing the assigned threshold for an entity that's being measured by the buoy.

**Props used:**
- *thresholds*: The assigned thresholds to the selected device.
- *deviceId*: The id assigned to the selected device.

## EditThresholdValue
EditThresholdValue is a component that gets used in deviceManagePanel. This component helps in assigning values to a threshold entity.

**Props used:**
- *value*: The value of threshold to the selected device.
- *metric*: The metric of the selected entity.
- *type*: The kind of entity selected.

# SaveChangesButton 
SaveChangesButton is a component that gets used in deviceManagePanel. This component helps in saving all the changes made by the user in the deviceManagePanel.

**Props used:**
- *updateDevice*: Updates the changes made to the selected device.

{: .fs-6 .fw-300 }