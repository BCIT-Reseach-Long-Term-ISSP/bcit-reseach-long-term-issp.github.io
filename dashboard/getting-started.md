---
layout: default
title: Getting Started
parent: Dashboard
permalink: /docs/dashboard/getting-started
nav_order: 2
---

# Getting Started
So you're ready to start developing, what now?
{: .fs-6 .fw-300 }

Before beginning, you should have cloned both the existing [backend](/docs/github-organization/dashboard-repos/iot-dashboard-2023-backend-repo/) and [frontend](/docs/github-organization/dashboard-repos/iot-dashboard-2023-frontend-repo/) repositories onto your local machine. The instructions on this page assumes that you have knowledge of version control and Node package manager isntalled on your machine.

You may also choose to install a Node version manager such as `nvm`. But that is up to you.

---

## Server (back-end)

1. Checkout the branch you’d like to run on.
2. Pull the latest update from the branch you want to grab.
3. Install the latest dependencies. You will have to run this command before running the build anyways for the very first time locally using one of the following commands:
    
    ```bash
    npm i
    npm install
    ```
    
4. Run the backend with `npm run dev`

---

## Client (front-end)

| 📍 In order for all elements of the frontend to be working, **you must run the backend server locally first**! Please note, also, that the tidal data is not pulled when in development since we utilize a cache and have limited free API calls. There’s no bug there. |

1. Checkout the branch you’d like to run on.
2. Pull the latest update from the branch you want to grab.
3. Install the latest dependencies. You will have to run this command before running the build anyways for the very first time locally using one of the following commands:
    
    ```bash
    npm i
    npm install
    ```
    
4. Run the frontend with `npm start`, this will open a local window with the application