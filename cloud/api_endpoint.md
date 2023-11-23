---
layout: default
title: API Endpoint
has_children: false
permalink: /docs/cloud/bidirectional_communication/api_endpoint
grand_parent: Cloud
parent: Bi-directional Communication
has_toc: false
---

# Cognito API Endpoint

The purpose of this endpoint is to provide user info to the Dashboard's admin portal, along with user management.

AWS Console Info:

-	Link: https://bcit-iot-coc.signin.aws.amazon.com/console
-	Username: dashboard_admin 
-   Password: YVR_admin_1! 

Once logged into AWS, change the region to Oregon, go to Cognito, then “yvr” user pool

Note: Authorization (JWT token) is required for all endpoints

## GET ALL USER

-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/user
-	Request:
    o	Header should include (Authorization: JWT token)
    o	GET Request
    o	No body required
-   Response:
    ![getalluser_01](/assets/getalluser_01.png)