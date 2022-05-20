---  
layout: default  
title: Test Cases
has_children: true  
permalink: /docs/dashboard/test-cases  
parent: Dashboard  
has_toc: true
---  

# Test Cases

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Graph Page Tests

| Description      | Steps || Expected Result |
| ----------- | ----------- | ----------- |
| Only numerical values are allowed when filtering table values | Enter any non-number | Error message appears asking the user to enter a numerical value |

## Edit Device Tests

| Description      | Steps || Expected Result |
| ----------- | ----------- | ----------- |
| Name entry cannot be blank | Delete current name or enter spaces | Error message appears asking the user to enter a valid name |
| Only numerical values are allowed when assigning thresholds | Enter any non-number | Error message appears asking the user to make a valid entry |
| Threshold minimum can not be greater than maximum | Enter a lower maximum than the minimum |  Error message appears asking the user to make a valid entry |
| User must be logged in to edit device | While not logged in click Save Changes | Error message appears saying data cannot be saved and that permission was denied |
| User must have administrator permissions to edit device | While logged in on an account without admin permissions click Save Changes  | Error message appears saying data cannot be saved and that permission was denied |

{: .fs-6 .fw-300 }