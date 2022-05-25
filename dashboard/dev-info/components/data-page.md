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
- *selectedDevices*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]
- *getDeviceFromId*: A function which returns settings data for a specified device.

**Functions implemented:**
None

**Noteworthy components used:**
- *TabsSection*: The tabbed component of the page. Renders data collected from the device selected.
- *MapWidget*: A component which renders a minimap. Currently only renders when a single device is selected.
- *WeatherWidget*: A component which renders the current weather display.
- *TidesWidget*: A component which renders the tide forecast display.

**Currently unused component:**
- *DeviceDescription*: A component which renders a short description of the selected device; Will include battery life, connectivity information etc.


## TabsSection

TabsSection is the tabbed component of the data page. Displays data collected from the device selected.

**Props used:**
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "3", "9"]
- *getDeviceFromId*: A function which returns settings data for a specified device.

**Functions implemented:**
- *apiCall*: Does not take any arguments. Makes an API call to the cloud data for current readings from the selected device.

**Noteworthy components used:**
- *Tabs/Tab*: Components from React Bootstrap which renders a tabbed layout. More information [here](/docs/dashboard/react/react-bootstrap).
- *OverviewPanel*: A component which renders an overview display of the current data for each metric collected by a single device.
- *DetailsPanel*: A component which renders a detailed look at data collected for a specific metric for the selected devices.


## OverviewPanel

OverviePanel is a component which renders an overview display of the current data for each metric collected by a single device.

**Props used:**
- *data*: An array; the current values of all metrics being measured by the device being displayed, in the format given by the API response.
    - Example: [{"buoy_id":"1","measure_name":"do","time":"2022-04-08 03:53:02.625000000","measure_value::double":"83.61","measure_value::boolean":null}, 
                {"buoy_id":"1","measure_name":"ph","time":"2022-04-08 03:53:02.625000000","measure_value::double":"7.00","measure_value::boolean":null}]
- *deviceInfo*: An object; The settings data for the device being displayed.
    - Example: {id: '1', longitude: -123.17532845257887, latitude: 49.196525732859754, name: 'B0', thresholds: {do: {max: 30, min: 1}, ph: {max: 10, min: 6}}, colour: "#FF8AEA"}

**Functions implemented:**
None

**Noteworthy components used:**
- *OverviewDataDisplay*: A component which renders the current reading for a single metric measured by a single device.


## OverviewDataDisplay

OverviewDataDisplay is a component which renders the current reading for a single metric measured by a single device.

**Props used:**
- *data*: An object; the data for one metric from one device, in the format given by the API response.
    - Example: {"buoy_id":"1","measure_name":"do","time":"2022-04-08 03:53:02.625000000","measure_value::double":"83.61","measure_value::boolean":null}
- *isWithinThreshold*: A boolean indicating whether or not the value given in the data prop is within the set threshold.

**Functions implemented:**
None

**Noteworthy components used:**
None


## DetailsPanel

DetailsPanel is a component which renders a detailed look at data collected for a specific metric for the device selected.

**Props used:**
- *mode*: A string. "quantitative or "qualitative" depending on the data being displayed.
    - Example: "quantitative"
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]
- *metric*: A string. The shorthand for the metric being displayed.
    - Example: "do"
- *getDeviceFromId*: A function which returns settings data for a specified device.

**Functions implemented:**
- *applyRange*: Does not take any arguments. Changes the rangeStart and rangeEnd states to their corresponding dates as per the selection indicated by the calendar.
    - This is used to change the date range of data being displayed
- *handleTimeClick*: Handles the selection at the time range dropdown. Changes the main text on the time range dropdown to indicate the current selection and toggles the range selection menu accordingly. Sets the time range if one of the preset values are selected.
    - This is used for the time range dropdown menu.
- *isUnique*: Returns whether a value within an array is unique within that array.
    - This is used to help create a list of unique metrics being measured by the selected devices to name and populate each tab.
- *handleThresholdClick*: Handles the selection at the threshold dropdown. Changes the main text on the threshold dropdown to indicate the current selection and toggles the range selection menu accordingly.
    - This is used for the threshold dropdown menu.
- *handleThresholdStartEntry*: Handles the text entry for selecting the start of the threshold range.
    - This is used to set the start of the threshold range.
- *handleThresholdEndEntry*:  Handles the text entry for selecting the end of the thrwshold range.
    - This is used to set the end of the threshold range.
- *submitThreshold*: Does not take any arguments. Validates whether the text entries are valid (must be a number) and filters the data according to the entered range.
    - This is used to prepare the data for use in the DataTable and DataDownloadButton components.

**Noteworthy components used:**
- *LastUpdateArea*: A component which renders the time last updated and the time range dropdown menu.
- *QualitativeDetailsPanel*: A component which renders a detailed look at qualitative data collected for a specific metric for the device selected.
- *QuantitativeDetailsPanel*: A component which renders a detailed look at quantitative data collected for a specific metric for the device selected.


## LastUpdateArea

LastUpdateArea is a component which renders the time last updated and the time range dropdown menu.

**Props used:**
- *lastUpdated*: A date object; the most recent timestamp from the data.
    - Example: new Date(2022, 5, 14)
- *calendarStartDate*: A date object; the start date for the date picker.
    - Example: new Date(2022, 5, 10)
- *setCalendarStartDate*: A function to set calendarStartDate.
- *calendarEndDate*: A date object; the end date for the date picker.
    - Example: new Date(2022, 5, 14)
- *setCalendarEndDate*: A function to set calendarEndDate.
- *timeDropdownSelection*: A string; the time range dropdown item currently selected.
    - Example: "year"
- *handleTimeClick*: A function handling a selection in the time range dropdown menu.
- *showTimeRange*: A boolean; toggles display of custom time range menu.
- *applyRange*: A function to set the time range of data being displayed.

**Functions implemented:**
None

**Noteworthy components used:**
- *DropdownButton*: A component from React Bootstrap which renders a dropdown menu for selecting time range and threshold options. More information [here](/docs/dashboard/react/react-bootstrap).
- *DatePicker*: A component from React DatePicker which renders a calendar datepicker for selecting a time range. More information [here](/docs/dashboard/react/react-datepicker). 


## QualitativeDetailsPanel

QualitativeDetailsPanel is a component which renders a detailed look at qualitative data collected for a specific metric for the device selected.

**Props used:**
- *lastUpdated*: A date object; the most recent timestamp from the data.
    - Example: new Date(2022, 5, 14)
- *calendarStartDate*: A date object; the start date for the date picker.
    - Example: new Date(2022, 5, 10)
- *setCalendarStartDate*: A function to set calendarStartDate.
- *calendarEndDate*: A date object; the end date for the date picker.
    - Example: new Date(2022, 5, 14)
- *setCalendarEndDate*: A function to set calendarEndDate.
- *timeDropdownSelection*: A string; the time range dropdown item currently selected.
    - Example: "year"
- *handleTimeClick*: A function handling a selection in the time range dropdown menu.
- *showTimeRange*: A boolean; toggles display of custom time range menu.
- *applyRange*: A function to set the time range of data being displayed.
- *thresholdDropdownSelection*: A string; the threshold dropdown item currently selected.
    - Example: "under"
- *handleThresholdClick*: A function handling a selection in the threshold dropdown menu.
- *valueList*: An array of objects; the historical data received from the cloud API.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null,"measure_value::varchar":null}]
- *downloadData*: An array of objects; the filtered data ready for download.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null,"measure_value::varchar":null}]
- *rangeStart*: A date object; the start date for the range of data to be displayed.
    - Example: new Date(2022, 5, 10) 
- *rangeEnd*: A date object; the end date for the range of data to be displayed.
    - Example: new Date(2022, 5, 14)
- *metricName*: A string. The full name for the metric being displayed.
    - Example: "dissolved oxygen"

**Functions implemented:**
None

**Noteworthy components used:**
- *LastUpdateArea*: A component which renders the time last updated and the time range dropdown menu.
- *QualitativeDetailFilters*: A component which renders the threshold dropdown menu for qualitative data.
- *DataDownloadButton*: A component that renders the data download button which allows data to be downloaded as a .csv file. Renders the file's corresponding file name.
- *DataTable*: A component that renders a data table displaying raw historical data within the selected date and threshold ranges.


## QuantitativeDetailsPanel

QuantitativeDetailsPanel is a component which renders a detailed look at quantitative data collected for a specific metric for the device selected.

**Props used:**
- *historicalData*: An array of objects; the historical data received from the cloud API.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null,"measure_value::varchar":null}]
- *unit*: A string; the unit associated with the data values being measured.
    - Example: "°C"
- *deviceId*: A list of IDs corresponding to devices which the user has selected for viewing.
    - Example: ["1", "9", "3"]
- *metric*: A string; the shorthand for the metric being displayed.
    - Example: "do"
- *metricValueType*: A string; the type of the data values.
    - Example: "measure_value::double"
- *metricName= A string; the full name of the metric being displayed.
    - Example: "dissolved oxygen"
- *lastUpdated*: A date object; the most recent timestamp from the data.
    - Example: new Date(2022, 5, 14)
- *calendarStartDate*: A date object; the start date for the date picker.
    - Example: new Date(2022, 5, 10)
- *setCalendarStartDate*: A function to set calendarStartDate.
- *calendarEndDate*: A date object; the end date for the date picker.
    - Example: new Date(2022, 5, 14)
- *setCalendarEndDate*: A function to set calendarEndDate.
- *timeDropdownSelection*: A string; the time range dropdown item currently selected.
    - Example: "year"
- *handleTimeClick*: A function handling a selection in the time range dropdown menu.
- *showTimeRange*: A boolean; toggles display of custom time range menu.
- *applyRange*: A function to set the time range of data being displayed.
- *thresholdDropdownSelection*: A string; the threshold dropdown item currently selected.
    - Example: "under"
- *handleThresholdClick*: A function handling a selection in the threshold dropdown menu.
- *thresholdStart*: A float; the start of the selected threshold.
    -Example: 3.5
- *thresholdEnd*: A float; the end of the selected threshold.
    - Example: 9.9
- *handleThresholdStartEntry*: A function which handles the text entry of the threshold start.
- *showThresholdRange*: A boolean; shows the custom threshold range menu.
- *handleThresholdEndEntry*: A function which handles the text entry of the threshold end.
- *submitThreshold*: A function which handles the submission of a threshold.
- *isInvalidSubmission*: A boolean; whether the threshold submission made by the user is valid or not.
- *downloadData*: An array of objects; the filtered data ready for download.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null,"measure_value::varchar":null}]
- *rangeStart*: A date object; the start date for the range of data to be displayed.
    - Example: new Date(2022, 5, 10) 
- *rangeEnd*: A date object; the end date for the range of data to be displayed.
    - Example: new Date(2022, 5, 14)
- *getDeviceFromId*: A function which returns settings data for a specified device.

**Functions implemented:**
None

**Noteworthy components used:**
- *LastUpdateArea*: A component which renders the time last updated and the time range dropdown menu.
- *Graph*: A component that renders historical data for the selected metric on a line graph.
- *QuantitativeDetailFilters*:  A component which renders the threshold dropdown menu for quantitative data.
- *DataDownloadButton*: A component that renders the data download button which allows data to be downloaded as a .csv file. Renders the file's corresponding file name.
- *DataTable*: A component that renders a data table displaying raw historical data within the selected date and threshold ranges.


## QualitativeDetailFilters

QualitativeDetailFilters is a component which renders the threshold dropdown menu for qualitative data.

**Props used:**
- *thresholdDropdownSelection*: A string; the threshold dropdown item currently selected.
    - Example: "under"
- *handleThresholdClick*: A function handling a selection in the threshold dropdown menu.
    - Example: handleThresholdClick
- *valueList*: An array of objects; the historical data received from the cloud API.
    - Example: [{"buoy_id":"1","measure_name":"ph","time":"2022-03-25 04:45:06.865000000","measure_value::double":"7.03","measure_value::boolean":null,"measure_value::varchar":null}]

**Functions implemented:**
None

**Noteworthy components used:**
- *DropdownButton*: A component from React Bootstrap which renders a dropdown menu for selecting time range and threshold options. More information [here](/docs/dashboard/react/react-bootstrap).


## QuantitativeDetailFilters

QuantitativeDetailFilters is a component which renders the threshold dropdown menu for quantitative data.

**Props used:**
- *thresholdDropdownSelection*: A string; the threshold dropdown item currently selected.
    - Example: "under"
- *handleThresholdClick*: A function handling a selection in the threshold dropdown menu.
    - Example: handleThresholdClick
- *thresholdStart*: A float; the start of the selected threshold.
    -Example: 3.5
- *thresholdEnd*: A float; the end of the selected threshold.
    - Example: 9.9
- *handleThresholdStartEntry*: A function which handles the text entry of the threshold start.
    - Example: handleThresholdStartEntry
- *showThresholdRange*: A boolean; shows the custom threshold range menu.
    - Example: true
- *handleThresholdEndEntry*: A function which handles the text entry of the threshold end.
    - Example: handleThresholdEndEntry
- *submitThreshold*: A function which handles the submission of a threshold.
    - Example: submitThreshold
- *isInvalidSubmission*: A boolean; whether the threshold submission made by the user is valid or not.
    - Example: true

**Functions implemented:**
None

**Noteworthy components used:**
- *DropdownButton*: A component from React Bootstrap which renders a dropdown menu for selecting time range and threshold options. More information [here](/docs/dashboard/react/react-bootstrap).


## Graph

Graph is a component that renders historical data for the selected metric on a line graph.

**Props used:**
- *metric*: A string. The shorthand for the metric being displayed.
    - Example: "do"
- *graphData*: An array of objects containing the buoy id as a string, x value as a date object, and y value as a float.
    - Example: [[{id: "1", x: new Date(2022, 3, 29), y: 9.5}, {id: "1", x: new Date(2022, 3, 30), y: 10.5}], [{id: "2", x: new Date(2022, 3, 29), y: 7.2}]]
- *getDeviceFromId*: A function which returns settings data for a specified device.

**Functions implemented:**
None

**Noteworthy components used:**
- *ChartContainer*: A component from react-timestream-charts which is a container for the whole chart. More information [here](/docs/dashboard/react/react-timestream-charts). 
- *ChartRow*: A component from react-timestream-charts which is a container for all the rows in the chart. More information [here](/docs/dashboard/react/react-timestream-charts). 
- *YAxis*: A component from react-timestream-charts which defines the Y axis of the chart. More information [here](/docs/dashboard/react/react-timestream-charts). 
- *Charts*: A component from react-timestream-charts which is the actual time series chart being plotted. More information [here](/docs/dashboard/react/react-timestream-charts). 
- *LineChart*: A component from react-timestream-charts which defines the line being plotted on the chart from time series data. More information [here](/docs/dashboard/react/react-timestream-charts). 
- *CrossHairs*: A component that renders the crosshair for the tracker while hovering over the graph.
- *Baseline*: A component from react-timestream-charts which defines the baselines being plotted on the chart. More information [here](/docs/dashboard/react/react-timestream-charts). 


## CrossHairs

CrossHairs is a component that renders the crosshair for the tracker while hovering over the graph.

**Props used:**
- *x*: x coordinate of crosshair.
- *y*: y coordinate of crosshair.

**Functions implemented:**
None

**Noteworthy components used:**
None


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

DeviceDescription is a component which renders a short description of the selected device. Not currently implemented.

**Props used:**
- *data*: An object containing data pertaining to the device, such as id, battery level, and connectivity. Currently using dummy data.

**Functions implemented:**
None

**Noteworthy components used:**
None

{: .fs-6 .fw-300 }