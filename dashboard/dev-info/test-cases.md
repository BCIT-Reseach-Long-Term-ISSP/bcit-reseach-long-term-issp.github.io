---  
layout: default  
title: Test Cases
has_children: true  
permalink: /docs/dashboard/test-cases  
parent: Dashboard  
has_toc: true
---  

# Test Cases

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

{: .fs-6 .fw-300 }