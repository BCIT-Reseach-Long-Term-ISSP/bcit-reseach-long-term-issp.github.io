---  
layout: default  
title: Proposals for Improvement
has_children: false  
permalink: /docs/dashboard/proposals-for-improvement
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: true
---  

# Proposals for Improvement
{: .no_toc }

This page contains recommendations for potential future features of and adjustments to the dashboard, as well as some questions and warnings for issues that may come up in the future.

Note that these are fully unordered; they aren't listed in order of priority or anything.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## API's AWS key

Currently, as of the end of May, the API hosted on the Firebase is using Charles Paz's API key for connecting to the AWS.

Naturally, this could become an issue in the future if Charles' API key is removed from the AWS, so it would likely be best to generate an API key to be used specifically for the hosted API.

## Mapbox API key

Currently, as of the end of May, the Mapbox API key (as defined in src/extras/constants.js) which is required to render the map is Aidan Thomlinson's.

This key is on a free plan, which allows 50,000 map loads per month. This is not a dire issue, but it could become an issue in the event that the number of users becomes much higher, or if a problem ever occurs that results in the public token being revoked.

Therefore, it would be beneficial, though not exactly dire, to have a permanent Mapbox account associated with the project.

The Mapbox website can be found [here](https://www.mapbox.com/).

## WeatherAPI key

Currently, as of the end of May, the WeatherAPI key (as defined in src/components/device/widgets/weatherWidget.jsx) which is required in order to grab the current weather in YVR is Denise Chew's.

Much like the Mapbox key, this key is on a free plan. While it allows 1 million calls per month, it would be beneficial to have a permanent WeatherAPI account associated with the project, in case of any potential unforeseen circumstances.

The WeatherAPI website can be found [here](https://www.weatherapi.com/).

## General speed improvements

Some queries can be somewhat slow, which means that some pages can take a good bit to load. The priority thus far has just been to focus on implementing the features, with speed as a less important factor, so there's a good chance that there's a fair number of ways that the site can be sped up.

In the future, it would be great if it's possible to pinpoint some of these issues (and possible ways to speed things up).

One way that was planned for speed up was usage of AWS's scheduled queries. These can be used to create aggregates and other such preprocessed data periodically. The cloud team was able to implement it on their end, but the dashboard team was not able to find time to implement it on our end. More information on these scheduled queries can be found [here](/docs/cloud/ts-scheduled-queries).

## Boolean thresholds

Thresholds can only be set for values that are actual numbers; boolean values cannot have thresholds. This means that warnings cannot be issued for boolean data types.

One potential challenge of implementing this is that the structure of a threshold object states a max and min, and warnings are queried by checking if a value has gone over or under the max or min. Naturally, this process would be wholly different for boolean values and thresholds.

However, warnings for boolean data types could be very important, so boolean thresholds would be a very helpful addition.

## Non-hardcoded default thresholds and data type names

Default thresholds and data type names are hardcoded in through constants.js and cloudAPIHelper.js respectively.

In the future, it would be beneficial to have these moved into the Firestore.
- It would be nice to be able to change the default thresholds from the dashboard itself, as the thresholds wanted for multiple devices could change depending on external factors (like season, for instance)
- If a device implements a new data type, it would be much more efficient to be able to give that data type a name from the dashboard itself, without needing someone to manually add it to the React files, then build, then deploy

## URL changes for different pages

There is only one URL for all pages of the dashboard: https://bcitema-f85bf.firebaseapp.com/.

However, users may, for instance, wish to refresh the notifications/manage device page. Right now, the refresh would bring them back to the map page, from which the user would need to navigate to the notifications page once more.

If the URL changed per page, then it would be possible to do so. Following the previous example, if the user was on the notifications page, the URL could be https://bcitema-f85bf.firebaseapp.com/notifications.

## Domain name registration

There is no domain registered for the dashboard, so the link is using a default firebaseapp.com link.

This is most certainly not a dire change, but if anyone comes up with a good domain name, the website could be hooked up to that domain once it's bought!

One benefit of a good domain name would mean that it's a lot easier to remember if, for example, you want to write down the URL on a sticky note.

## Clean up imports

A lot of components have a lot of now-unused imports. These were once being used, but aren't anymore.

They aren't really doing any harm there, but they do make the top of some files a bit cluttered.

## More comprehensive warnings

Warnings only state the number of readings that were over or under a given data type's thresholds, or if the device has not transmitted any readings in the last 2 hours.

It would be beneficial if these warnings could be more informative, and would let the user see when these warnings occurred, and extra info pertaining to each specific warning under a device.

A mockup can be found below:

![Comprehensive warnings mockup](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/ComprehensiveWarningsMockup.png?raw=true "Comprehensive warnings mockup")

## Better mobile support

While all pages should at least work on mobile, some pages have layouts that are a bit cumbersome on mobile. One particularly tough page is the device page, which has both vertical and horizontal scrolling.

Below is a side-by-side of the current page, as well as a mock up of a more mobile-friendly version.

![Mobile device page now](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DevicePageMobileOld.png?raw=true "Mobile device page now")
![Mobile device page mockup](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/DevicePageMobileNouveau.png?raw=true "Mobile device page mockup")

## Checkbox selection for device page

Devices that do not have locations on the map cannot be selected; this means that their data cannot be viewed on the device page.

A checkbox selection option on the device page could be useful to allow for this, and would also allow for devices to be deselected without going to the map page.

## "Pages" for the device page's data table

On the device page, when a tab for a data type is navigated to, a data table is displayed showing information pertaining to all readings of that data type in the set time frame. 

An issue can crop up with this, however, when the time frame is very broad, or when there are many devices selected, as there could be thousands of data points, and all of these would appear in the table. Naturally, this can make loading this page fairly slow.

One solution to this would be to separate these data points in the table into "pages" of sorts, kind of like when you're on an online store. For instance, it could be set to where only 100 data points are shown at a time, so the user would, by default, see data points 1-100. Then, they could choose to see data points 101-200, and so on.

This would, hopefully, provide a tremendous speed boost to the device page when working with lots of data.

## Checks for unsaved changes when managing a device

When a device is being edited, the user is able to freely and instantly switch to another device or another page without saving their changes.

This could be troublesome, however, if the user didn't intend to do so, and had just done several changes only for all of them to crumble through their fingers like ash.

Thus, it would be helpful if the page checked for unsaved changes, and prompted the user to either go back or discard their changes when they attempt to leave without saving.

## General comments

- Ability to download data in different formats, i.e. .csv and .xlsx
- If there is the ability to create a histogram for a selected parameter for a given amount of time such that the system recognizes data ranges based on the minimum, maximum, mean and mode, and creates a histogram depicting frequency of data – this gives us an additional tool for storytelling, whether it tells a good story or not. This could be asking for too much, but I think that at the very least a histogram that can show a distribution of minimum to maximum values can be useful.
- Ability to toggle between different charts that display the data in different formats, e.g. histogram, or the ability to create comparison graphs that can show two time variables (e.g. how does 2022 differ from 2021?) – note this only works for one site at a time

## Map page

- All devices should be shown within “selected devices” window with a toggle check box to select them similar to selecting them on the map.
- Does mapbox allow for satellite imagery? It would be nice to be able to toggle between layers.
- Labels on the stations in the map so it is clear to the user where each station is located (this might not be as applicable since we know where our stations are, but in making the system as user-friendly as possible I think it is a good tool to have, especially if we want to utilize this with people who may not be as familiar).
- Box button: should allow for dragging to create a box instead of having to grab the corners of the existing box to alter the size (similar to the “identify” function on GIS). The way that the box is set up now in which you have to drag either end of the corners reduces ease of access.
- Ability for the stations to flash or have some kind of alert to let us know exceedances have occurred without actually clicking the station (ex. flashing red/orange/yellow depending on the severity of the exceedance). At a glance you would be able to open the map and know where exceedances have occurred without having to click anything. Then click to find out further details. Then the alarm can only be deactivated once it has been clicked through to view the problem. Similar to the overview data page where some of the parameter squares are Red rather than blue when stations are selected.

## Data page

- Overview dashboard
  - Top “device” shown should be the highest value for all devices selected and identify which device its coming from (ideally as click through). In other words, this will show all the worst water quality at a glance and let you drill down to the specifics.
  - I was unclear on whether these values update in real time in the information page, or will only the latest timestamped data recording from when the user navigates to the information page?
  - Ability to click specific parameters for more detail on the overview page to take us to the selected parameter. Another way to click to each parameter rather than only being able to get there from the parameters listed at the top beside Overview.
  - Ability to select the meters of interest from Overview Data Page without having to click back to the map to select.
  - Ability to change between units for each parameter if needed (ex. L/s to gallons/min,  ppm to ppt, mS/cm to µS/cm)
  - Weather and Tide Schedule should include the date for clarity, ability to view future, present and historical weather/tide data.
  - If possible alerts for King Tides, Freshet Melts, atmospheric rivers, etc…
- Dissolved Oxygen
- Electrical Conductivity
  - Units should be micro Simens/centimeter (µS/cm)
- pH
  - set the data range for pH, i.e. 1 to 14
- Turbidity
- TSS
- Temp
  - An alarm when temperatures reach 4°C or lower
- Liquid Level
  - This should be water level?
  - what does 'true' mean?
  - This should be relative to tide, to tell us whether the water level is at low, mid or high tide along with a numeric value – ideally in geodetic.
- Water flow
  - TBD
- Water pressure
  - Is this water level?

## Alarm page

- 72 hours is a good timeline for receiving device warnings that have been logged. I would suggest the ability to change that time range (e.g. for a long weekend when we ideally wouldn’t be reading these alerts for over 72 hours) up to a maximum of five days if the system cannot store alerts for very long. Realistically data can be retrieved and those exceedances can also be read through the data but having the alert is a good shortcut way to determine that.
- Alarms should be able to be forwarded to email accounts with customizable messages and triggers.
- In the Device Management, this would be a good place to be able to select whether to display a label for each station on the map.
- Edit Device - this function should only be accessible to certain users (ex. admin for ENV only)

## Manual

- I noticed when data is downloaded the date/time stamp is in UTC. Ability to change to PST or whatever time zone would be nice.

{: .fs-6 .fw-300 }