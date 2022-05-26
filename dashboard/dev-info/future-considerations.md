---  
layout: default  
title: Future Considerations
has_children: false  
permalink: /docs/dashboard/future-considerations
parent: Dashboard  
has_toc: true
---  

# Future Considerations
{: .no_toc }

This page contains recommendations for potential future features of and adjustments to the dashboard, as well as some warnings for issues that may come up in the future.

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

{: .fs-6 .fw-300 }