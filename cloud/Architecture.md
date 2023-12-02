---
layout: default
title: Architecture
has_children: false
permalink: /docs/cloud/arch
parent: Cloud
has_toc: false
nav_order: 14
---

# Overview  

During the 2023 iteration. There were two cloud teams (BBY and DTC). Under their amazing work, we have upgraded the architecture significantly. 

![Final Cloud architecture for 2023](/cloud/assets/architecture/final-cloud-2023-architecture.drawio.png)

The updated architectures aims to achieve:  

- Improved security
- Cost optimization
- Removal of redundancies
- Improved backup and recoverability of timestream db and dynamodb
- Lambdas and Lambda Layers to process calibration data
- CI/CD of Lambdas

## Key Features / Concepts:

1. AWS Cognito:

2. Calibration Lambdas:

3. MQTT and IoT Core:

# Current Usage

| Stack Name                                 | Description                                                                                                             |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| `yvr-stage-api-gw`                         | Manages resources relevant to the API Gateway for updating device configuration and user data                           |
| `yvr-stage-iot-rule`                       | Manages IoT rules for invoking the calibration lambda function                                                          |
| `yvr-stage-calibration-lambda-function`    | Manages resources relevant to the Lambda function that calibrates the incoming data from device                         |
| `yvr-stage-device-lambda-function`         | Manages resources relevant to the Lambda function that performs CRUD operation of device configuration data in DynamoDB |
| `yvr-stage-user-lambda-function`           | Manages resources relevant to the Lambda function that performs CRUD operation of user data in DynamoDB                 |
| `yvr-stage-cognito-get-users-info-lambda-function`         | Manages resources relevant to the Lambda function that sses the AWS Cognito API to get user information                                                                        |
| `yvr-stage-cognito-get-role-lambda-function`               | Manages resources relevant to the Lambda function that sses the AWS Cognito API to get user role                                                                               |
| `yvr-stage-cognito-add-update-delete-user-lambda-function` | Manages resources relevant to the Lambda function that sses the AWS Cognito API to add, update, or delete a user                                                               |