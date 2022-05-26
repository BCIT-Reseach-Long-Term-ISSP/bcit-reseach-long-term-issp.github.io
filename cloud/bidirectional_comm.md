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

There are two main ways to establish communication between AWS services and dashboard.

1. Integrate AWS SDK with dashboard API
2. Create unique API for Cloud services

The first option to integrate the AWS SDK with the dashboard team's API should be considered for future teams, as it helps consolidate all services into a single API service. However, since we were dealing with time constraints, we ended up resorting to the second option to help decouple dependencies between teams. 

We used the following cloud architecture schema to create a simple API using AWS API gateway and AWS Lambda.

![Cloud architecture of public lambda function](/cloud/assets/bidirectional_comm/1_public_lambda_diagram.png)
<figcaption align="center"><b>Cloud architecture for public Cloud API for IoT communication</b></figcaption>


### What is AWS API Gateway?
AWS API Gateway is a fully managed service that makes it easy for us to create, publish, maintain, monitor, and secure APIs at any scale. Using API gateway allows us to create RESTful APIs or even WebSocket APIs that enable two-way communication between AWS services and other applications specifically with the Dashboard.

### What is AWS Lambda?
AWS Lambda is a compute service that lets us run code without provisioning or managing servers. It allows us to run isolated code on high-availability compute infrastructure and performs administration of the compute resources. 


