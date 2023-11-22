---
layout: default
title: AWS Cloudformation
has_children: false
permalink: /docs/cloud/aws-cloudformation
parent: Cloud
has_toc: false
nav_order: 13
---

# Overview

Amazon Web Services (AWS) CloudFormation is a service that helps users model, provision, and manage their AWS infrastructure resources in a consistent, predictable, and repeatable manner. It enables the creation, modification, and deletion of a collection of resources together as a single unit, referred to as a "stack."

## Key Features / Concepts:

1. Templates: CloudFormation uses JSON or YAML formatted templates to define the desired resources, their properties, and their relationships. These templates serve as a blueprint for creating and configuring AWS resources.

2. Stacks: A stack is a collection of AWS resources created from a CloudFormation template. Stacks can be created, updated, or deleted as a single unit, allowing for easy management of resources.

3. Change Sets: Change sets allow users to preview the changes that will be made to a stack before executing them. This helps to identify potential issues before they impact the environment.

# Current Usage

| Stack Name                              | Description                                                                                                             |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| `yvr-stage-api-gw`                      | Manages resources relevant to the API Gateway for updating device configuration and user data                           |
| `yvr-stage-iot-rule`                    | Manages IoT rules for invoking the calibration lambda function                                                          |
| `yvr-stage-calibration-lambda-function` | Manages resources relevant to the Lambda function that calibrates the incoming data from device                         |
| `yvr-stage-device-lambda-function`      | Manages resources relevant to the Lambda function that performs CRUD operation of device configuration data in DynamoDB |
| `yvr-stage-user-lambda-function`        | Manages resources relevant to the Lambda function that performs CRUD operation of user data in DynamoDB                 |
