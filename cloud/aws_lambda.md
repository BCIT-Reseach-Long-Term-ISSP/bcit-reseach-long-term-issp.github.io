---
layout: default
title: AWS Lambda
has_children: false
permalink: /docs/cloud/bidirectional_communication/aws_lambda
grand_parent: Cloud
parent: Bi-directional Communication
has_toc: false
---

# AWS Lambda

## Overview

AWS Lambda is a compute service that lets us run code without provisioning or managing servers. It allows us to run isolated code on high-availability compute infrastructure and performs administration of the compute resources.

## How does it work?

AWS Lambda runs code in response to events such as HTTP requests. It automatically manages the compute resources required by that code. It starts our code when needed and scales automatically, from a few requests per day to thousands per second. We pay only for the compute time we consume - there is no charge when our code is not running.

## How did we use it?

We used AWS Lambda to create a public API that allows the Dashboard to communicate with the IoT devices. We created a Lambda function that is triggered by an HTTP request from the Dashboard. The Lambda function then sends a message to the IoT device using the AWS IoT Core service. The IoT device then responds to the message and the Lambda function returns the response to the Dashboard.

## How to create a Lambda function?

1. Go to the AWS Lambda console and click on "Create function".

2. Select "Author from scratch" and fill in the following information:

![Create function](/cloud/assets/bidirectional_comm/1_create_function.png)

3. Click on "Create function" and you will be redirected to the function's page. Scroll down to the "Function code" section and click on "Actions" and then "Upload a .zip file". Upload the .zip file containing the code for the Lambda function or copy and paste the code directly into the code editor.

## Configuring the Lambda function

### IAM Role

The Lambda function needs to have the correct permissions to be able to communicate with the IoT devices. To do this, we need to create an IAM role that has the following policies attached:

- AWSLambdaBasicExecutionRole
- AWSIoTDataAccess

In addition to that, we must include any other policies that are required by the Lambda function as needed. 

### Memory

The amount of memory allocated to the Lambda function will depend on the size of the code and the amount of memory required to run the code. The more memory we allocate to the function, the more CPU power we allocate to it. The amount of memory allocated to the function will also affect the amount of time it takes to run the code.

In our case, we allocated 256 MB of memory to the function and it was more than enough to run the code and showed significant improvements in the amount of time it took to run the code. 

We can determine the optimal amount of memory to allocate to the function by running the code with different amounts of memory and measuring the amount of time it takes to run the code.

AWS PowerTuning is a tool that can be used to determine the optimal amount of memory to allocate to the function. It runs the function with different amounts of memory and measures the amount of time it takes to run the code. It then determines the optimal amount of memory to allocate to the function based on the results of the tests.

### Timeout

The timeout for the Lambda function will depend on the amount of time it takes to run the code. The maximum timeout is 15 minutes. If the function takes longer than the timeout to run, it will be terminated and the code will not be executed. 


