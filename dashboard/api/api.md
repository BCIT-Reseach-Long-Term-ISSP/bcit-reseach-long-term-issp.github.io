---
layout: default
title: API Endpoints
parent: Dashboard
has_children: true
permalink: /docs/dashboard/api
has_toc: true
nav_order: 5
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
| Weather and Tide        | Third-party API   | Dashbaoard | `/api/weather`


The child pages in this section will detail what each of these data sources and API routes are.
