---  
layout: default  
title: Navbar
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/navbar
---  

# Navbar

The navbar is used for switching between pages of the dashboard.

The navbar is comprised of only a single component: the Navbar component. Details of this component can be found below.

## Navbar

The Navbar component consists of three buttons: the map button, the notifications button, and the data button. Each button switches which page of the dashboard the user is on.

**Props used:**
- *currentPage*: A string which indicates the current page being displayed.
    - The values for this are defined in the constants.js file found in src/extras; MAP, NOTIFICATIONS, and DATA. This is simply to reduce the likelihood of something like a typo.
- *setPage*: A function which takes an argument that is used to change the current page.
    - For example, calling setPage with an argument of MAP (from the constants.js file) while on the notifications page would switch the dashboard to the map page.

**Functions implemented:**
- *getSelected*: Returns a CSS id which indicates that a given navbar element is the button for the page which the user is currently on.
    - If the given navbar element is the currentPage, then it returns "navbar-element-selected"; otherwise, it returns an empty string.

**Noteworthy components used:**
- *Clearfix*: A component which is simply a clearfix implementation for floating elements.
- *BellFill*: A component from react-bootstrap-icons which renders a notification bell. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *PinMapFill*: A component from react-bootstrap-icons which renders a map with a pin in it. More information [here](/docs/dashboard/react/react-bootstrap-icons).
- *GraphDown*: A component from react-bootstrap-icons which renders a graph with a downward trend. More information [here](/docs/dashboard/react/react-bootstrap-icons).

{: .fs-6 .fw-300 }