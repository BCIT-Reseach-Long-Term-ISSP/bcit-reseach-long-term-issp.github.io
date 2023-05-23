---
layout: default
title: Deployment
parent: Dashboard
permalink: /docs/dashboard/deployment
nav_order: 6
---

# Deployment
LGTM, Ship It.
{: .fs-6 .fw-300 }

Note: Both backend and frontend are deployed with accounts that use the yvrdashboard@gmail.com email. The log-in credentials for these accounts should be passed on from the previous team and should not be added to this public documentation.

---

## Backend

The backend is deployed and hosted using the free service from Render. This service currently being used is a free tier service which includes the following:

- 500 build minutes a month
- 100 GB bandwidth
- Automatic re-deploys from GitHub

The team recommends migrating to the **Team** or **Organization** plans which are paid tier services which provide more build minutes and bandwidth per month.

---

## Frontend

The frontend is deployed and hosted using a free service from Netlify. The frontend had to be migrated to a repo on the shared email account due to the free service not allowing deployment from a private repo of an organization on Github. Therefore, the team recommends upgrading to a paid service which lifts this restriction.