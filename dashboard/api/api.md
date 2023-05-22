---
layout: default
title: API Endpoints
parent: Dashboard
has_children: true
permalink: /docs/dashboard/api
has_toc: true
nav_order: 2
---

# Server APIs
The backend provides APIs to grab data from AWS Timestream, our own MongoDB, and AWS RDS set up with Device, Thresholds, and Calibration details.
{: .fs-6 .fw-300 }

## Where is data coming from?

| Data                    | Source            | Owner      | Dashboard API Route   
| -------------           |:-------           | :-----     | :------------
| Real-time Sensor Data   | AWS Timestream    | Cloud      | `/api/ts`
| Device Settings         | AWS RDS           | Cloud      | `/api/device`
| Sensor Settings         | AWS RDS           | Cloud      | `/api/device`
| Calibration             | AWS RDS           | Cloud      | `/api/calibration`
| User Alert Thresholds   | MongoDB           | Dashboard  | `/api/userThreshold`
| Default Thresholds      | MongoDB           | Dashboard  | `/api/defaultThreshold`
| Sessions                | MongoDB           | Dashboard  | `/api/session`
| Users                   | MongoDB           | Dashbaoard | `/api/user`


The child pages in this section will detail what each of these data sources and API routes are.

# Thresholds

Thresholds are values used for alert system. Users may want to receive alerts for requested metrics from requested devices if these metrics are below or above certain values. The results of comparing metric measurements to these thresholds will determine whether or not an alert should be sent to the user. There are 2 collections related to thresholds in the database; `defaultThresholds` and `userThresholds`.

### Default Thresholds

![Untitled](Back-end%20Server%20Architecture%205c3544028faa4c38964c5714a72d8b8b/Untitled%2017.png)

For each metric that can be measured by devices within the scope of this project, a minimum and a maximum threshold value is designated. If users don’t want to designate their own threshold values, they can use these default values to receive alerts for the metrics they want from the device they request. 

![Untitled](Back-end%20Server%20Architecture%205c3544028faa4c38964c5714a72d8b8b/Untitled%2018.png)

The main purpose of default thresholds is to give YVR the ability to control alert system triggers based on their priority when evaluating metrics from devices. Thus, default threshold documents stored in the database should only be created, updated and deleted by “admin” type user.

### User Thresholds

![Untitled](Back-end%20Server%20Architecture%205c3544028faa4c38964c5714a72d8b8b/Untitled%2019.png)

As specified before users can use default threshold values to receive alerts which are designated for each metric by “admin”. However, if they want they can designate their own threshold values for each metric in each device. When a user decides to track a device that is in the field they can designate minimum and maximum threshold values for each metric measured by that device too. If they don’t specify a threshold value, default threshold values will be assigned for each metric. These customized threshold values for each user and each device they track is stored in “userthresholds” collections with users’ choice of receiving an alert for each metric. 

![Untitled](Back-end%20Server%20Architecture%205c3544028faa4c38964c5714a72d8b8b/Untitled%2020.png)

UserThreshold functions can be found in related directories.

![Untitled](Back-end%20Server%20Architecture%205c3544028faa4c38964c5714a72d8b8b/Untitled%2021.png)