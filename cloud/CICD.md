---
layout: default
title: AWS Cloudformation
has_children: false
permalink: /docs/cloud/aws-cloudformation
parent: Cloud
has_toc: false
nav_order: 14
---


# CI/CD Pipeline with GitHub Actions

This document describes how to set up a CI/CD pipeline to automate the deployment and updates of your AWS resources using GitHub Actions.

## Prerequisites

Before you begin, make sure you have the following:

- An AWS account
- GitHub account
- A GitHub repository to store your CloudFormation templates

## Overview

The process follows these steps:

1. Developer pushes code to the GitHub repository.
2. GitHub Actions is triggered by a push event or a manual event.
3. GitHub Actions runs the defined workflow, deploying or updating the CloudFormation resources in AWS.

## Steps

### Step 1: AWS Configuration

1. Create an IAM role for GitHub Actions with programmatic access.
2. Assign necessary permissions for CloudFormation stack operations to the IAM role.
3. Save the IAM role arn.

### Step 2: Setting Up The GitHub Repository

1. Add your new lambda function / cloudformation yaml files to the repo.
2. In your GitHub repository, navigate to `Settings` > `Secrets`.
3. Add the AWS role arn, related S3 buckets, and the aws region as secrets.

### Step 3: Setting Up GitHub Actions Workflow

- CICD for Lambda Functions 
  - The file `.github/workflows/deploy_lambda.yml` defines the conditions for triggering the workflow, as well as the steps that are executed when the conditions are met.
  - Currently, the workflow is triggered when there is a push event in the main branch that includes changes in the `Lambda` directory.
  - The workflow then copies the zip files to the S3 bucket `yvr-lambda-functions` and updates the corresponding lambda functions. 

- CICD for Cloudformation Stack
  - upload_cloudformation workflow: upload cloudformation yaml files to the S3 bucket `yvr-cloudformation-templates`.
  - deploy_infras workflow: triggered by a manual action, deploy updates to the cloudformation stack.