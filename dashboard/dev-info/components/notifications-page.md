---  
layout: default  
title: Notifications Page Components
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

<!-- **Props used:**
No props are being currently used as the component isn't fully functional yet. -->

**Functions implemented:**
- *deviceManageEditSection*: Displays the available buoys that are transmitting data.
- *deviceManagePanel*: This component helps change the name, colour, latitude, longitude, threshold, and the message that is being sent in by the devices.
- *editLocation*: Helper function for deviceManagePanel. This function helps in setting the latitude and longitude for the selected buoy.

- *editName*:Helper function for deviceManagePanel. This function helps in changing the assigned name for a buoy.

- *editThresholds*:Helper function for deviceManagePanel. This function helps in changing the assigned threshold for an entity that's being measured by the buoy.

- *editThresholdValue*: Helper function for editThresholds. This function helps in assigning values to a threshold entity.

- *saveChangesButton*: Helper function for deviceManagePanel. This function helps in saving all the changes made by the user in the deviceManagePanel.
  
{: .fs-6 .fw-300 }