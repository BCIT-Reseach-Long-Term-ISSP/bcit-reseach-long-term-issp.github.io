---
layout: default
title: Bi-directional Communication
parent: Cloud
has_children: true
permalink: /docs/cloud/bidirectional_communication
has_toc: true
nav_order: 9
---

# Bi-directional Communication

## Overview

So far, we have been focusing on ensuring data gets from the buoy sensors to the Dashboard through the cloud. But we also need to account for being able to communicate from the Client dashboard to specific buoys or even to individual sensors. This fine grain through the dashboard will be essential for changing sensor configurations such as setting measurement time intervals or even disabling a device entirely. 

### How will communication be facilitated?

We used the following cloud architecture schema to make communication as simple and robust as possible.

![Cloud architecture for bidirectional communication](/cloud/assets/bidirectional_comm/bidirectional_communication.png)
<figcaption align="center"><b>Cloud architecture for bidirectional communication</b></figcaption>


### What is AWS API Gateway?
AWS API Gateway is a fully managed service that makes it easy for us to create, publish, maintain, monitor, and secure APIs at any scale. Using API gateway allows us to create RESTful APIs or even WebSocket APIs that enable two-way communication between AWS services and other applications specifically with the Dashboard.

### What is AWS Lambda?
AWS Lambda is a compute service that lets us run code without provisioning or managing servers. It allows us to run isolated code on high-availability compute infrastructure and performs administration of the compute resources. 


### What is Amazon Cognito?
AWS Cognito is a fully managed identity and access management service provided by Amazon Web Services. It allows us to easily manage user authentication and further secures API Gateway.

### What is Amazon DynamoDB?
Amazon DynamoDB is a fully managed NoSQL database service provided by Amazon Web Services. It is designed to provide fast and predictable performance with seamless scalability. It enables us to store the configuration data provided by the dashboard.

### What is Amazon Timestream?
AWS Timestream is a fully managed, serverless time-series database service provided by Amazon Web Services. It is designed to handle the ingestion, storage, and query of time-series data at scale, making it ideal for applications such as IoT. 

### What is IoT Core?
AWS IoT Core is the platform that enables users to connect devices to AWS Services and other devices, secure data and interactions, and process and act upon device data. It allows to send the configuration data to the devices and read measurements from the scanners.

