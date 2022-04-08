---  
layout: default  
title: Usage  
has_children: false  
permalink: /docs/dashboard/usage  
parent: Dashboard  
has_toc: true
---  

# Getting Started / Setup 

This section contains information about how to use the dashboard to see information.

To begin, we must first start our react app by navigating to the root directory of the project/app, and entering this command in your terminal:
```npm start```

**1.** Navigate to localhost:3000, where you will be greeted by the map page.

![Landing Map Page](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Map1Selected.png?raw=true "Landing Map Page")

Here, we can select multiple different devices, and in future implementations of the dashboard, these selected devices will be moved on over to the device overview/statistic page, and we will be able to look at all of the information of the selected devices together.

![Map Page Multiple Devices](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/MapMultiSelected.png?raw=true "Map Page Multiple Devices")

## Viewing Device and Sensor Statistics

**2.** Click on the device statistic button (rightmost button) in the navbar.

![Navbar Info Page Highlighted](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/NavbarInfoHighlighted.png?raw=true "Navbar Info Page Highlighted")

Here, we can view a general statistic overview of all the sensors on a particular device. The statistics/measurements displayed are all from the latest timestamped data recording.

Furthermore, we can view the device's location on the map by looking at the widget on the top right of the page.

![Map Widget Zoomed](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/MapWidgetZoom.png?raw=true "Map Widget Zoomed")

Below this Widget, we can also view weather info in the YVR area, tide schedule, and device ID and battery level.

![Device Info Sidebar](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DeviceInfoSidebar.png?raw=true "Device Info Sidebar")

**3.** Click on any one of the several tabs at the top of the window to view a detailed graph view of a specific sensor.

![Device Info Tab Highlighted](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DeviceInfoTabHighlighted.png?raw=true "Device Info Tab Highlighted")

Here, we can view a specific sensor's data readings over a specified range of time, and we can read the current, maximum, minimum, and average readings in the specified range of time.

![Device Info Graph](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DeviceInfoGraph.png?raw=true "Device Info Graph")

We can also look at this information in table format.

![Device Info Table](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DeviceInfoTable.png?raw=true "Device Info Table")

Finally, we can export and download this data as well by clicking on "Download Data"

{: .fs-6 .fw-300 }
