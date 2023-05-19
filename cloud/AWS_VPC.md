---
layout: default
title: AWS Virtual Private Cloud
has_children: true
permalink: /docs/cloud/aws-vpc
parent: Cloud
has_toc: true
nav_order: 17
---

# AWS Virtual Private Cloud

## Overview
Amazon Virtual Private Cloud (VPC) offers a secured, virtual networking environment that allows the launch of AWS resources in a defined virtual network. In our design, the `yvr-configuration` database and Lambda functions used for API gateways are positioned within the VPC, adding an extra layer of security. A VPC Endpoint is utilized to securely connect our VPC to Secrets Manager, without exposing the traffic to the public internet. This strategy effectively leverages VPC's isolation to enhance data security and network performance.

## Current Usage
We use VPC to isolate our resources of DB and Lambda functions from the public internet and use VPC Endpoint to connect to Secrets Manager.
![current_usage](assets/vpc/vpc_current_usage.png)

## How to Use

### Create a VPC