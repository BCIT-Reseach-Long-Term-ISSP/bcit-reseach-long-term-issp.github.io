---  
layout: default  
title: react-datepicker
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/react-datepicker
---  

# React Datepicker
{: .no_toc }

. The website for it can be found [here](https://reactdatepicker.com/).

Below are components which are used within the dashboard. Please note that some components may take props which are unlisted here; the props listed here are merely the ones used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## DatePicker

Datepicker is a component that renders a popup calendar that can be used for inputting dates.

**Props Used:**
- *selected*: A Date object; the current selected date on the calendar
- *onChange*: A function; handles a date selection.
- *selectsStart*: Indicates that the calendar is used for selecting the start date.
- *selectsEnd*: Indicates that the calendar is used for selecting the end date.
- *startDate*: A Date object; the current selected start date.
- *endDate*: A Date object; the current selected end date.
- *minDate*: A Date object; the minimum selectable date.
- *maxDate*: A Date object; the maximum selectable date.