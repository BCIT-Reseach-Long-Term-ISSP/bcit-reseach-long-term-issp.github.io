---  
layout: default  
title: Data Page Components
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/data-page
---  

# Data Page Components
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## SingleDevicePage

SingleDevicePage is a component which renders the entirety of the data page for a single device.

**Props used:**
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]

**Functions implemented:**
None

**Noteworthy components used:**
- *TabsSection*: The tabbed component of the page. Renders data collected from the device selected.
- *MapWidget*: A component which renders a minimap.
- *WeatherWidget*: A component which renders the current weather display.
- *TidesWidget*: A component which renders the tide forecast display.
- *DeviceDescription*: A component which renders a short description of the selected device.

## TabsSection

TabsSection is the tabbed component of the data page. Displays data collected from the device selected.

**Props used:**
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]

**Functions implemented:**
- *apiCall*: Does not take any arguments. Makes an API call to the cloud data for current readings from the selected device.

**Noteworthy components used:**
- *Tabs/Tab*: Components from React Bootstrap which renders a tabbed layout. More information [here](/docs/dashboard/react/react-bootstrap).
- *OverviewDataDisplay*: A component which renders the current reading for a single metric measured by the device selected.
- *QuantitativeDetails*: A component which renders a detailed look at quantitative data collected for a specific metric for the device selected.
- *QualitativeDetails*: A component which renders a detailed look at qualitative data collected for a specific metric for the device selected.

## OverviewDataDisplay

OverviewDataDisplay is a component which renders the current reading for a single metric measured by the device selected.

**Props used:**
- *data*: The data for display as an onbect, taken from the API response.
    - Example: {"buoy_id":"1","measure_name":"do","time":"2022-04-08 03:53:02.625000000","measure_value::double":"83.61","measure_value::boolean":null}
- *isWithinThreshold*: A boolean indicating whether or not the value given in the data prop is within the set threshold.

**Functions implemented:**
None

**Noteworthy components used:**
None

## QuantitativeDetails

QuantitativeDetails is a component which renders a detailed look at quantitative data collected for a specific metric for the device selected.

**Props used:**
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]
- *metric*: A string. The shorthand for the metric being displayed.
    - Example: "do"

**Functions implemented:**
- *padDate*: Takes an integer as an argument and returns a string that is padded by a zero if the integer is a single digit.
    - This is used as a helper to prepare the time readings for display on the graph.
- *stringifyDate*: Takes a Date object as an argument and returns a custom formatted string of the date.
    - This is used to prepare the time readings for display on the graph.
- *applyRange*: Does not take any arguments. Changes the rangeStart and rangeEnd states to their corresponding dates as per the selection indicated by the calendar.
    - This is used to change the date range of data being displayed
- *handleTimeClick*: Handles the selection at the time range dropdown. Changes the main text on the time range dropdown to indicate the current selection and toggles the range selection menu accordingly. Sets the time range if one of the preset values are selected.
    - This is used for the time range dropdown menu.
- *handleThresholdClick*: Handles the selection at the threshold dropdown. Changes the main text on the threshold dropdown to indicate the current selection and toggles the range selection menu accordingly.
    - This is used for the threshold dropdown menu.
- *handleThresholdStartEntry*: Handles the text entry for selecting the start of the threshold range.
    - This is used to set the start of the threshold range.
- *handleThresholdEndEntry*:  Handles the text entry for selecting the end of the thrwshold range.
    - This is used to set the end of the threshold range.
- *submitThreshold*: Does not take any arguments. Validates whether the text entries are valid (must be a number) and filters the data according to the entered range.
    - This is used to prepare the data for use in the DataTable and DataDownloadButton components.

**Noteworthy components used:**
- *Graph*: A component that renders historical data for the selected metric on a line graph.
- *DropdownButton*: A component from React Bootstrap which renders a dropdown menu for selecting time range and threshold options. More information [here](/docs/dashboard/react/react-bootstrap).
- *DatePicker*: A component from React DatePicker which renders a calendar datepicker for selecting a time range. More information [here](/docs/dashboard/react/react-bootstrap). 
- *DataDownloadButton*: A component that renders the data download button which allows data to be downloaded as a .csv file. Renders the file's corresponding file name.
- *DataTable*: A component that renders a data table displaying raw historical data within the selected date and threshold ranges.


## QualitativeDetails

QualitativeDetails is a component which renders a detailed look at qualitative data collected for a specific metric for the device selected.

**Props used:**
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]
- *metric*: A string. The shorthand for the metric being displayed.
    - Example: "do"

**Functions implemented:**
- *padDate*: Takes an integer as an argument and returns a string that is padded by a zero if the integer is a single digit.
    - This is used as a helper to prepare the time readings for display on the graph.
- *stringifyDate*: Takes a Date object as an argument and returns a custom formatted string of the date.
    - This is used to prepare the time readings for display on the graph.
- *applyRange*: Does not take any arguments. Changes the rangeStart and rangeEnd states to their corresponding dates as per the selection indicated by the calendar.
    - This is used to change the date range of data being displayed
- *handleTimeClick*: Handles the selection at the time range dropdown. Changes the main text on the time range dropdown to indicate the current selection and toggles the range selection menu accordingly. Sets the time range if one of the preset values are selected.
    - This is used for the time range dropdown menu.
- *handleThresholdClick*: Handles the selection at the threshold dropdown. Changes the main text on the threshold dropdown to indicate the current selection and toggles the range selection menu accordingly.
    - This is used for the threshold dropdown menu.
- *handleThresholdStartEntry*: Handles the text entry for selecting the start of the threshold range.
    - This is used to set the start of the threshold range.
- *handleThresholdEndEntry*:  Handles the text entry for selecting the end of the thrwshold range.
    - This is used to set the end of the threshold range.
- *submitThreshold*: Does not take any arguments. Validates whether the text entries are valid (must be a number) and filters the data according to the entered range.
    - This is used to prepare the data for use in the DataTable and DataDownloadButton components.

**Noteworthy components used:**
- *DropdownButton*: A component from React Bootstrap which renders a dropdown menu for selecting time range and threshold options. More information [here](/docs/dashboard/react/react-bootstrap).
- *DatePicker*: A component from React DatePicker which renders a calendar datepicker for selecting a time range. More information [here](/docs/dashboard/react/react-bootstrap). 
- *DataDownloadButton*: A component that renders the data download button which allows data to be downloaded as a .csv file. Renders the file's corresponding file name.
- *DataTable*: A component that renders a data table displaying raw historical data within the selected date and threshold ranges. Readings exceeding the set thresholds will appear as red.

## Graph

Graph is a component that renders historical data for the selected metric on a line graph.

**Props used:**
- *deviceId*: A list of one ID corresponding to devices which the user has selected for viewing.
    - Example: ["1"]
- *metric*: A string. The shorthand for the metric being displayed.
    - Example: "do"
- *graphData*: An array of objects containing a date string and a value float.
    - Ezample: [{time: "2022-03-24 03:50", value: 21.4}, {time: "2022-03-25 11:30", value: 20.0}]

**Functions implemented:**
None

**Noteworthy components used:**
- *Line*: A component from react-chartjs-2 which renders a line graph displaying the data from the graphData prop. More information [here](/docs/dashboard/react/react-chartsjs-2). 

## DataDownloadButton

DataDownloadButton is a component that renders the data download button which allows data to be downloaded as a .csv file. Renders the file's corresponding file name.

**Props used:**
- *data*: An array of objects containing historical data of measurements to be turned into a csv file for download.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null},{"buoy_id":"1","measure_name":"ph","time":"2022-03-31 23:03:36.231000000","measure_value::double":"7.86","measure_value::boolean":null}]
- *start*: An ISO 8601 format string indicating the start of the date range for the data.
    - Example: "2022-03-25T00:00:00.000Z"
- *end*: An ISO 8601 format string indicating the end of the date range for the data.
    - Example: "2022-04-01T00:00:00.000Z"

**Functions implemented:**
- *isUnique*: Returns true if a value from an array of objects is unique. Returns false otherwise.
    - This is used along with the filter() method to make an array of unique device IDs and an array of unique metric types.
- *parseList*: Takes an array of strings as an argument and returns a formatted string summarizing the data prop details.
    - This is used to name the csv file being downloaded.

**Noteworthy components used:**
- *CSVLink*: A component from react-csv which generates a csv from the data prop and renders a button to download it. More information [here](/docs/dashboard/react/react-csv). 

## DataTable

DataTable is a component that renders a data table displaying raw historical data within the selected date and threshold ranges. Readings exceeding the set thresholds will appear as red.

**Props used:**
- *data*: An array of objects containing historical data of measurements to be displayed as a table.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null},{"buoy_id":"1","measure_name":"ph","time":"2022-03-31 23:03:36.231000000","measure_value::double":"7.86","measure_value::boolean":null}]

**Functions implemented:**
None

**Noteworthy components used:**
None


## MapWidget

The MapWidget component is a small map display meant to be used on the devices page along with the other widgets of that page.

It displays a single marker for a single given device. 

**Props used:**
- *device*: An object representing a device.
    - This device is needed to be passed as a prop into MapMarker.

**Noteworthy components used:**
- *MapMarker*: A component which renders a marker on the map. More information [here](/docs/dashboard/react/map-page#mapmarker).
    - The getSelected and condUpdateSelDevices props given by the MapWidget are dummy functions that are essentially given just to prevent issues.


## WeatherWidget

WeatherWidget is a component which renders the current weather display with data from WeatherAPI.com.

**Props used:**
None

**Functions implemented:**
None

**Noteworthy components used:**
None

## TidesWidget

TidesWidget is a component which renders the tide forecast display with data from tides.gc.ca.

**Props used:**
None

**Functions implemented:**
- *padTime*: Takes an integer as an argument and returns its string equivalent, padded with a zero if a single digit.
    - This is used to prepare the time information for display.
- *getTime*: Takes a date as an argument and ISO 8601 format string and returns a formatted time string for display.
    - This is used to prepare the time information for display.
- *assignHighLow*: Takes the data (an array of objects) from the tide API as an argument and adds a new string value indicating whether that reading is for a high or low tide.

**Noteworthy components used:**
None

## DeviceDescription

DeviceDescription is a component which renders a short description of the selected device.

**Props used:**
- *data*: An object containing data pertaining to the device, such as id, battery level, and connectivity. Currently using dummy data.

**Functions implemented:**
None

**Noteworthy components used:**
None

{: .fs-6 .fw-300 }