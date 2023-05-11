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

## Key Features:

1. Templates: CloudFormation uses JSON or YAML formatted templates to define the desired resources, their properties, and their relationships. These templates serve as a blueprint for creating and configuring AWS resources.

2. Stacks: A stack is a collection of AWS resources created from a CloudFormation template. Stacks can be created, updated, or deleted as a single unit, allowing for easy management of resources.

3. Change Sets: Change sets allow users to preview the changes that will be made to a stack before executing them. This helps to identify potential issues before they impact the environment.

4. Versioning and Rollbacks: CloudFormation supports versioning of templates and automatically rolls back to a previous stable state if stack creation or update fails. This ensures that resources are not left in an inconsistent state.

5. Drift Detection: Drift detection helps users identify resources that have been modified outside of CloudFormation, ensuring that the infrastructure stays in sync with the template.

6. Nested Stacks: CloudFormation supports the creation of nested stacks, which allows users to break down complex architectures into smaller, reusable components.


# Current Usage
![cloudformation - current usage](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/cloudformation/aws_chart.png)

The API gateway, together with the integrated Lambda functions, that exposes the endpoints for device configuration purposes are currently defined in a cloudformation template. 

- Stack name: config-stack
- Template: infrastructure.yaml

