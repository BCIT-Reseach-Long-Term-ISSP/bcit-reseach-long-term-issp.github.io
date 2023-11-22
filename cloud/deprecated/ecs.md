---
layout: default
title: Proposal - CI/CD Pipeline Using ECR, ECS, and GitHub
grand_parent: Cloud
parent: Deprecated
has_children: false
permalink: /docs/cloud/deprecated/ecs
has_toc: false
---

# Introduction

Deprecated
{: .label .label-red }

This document outlines a proposal to create a CI/CD pipeline using ECR, ECS, and GitHub. As of May 2022, we are using Firebase Hosting to deploy the current web application. Because this project is still in its early stages, it was more beneficial to use Firebase Hosting due to its quick setup and lower learning curve compared to AWS. However, deployment using AWS would be beneficial to limit third-party dependency since the microservices that the project is mainly comprised of are from AWS and because their ecosystem is meant to be all-inclusive. 

In the following sections, you will learn about the advantages of ECR and ECS in regard to their cost and security, as well as the benefits of integrating a CI/CD pipeline.

# What is Docker?

Before continuing, understanding Docker is the first step.

Docker is an open-source containerization platform that allows developers to easily package, ship, and run any application as a lightweight, portable, self-sufficient container, which can be run on any machine in an efficient manner. Self-sufficient meaning that each container contains everything an application or part of an application needs to run. This allows for more consistency due to the same software, operating system, and hardware configurations.

![Docker Architecture](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/cloud/assets/ecs_2.png?raw=true)

The main benefit is that it is highly scalable. For example, as the application grows, it may require 10 more containers to run. It is more time-efficient to utilize containers rather than adding 10 more hosts. With Docker’s design, although multiple containers may run on the same host, we can ensure that each application is isolated which is useful when modifying and updating the application. 


# What is ECS?

Amazon ECS or Elastic Container Service is a container management service dependent on Docker. This service quickly launches, exits, and manages Docker containers on a cluster of EC2 virtual machine instances. These containers can be launched using the AWS management console or programmatically using available SDK kits provided by AWS. A huge benefit when using ECS is you can migrate applications to the cloud without having to alter the original codebase (i.e., New environment parameters). 

Based on the example above, if we were to solely use an **EC2** instance to host an application, it would be one-to-one. Whereas with containers, we can launch 10 different applications on the same EC2 instance.

Because of AWS’s pay-as-you-go approach, costs can be diminished using ECS because the application consumes the resources only at the time that it needs them.

# What is ECR?

Amazon ECR or Elastic Container Registry is a container image registry where users or EC2 instances can access container repositories and images. An image contains the application code and all dependencies that are required to run said application, such as libraries, packages, and the language runtime for interpreted languages. All images that are stored within ECR are only accessed through HTTPS and are also encrypted. Access can also be restricted to users or services with IAM policies. 

![Container Image Architecture](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/cloud/assets/ecs_1.png?raw=true)

# Goals

- Deliver changes with all potential bugs and issues being caught before the deployment stage
- Improved scalability (i.e., adding postprocessing for ingested data)
- Increased cost-efficiency
- Improved security
- Higher availability with load balancing to automatically scale request-handling capacity in response to incoming traffic across multiple instances (i.e., Elastic Loading Balancing (ELB))

# Proposed Solution

By integrating a CI/CD pipeline using GitHub Actions, the setup is very simple as well as a multitude of resources and workflows that can be used based on our needs. With GitHub Actions, we can set any webhook on GitHub as an event trigger for an automation or CI/CD pipeline  (i.e., Pull requests, push).  Maintaining releases will be automatic, which reduces overhead. 

A workflow is made available to deploy to Amazon ECS.
![ECS Workflow](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/cloud/assets/ecs_3.png?raw=true)

To integrate the pipeline, here is an informative step-to-step guide: https://blog.devgenius.io/host-any-app-to-aws-and-github-using-continuous-deployment-ci-cd-pipeline-step-by-step-d4150dbee2e8

# Cost

Below is a basic overview of the general cost of various parameters for all services required:

## ECR

- **Storage:** $0.10 per GB / month for data stored in repositories
- **Data Transfer-In:** Free

## ECS

- Only pay for the AWS EC2 instances and attached EBS volumes (Storage). Due to the current scope of the project, it is suggested to use the **t2.micro** instance which currently sits at an hourly rate of $0.0116 or approximately $8.35 per month.

## CI/CD with GitHub

- Currently, each GitHub account receives a certain amount of free minutes per month and storage. Minutes reset every month, while storage usage doesn’t
    
    
    | Product | Storage | Minutes (per month) |
    | --- | --- | --- |
    | GitHub Free | 500 MB | 2,000 |
    | GitHub Pro | 1 GB  | 3,000 |

- Additional minutes used are charged with a pay-as-you-go approach. Rates depend on your selected instance
    
    
    | OS | Price per additional minute (USD) |
    | --- | --- |
    | Linux | $0.008 |
    | Windows | $0.016 |
    | MacOS | $0.08 |

- The projected monthly cost will remain at $0.00 per month due to the current scope of the project

# Resources

[https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)

[https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)

[https://www.youtube.com/watch?v=46mFdtpy3NQ&t=600s&ab_channel=Simplilearn](https://www.youtube.com/watch?v=46mFdtpy3NQ&t=600s&ab_channel=Simplilearn)