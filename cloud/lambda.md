---
layout: default
title: Lambda
has_children: false
permalink: /docs/cloud/lambda
parent: Cloud
has_toc: false
nav_order: 12
---

# AWS Lambda

## Overview

AWS Lambda is a compute service that lets us run code without provisioning or managing servers. It allows us to run isolated code on high-availability compute infrastructure and performs administration of the compute resources.

## How does it work?

AWS Lambda runs code in response to events such as HTTP requests, or IoT events.  When an event occurs, AWS Lambda automatically provisions the necessary compute resources to run your code. It then executes your code in a secure and isolated environment.  

Lambda automatically scales your functions in response to the incoming request rate. It can handle multiple requests simultaneously, allowing you to run highly scalable applications without worrying about infrastructure management.

## How did we develop a Lambda function?

1. Go to the AWS Lambda console and click on "Create function".

2. Select "Author from scratch" and fill in the following information:
    ![Create function](/cloud/assets/bidirectional_comm/1_create_function.png)

3. Go to the **Code** tab.  Develop source code in the code editor or upload a .zip file containing the code for the Lambda function

4. Go to the **Configuration** tab and customize the configuration settings if needed


## How did we deploy a Lambda function?
1. After we had finalized the source code and configuration of the Lambda function, we added the source code to GitHub repository for version control.  
   - `cloud-2023` is the GitHub repository
   - `src/lambda_functions` is the directory that contains the source code for the Lambda functions, and the corresponding `requirements.txt` file that defines the dependencies for the Lambda functions

2. GitHub Actions would then zip the source code, upload it to an S3 bucket, and use CloudFormation to create a new instance of Lambda function with the uploaded source code in the S3 bucket.  
   - `.github/workflows/deploy_lambda.yml` is the GitHub Actions workflow that deploys the Lambda function.  The name of the Lambda function has to be included in `names_of_lambdas_for_deployment` in the `Deploy changes of Lambda functions` step
   - `src/cloudformation/lambda_function.yml` is the CloudFormation template that defines the configuration settings for the Lambda function
   - The naming convention of the Lambda function is `yvr-stage-{function_name}`.  For example, `yvr-stage-calibration-lambda-function` is the name of the Lambda function for calibration.
   - The configuration settings for the Lambda function were specified in the CloudFormation template, for example environment variables
   - The benefit of using CloudFormation to deploy the Lambda function is that it allows us to easily provision and manage instances of the Lambda function, along with other necessary resources such as IAM roles and CloudWatch logs.  It also allows us to easily update or rollback the Lambda function if needed.

## Current Usage

| Lambda Function Name | Description |
| -------------------- | ----------- |
| `yvr-stage-calibration`                    | Calibrates the incoming data from device and stores it to Timestream                                                             |
| `yvr-stage-device`                         | Performs CRUD operation of device configuration data in DynamoDB  and publishes the device configuration changes to an IoT topic |
| `yvr-stage-user`                           | Performs CRUD operation of user data in DynamoDB                                                                                 |
| `yvr-stage-cognito-get-users-info`         | Uses the AWS Cognito API to get user information                                                                                 |
| `yvr-stage-cognito-get-role`               | Uses the AWS Cognito API to get user role                                                                                        |
| `yvr-stage-cognito-add-update-delete-user` | Uses the AWS Cognito API to add, update, or delete a user                                                                        |