---
layout: default
title: Cognito API Endpoint
has_children: false
permalink: /docs/cloud/bidirectional_communication/cognito_api_endpoint
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
    -   Header should include (Authorization: JWT token)
    -   GET Request
    -   No body required

-   Response:


![getalluser_01](assets/api_endpoint01.png)


## ADD A NEW USER

-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/user
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body Required, include the following:
        -   Operation is “add”
        -   Email
        -   Password must be 8 characters minimum length
            -   At least 1 number
            -   At least 1 lowercase letter
            -   At least 1 uppercase letter
            -   At least 1 special character
        -   Role could either be “admin” or “user”

-   Example Request:

![addnewuser_01](assets/api_endpoint02.png)

-   Example Response:

![addnewuser_02](assets/api_endpoint03.png)


## UPDATE A USER

-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/user
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body Required, include the following:
        -   Operation is “update”
        -   Old email
        -   New email
        -   Password must be 8 characters minimum length
            -   At least 1 number
            -   At least 1 lowercase letter
            -   At least 1 uppercase letter
            -   At least 1 special character
        -   Role could either be “admin” or “user”


-   Example Request:

![updateauser_01](assets/api_endpoint04.png)

-   Example Response:

![updateauser_02](assets/api_endpoint05.png)


## DELETE USER

-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/user
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body Required, include the following:
        -   Operation is “delete”
        -   Email

-   Example Request:

![deleteuser_01](assets/api_endpoint06.png)

-   Example Response:

![deleteuser_02](assets/api_endpoint07.png)


## CHECK USER'S ROLE
*Note this endpoint is different from previous ones, have /role in the url path

-	Endpoint: https://c5hn9pagt5.execute-api.us-west-2.amazonaws.com/prod/user/role 
-	Request:
    -   Header should include (Authorization: JWT token)
    -   POST Request
    -   Body Required, include the following:
        -   Email

-   Example Request:

![checkuserrole_01](assets/api_endpoint08.png)

-   Example Response:

![checkuserrole_02](assets/api_endpoint09.png)







