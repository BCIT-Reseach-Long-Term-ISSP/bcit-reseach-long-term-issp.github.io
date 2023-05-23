---
layout: default
title: Improvements
parent: Dashboard
permalink: /docs/dashboard/improvements
nav_order: 8
---

# Improvements
Possible improvements and bug fixes as suggested by the previous Dashboard team.
{: .fs-6 .fw-300 }

Last updated: May 2023

## Improvements
- **Map modal select**: Currently the map modal select does not affect any changes to the components that display data based on selected devices. The Recoil state has been implemented but the incoming team will need to make sure the relevant components are displaying data based on the list of selected device ids
- **Hardcoded Metrics / Device Ids:** Because of the unstructured and messy state of data coming from the devices and cloud layers, the Dashboard has hardcoded metrics and device ids. Upon confirmation that testing data has been removed and that all data is verified to be accurate, the incoming Dashboard teams will have to refactor the hardcoded information in the Backend repository.
- **Feature Integration:** The incoming teams should focus on integrating their existing completed features to the code base and test that everything is working as it should.
- **Devices API**: Given the truncated time to develop the Devices API on the AWS Gateway, the API will need to be modified by the incoming Cloud team. Any modification on the Cloud end will result in structural changes to the Backend.
- **Mongo DB**: Currently, the backend set up is only being used for user authentication and validation. Due to the development of the Devices API, much of the Mongo db backend is now redundant. However, our team recommends converting the Backend that the team set up on Mongo to a proxy server which could be used to optimize the large flow of data coming from AWS.
- **JWT Token for AWS:** The method to request a API key from AWS Secret Manger is set up in the **Sessions** model but the team is using a hardcoded JWT with Admin roles set as the JWT key. This needs to be changed to dynamically requesting the key to protect admin-access only routes. The information for the Token method can be found under the Sessions section of the Backend API documentation.
- **CREATE, DELETE, other UPDATE functionality:** The application as a whole is missing CREATE operations, such as-- create a new device, add a new sensor to a device or DELETE them. There may also be foreseeable better implementation of displaying sensor details in the future.

## Bugs and Fixes
- **General Settings Panel**: The current panel pulls from a recoil state that is global to the device manager page. Thus, on save and re-fetch, the modal closes. The panel should be implemented like the Thresholds panel using useState to prevent modal closure.