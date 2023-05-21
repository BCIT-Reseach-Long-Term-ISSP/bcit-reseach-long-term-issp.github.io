---  
layout: default  
title: Test Cases
has_children: false  
permalink: /docs/dashboard/v2-2022/test-cases  
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard 
has_toc: true
---  

# Test Cases
{: .no_toc }

This page lists possible test cases for the Dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Data Page Tests

| Description      | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Selecting one buoy on the map will display that buoy's associated metrics | Select one buoy on the map | The buoy's associated metrics will populate the data page tabs and the overview display |
| Selecting multiple buoys on the map will display all associated metrics from all buoys combined | Select more than one buoy on the map | All associated metrics will populate the data page and each buoy's associated metrics will populate the data page in order of buoy id numerical order |
| When no buoy is selected, no buoy data will be displayed on the data page | Deselect all buoys and navigate to the data page | The message "No buoy selected" will be displayed and no tabs appear |
| Quantitative metrics will display a time series graph on the detailed data page | query data from a buoy with metrics that measure quanitative data | A time series graph data wll be displayed when that metric's tab is selected |
| Only numerical values are allowed when filtering table values for quantitative data | Enter any non-number | Error message appears asking the user to enter a numerical value |
| When filtering values by range, the first text entry must be of a lower number than the next | Enter a higher number in the first text box than the second | Error message appears |
| Qualitative metrics will allow the user to filter table values by all existing values that have been measured in the buoy within the time range | Use data from a buoy with metrics that measure qualitative data | The filter table values dropdown menu will be populated with all existing values that have been measured in the buoy |
| Values outside of the set threshold associated with that buoy will display as red in the overview tab and in the data tables | Query data from a buoy which returns values outside of the set threshold | Values will display as red in the overview tab and data tables |

## Edit Device Tab Tests

| Description      | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Name entry cannot be blank | Delete current name or enter spaces | Error message appears asking the user to enter a valid name |
| Only numerical values are allowed when assigning thresholds | Enter any non-number | Error message appears asking the user to make a valid entry |
| Threshold minimum can not be greater than maximum | Enter a lower maximum than the minimum |  Error message appears asking the user to make a valid entry |
| User must be logged in as an administrator to edit device | While not logged in, click Save Changes | Error message appears saying data cannot be saved and that permission was denied |
| User must have administrator permissions to edit device | While logged in on an account without admin permissions, click Save Changes | Error message appears saying data cannot be saved and that permission was denied |

## Map Tests

| Description | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Clicking on an unselected device will select it | Click on a device's pin which is black | The device's pin will turn green, and the device's name will appear in the Selected Devices section |
| Clicking on a selected device will deselect it | Click on a device's pin which is green | The device's pin will turn black, and the device's name will disappear from the Selected Devices section |
| Area select will do nothing if no devices are in the selected area | Activate the area select mode, and then move the selection such that no devices fall in the area. Then, press the green checkmark to confirm the selection | No devices will be selected, and area select mode will be exited |
| Cancelling area select will mean that any unselected devices in the selection area will remain unselected | Activate the area select mode, and then move the selection such that unselected devices fall within the area. Then, press the red X to cancel the selection | The unselected devices will remain unselected |
| User can deselect devices from the Selected Devices section | With a device selected, click on the red - icon to the left of the device's name in the Selected Devices section | The device will be removed from the Selected Devices section, and its pin on the map will turn black |

{: .fs-6 .fw-300 }