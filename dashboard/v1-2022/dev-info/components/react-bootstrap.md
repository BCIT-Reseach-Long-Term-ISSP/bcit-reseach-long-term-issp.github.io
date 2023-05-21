---  
layout: default  
title: react-bootstrap
parent: Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/v2-2022/react-bootstrap
---  

# react-boostrap
{: .no_toc }

React Bootstrap is a suite of components that are commonly used to build websites. The design elements are responsive and functional.
. The website for it can be found [here](https://react-bootstrap.github.io/).

Below are components which are used within the dashboard. Please note that some components may take props which are unlisted here; the props listed here are merely the ones used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Tabs

Tabs is a component which renders a tabbed display.

**Props Used:**
- *defaultActiveKey*: A string; the eventKey of the default tab that is shown.


## Tab

Tab is the individual tab/page belonging to a tabs component.

**Props Used:**
- *eventKey*: A string; a unique identifier for a tab.

## DropdownButton

DropdownButton is a component which renders a dropdown menu with clickable buttons.

**Props Used:**
- *title*: A string; the text displayed on the dropdown button.
- *size*: A string; the size of the button.
- *onSelect*: A function; handles the selection of a menu item.

## Dropdown.Item

Dropdown.Item is the individual menu item of a dropdown menu.

**Props Used:**
- *eventKey*: A string; a unique identifier for a dropdown item.