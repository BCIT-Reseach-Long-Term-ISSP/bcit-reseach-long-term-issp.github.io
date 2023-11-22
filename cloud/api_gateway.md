---
layout: default
title: API Gateway
has_children: false
permalink: /docs/cloud/bidirectional_communication/api_gateway
grand_parent: Cloud
parent: Bi-directional Communication
has_toc: false
---

# API Gateway

## Overview

The API Gateway is a service that allows us to create, publish, maintain, monitor, and secure APIs at any scale. Using API gateway allows us to create RESTful APIs or even WebSocket APIs that enable two-way communication between AWS services and other applications specifically with the Dashboard.

## How it works

The API Gateway is a fully managed service that handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, authorization and access control, monitoring, and API version management. 

The API Gateway has a few key components that we need to understand in order to use it effectively.

### API

An API is a collection of resources and methods that are integrated with backend HTTP endpoints, Lambda functions, or other AWS services.

### Resources

Resources are the fundamental entities in the API Gateway. They are the URLs that we use to access the API. For example, if we want to access the API for the devices/buoys, we would use the following URL:

```
https://<api-id>.execute-api.<region>.amazonaws.com/test/devices
```

### Methods

Methods are the actions that can be performed on a resource ie GET, POST, PUT, DELETE etc. 

When we create a method, we need to specify the integration type. The integration type is the type of integration that we want to use to integrate the API with the backend. We can use HTTP, Lambda, or AWS services as the integration type.

### How it works

We are using Lambda functions as the integration type for the API. This means that when we call the API, the API will call the Lambda function that is associated with the method.

We can create a method and associate it with a Lambda function using the following steps:

1. Create a Lambda function that will be used to process the request.

2. Create a method that will be used to call the Lambda function.

![API Gateway Method Creation](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/1_api_gateway.png)
<figcaption align="center"><b>API Gateway Method Creation</b></figcaption>

3. Associate the Lambda function with the method.

![API Gateway Method Integration](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/2_api_gateway.png)
<figcaption align="center"><b>API Gateway Method Integration</b></figcaption>

The Lambda Proxy Integration is used to pass the request to the Lambda function. The Lambda function will then process the request and return the response to the API Gateway. The API Gateway will then return the response to the client.
The default Lambda offers more control over the transmission data. The request data can be modified before it is passed to the Lambda function. The response data can also be modified before it is returned to the client.

### Stages

Stages are the different versions of the API. For example, if we want to access the test stage of the API, we would use the following URL:

```
https://<api-id>.execute-api.<region>.amazonaws.com/test/<resource>
```

### Deployments

Deployments are the process of deploying the API to a stage. 

### Authorizers

Authorizers are the way we can control access to the API. We can use IAM roles, Lambda functions, or Cognito User Pools to control access to the API. We can implement custom authorizers to control access to the API.

### Custom Authorizers - AWS Lambda

In order to validate the authorization token, we need to create a custom authorizer. The custom authorizer will validate the authorization token and return the principal ID. The principal ID is the user ID that is used to identify the user. The principal ID is used to identify the user in the API Gateway.

### How it works

The lambda authorizer is a separate lambda function that is assigned to the Lambda functions that we wish to protect.

We can create the lambda authorizer using the following steps:

1. Create a lambda function that will be used to validate the authorization token.

2. Create a lambda authorizer that will be used to validate the authorization token.

![Creating a lambda authorizer](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/1_lambda_authorizer.png)
<figcaption align="center"><b>Creating a lambda authorizer</b></figcaption>

![Creating a lambda authorizer](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/2_lambda_authorizer.png)
<figcaption align="center"><b>Creating a lambda authorizer</b></figcaption>

3. The lambda function is the function that will be used to validate the authorization token. The lambda function will be called by the lambda authorizer.

4. The lambda event payload is what is passed to the lambda function. The lambda event payload contains the authorization token.

5. The Token Source is the source of the authorization token. The Token Source is the header that contains the authorization token. In our case, the Token Source is the "authorizationToken" header.


### Usage Plans

Usage plans are the way we can control how much traffic is allowed to access the API. We can set limits on the number of requests per second, the number of requests per day, or the number of requests per month.

### Throttling

Throttling is the way we can control how much traffic is allowed to access the API. We can set limits on the number of requests per second, the number of requests per day, or the number of requests per month.

### API Keys

API keys are the way we can control access to the API. We can use IAM roles, Lambda functions, or Cognito User Pools to control access to the API.

### Caching

Caching is the way we can cache the responses from the API. We can set the TTL for the cache.

We can enable caching for a specific stage or for all stages in the API. We can also enable caching for a specific resource or for all resources in the API.

The TTL for the cache can be set to a specific value or to a value that is based on the response from the API. For example, we can set the TTL for the cache to 5 minutes or to a value that is based on the response from the API.

![Caching](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/1_api_cache.png)
<figcaption align="center"><b>Caching</b></figcaption>

In our case, we will enable caching for all resources in the API.

It is particularly important to enable caching for the API Gateway because the API Gateway is a proxy for the backend services. If we do not enable caching, then the API Gateway will have to call the backend services every time a request is made to the API Gateway. This will result in a lot of calls to the backend services.

### Current usage
![Current API Gateway](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/1_api_gateway_current.png)
<figcaption align="center"><b>Current API Gateway</b></figcaption>

Currently we have implemented our api gateway, yvr-stage-api-gw, in us-west-2. There are two resources available, data and device.

![Current Gateway Resource](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/bidirectional_comm/1_gateway_resource_current.png)
<figcaption align="center"><b>Current API Gateway Resource</b></figcaption>

Data resource handles requests related to users, such as creating new users and reseting user passwords. Device resource allows Dashboard to perform CRUD operation to the device database. Both resources call lambda functions to provide functionalities. Data resource triggers the yvr-stage-user lambda function. Device resource triggers the yvr-stage-device lambda function. Refer to corresponding documentation for details.

