---  
layout: default  
title: Warnings
has_children: false  
permalink: /docs/dashboard/v2-2022/warnings
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: true
---  

# Warnings
{: .no_toc }

This page contains information about the "warnings" functionality, and the components that pertain to the warnings tab of the notifications/manage device page.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Warnings

A warning in the dashboard essentially covers any information of note pertaining to each individual device.

Currently, there are three types of warnings:
- At least one reading within the last 72 hours has gone above the max threshold for that device
- At least one reading within the last 72 hours has gone below the min threshold for that device
- No readings have been made in the last 2 hours

These warnings help to indicate to the user when something potentially alarming has happened in the water, or to the device.

Currently, warnings are only grabbed on page refresh. This is due to the number of queries involved currently.

Please note that, at the current time, grabbing warnings has a bit of a delay, so they will not show up immediately.

## Grabbing warnings/App's warning state

Warnings are grabbed in the App component, primarily using a function named "getAllWarnings". They are then stored in the App component's in the warning state, because components in multiple pages require that data.

Warnings are checked for each device that has device information in the Firestore.

The warnings state will be one of three values, each with its own meaning:
- *undefined*: Warnings have not been grabbed yet.
- *true*: Warnings are in the process of being grabbed.
- *(Some object)*: Warnings have been grabbed; this object contains that information on the warnings. Note that if no devices have any warnings, this object will be empty.

Promises are created to make queries to the AWS via the API to see if thresholds have been broken, and to check if readings have been made in the last 2 hours. These promises are all added to an array to ensure that all devices have been checked for warnings before any further actions are taken. Once all promises are resolved, however, the App component's "warnings" state is updated with the warnings data.

## Map's indicator for warnings

The map indicates that a device has warning(s) by putting a small red circular notification badge in the top left of a device's marker. This is done by checking the warnings state via the getNotification function in the MapMarker component.

## WarningsTab

The WarningsTab component is a component to be used in the warnings tab of the notifications/manage device page.

It displays the message "Grabbing warnings..." when warnings are in the process of being grabbed; if warnings have been grabbed, however, it displays these warnings, grouped by device.

**Props used:**
- *warnings*: The warnings state, passed down from the App component. This contains information pertaining to which devices have warnings, and what type of warning it is.
    - Example: `{"1": {"over": [LIST OF WARNINGS HERE], "under": [LIST OF WARNINGS HERE]}, "2": {"activity": [LIST OF WARNINGS HERE]}}`
- *getDeviceFromId*: Takes a device id as an argument and returns the device from the deviceList which has that id.

## WarningsMessage

The WarningsMessage component renders as a message box with information pertaining to a device's warnings. It has a header with the device's name and ID, and its body contains the messages relating to the warnings themselves.

The body of the component solely contains the children of the element. An example is this: `<WarningsMessage>(Child elements go here)</WarningsMessage>`.

**Props used:**
- *device*: An object representing a device.
- *children*: The children of the element (an example can be found above).

{: .fs-6 .fw-300 }