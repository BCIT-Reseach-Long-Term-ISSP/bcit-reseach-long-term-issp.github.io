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

## Graph Page Tests

| Description      | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Only numerical values are allowed when filtering table values | Enter any non-number | Error message appears asking the user to enter a numerical value |

## Edit Device Tests

| Description      | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Name entry cannot be blank | Delete current name or enter spaces | Error message appears asking the user to enter a valid name |
| Only numerical values are allowed when assigning thresholds | Enter any non-number | Error message appears asking the user to make a valid entry |
| Threshold minimum can not be greater than maximum | Enter a lower maximum than the minimum |  Error message appears asking the user to make a valid entry |
| User must be logged in to edit device | While not logged in click Save Changes | Error message appears saying data cannot be saved and that permission was denied |
| User must have administrator permissions to edit device | While logged in on an account without admin permissions click Save Changes  | Error message appears saying data cannot be saved and that permission was denied |

## Map Tests

| Description | Steps | Expected Result |
| ----------- | ----------- | ----------- |
| Clicking on an unselected device will select it | Click on a device's pin which is black | The device's pin will turn green, and the device's name will appear in the Selected Devices section |
| Clicking on a selected device will deselect it | Click on a device's pin which is green | The device's pin will turn black, and the device's name will disappear from the Selected Devices section |
| Area select will do nothing if no devices are in the selected area | Activate the area select mode, and then move the selection such that no devices fall in the area. Then, press the green checkmark to confirm the selection | No devices will be selected, and area select mode will be exited |
| Cancelling area select will mean that any unselected devices in the selection area will remain unselected | Activate the area select mode, and then move the selection such that unselected devices fall within the area. Then, press the red X to cancel the selection | The unselected devices will remain unselected |
| User can deselect devices from the Selected Devices section | With a device selected, click on the red - icon to the left of the device's name in the Selected Devices section | The device will be removed from the Selected Devices section, and its pin on the map will turn black |

{: .fs-6 .fw-300 }