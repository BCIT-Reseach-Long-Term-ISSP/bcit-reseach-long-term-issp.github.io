---
layout: default
title: AWS Cloudformation
grand_parent: Cloud
parent: Deprecated
has_children: false
permalink: /docs/cloud/deprecated/aws-cloudformation
has_toc: false
---

# Overview

Deprecated
{: .label .label-red }

Amazon Web Services (AWS) CloudFormation is a service that helps users model, provision, and manage their AWS infrastructure resources in a consistent, predictable, and repeatable manner. It enables the creation, modification, and deletion of a collection of resources together as a single unit, referred to as a "stack."

## Key Features / Concepts:

1. Templates: CloudFormation uses JSON or YAML formatted templates to define the desired resources, their properties, and their relationships. These templates serve as a blueprint for creating and configuring AWS resources.

2. Stacks: A stack is a collection of AWS resources created from a CloudFormation template. Stacks can be created, updated, or deleted as a single unit, allowing for easy management of resources.

3. Change Sets: Change sets allow users to preview the changes that will be made to a stack before executing them. This helps to identify potential issues before they impact the environment.

4. Nested Stacks: CloudFormation supports the creation of nested stacks, which allows users to break down complex architectures into smaller, reusable components.

# Current Usage

![cloudformation - current usage](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/cloudformation/aws_chart.png)

The API gateway, together with the integrated Lambda functions, that exposes the endpoints for device configuration purposes are currently defined in cloudformation templates.

- Stack name: device-config-stack
- Template: cloudformation/ApiGatewayMaster.yaml

The template `ApiGatewayMaster.yaml` includes 6 nested stacks. Each defines a group of related resources. The nested stacks are

- `ApiGatewayStack`: defines the REST Api Gateway
- `AuthValidationLambdaStack`: defines all the resources and permissions necessary for the /AuthValidation endpoint
- `DeviceConfigLambdaStack`: defines all the resources and permissions necessary for the /config endpoint
- `CalibrationPointsLambdaStack`: defines all the resources and permissions necessary for the /calibration_points endpoint
- `DevicesLambdaStack`: defines all the resources and permissions necessary for the /devices endpoint
- `SensorsLambdaStack`: defines all the resources and permissions necessary for the /sensors endpoint
