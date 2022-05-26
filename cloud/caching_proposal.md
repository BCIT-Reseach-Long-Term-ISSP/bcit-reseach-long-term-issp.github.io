---
layout: default
title: Caching Proposal
has_children: false
permalink: /docs/cloud/redis_proposal
parent: Cloud
has_toc: false
nav_order: 11
---

# Summary

Implementing a caching layer into the EMA Project’s existing architecture will drastically speed up the dashboard application’s response time. I propose to use Redis as an application cache to load data to the cache only when changed since the dashboard performs many database reads. 

# Background

> “Caching **improves application response time** by storing copies of the most frequently used data on ephemeral but very fast storage. In-memory caching solutions, which hold the working set in speedy DRAM instead of slow spinning disks, can be extremely effective at achieving these goals. While caching is commonly used to improve application latency, a highly available and resilient cache can also help applications scale. Offloading responsibilities from the application’s main logic to the caching layer frees up compute resources to process more incoming requests.“
- [https://redis.com/solutions/use-cases/caching/](https://redis.com/solutions/use-cases/caching/)
> 

Without a caching layer, the Timestream database is queried every time a user views the website. This can add unnecessary cost per query if the data remains unchanged. With a Redis cache running on an EC2 instance, the database can be queried whenever the device publishes new data to the cloud. 

# Goals

- **Increased speed -** As a result of implementing caching, the dashboard’s users will have a seemingly instantaneous page load time.
- **A hosted API -** Running the Redis cache on an ECS instance will allow us to create a secure API for the dashboard team on the cloud which will create a simplified interface for both publishing to the devices and reading from the Timestream database..

# Proposed Solution

By running a Redis instance on an AWS ECS instance: 

- We can update Timestream and refresh the cache whenever the device publishes new data
- Having a server on the EC2 node will allow us to create an API for the dashboard hosted on the node which will simplify read requests and publishing for future teams
- Configuring a Redis instance ourselves VS running AWS Elasticache is more cost efficient
    
    ![ElastiCache cost](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/cache_figure_1.png)
       
    vs for 10 ECS instances (we would only need one to start)    
    ![ECS cost](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/cache_figure_2.png)
    
- We can configure a Kubernetes cluster to containerize the application allowing for future load balancing.

![A diagram showing the proposed architecture except the ElastiCache instance will be replaced with an ECS instance a Docker image within a Kubernetes container. ](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/cache_figure_3.png)

A diagram showing the proposed architecture except the ElastiCache instance will be replaced with an ECS instance a Docker image within a Kubernetes container. 

### Risks

- Added layer of complexity
- Maintaining a fresh cache
- If the buoy data publishes every 10 seconds, having a cache is redundant since the data keeps changing. In this case, I recommend keeping a cache to help speed up queries like a unique list of Device IDs or sensors which will not change as frequently.

### Milestones

- Exponential improvement for the dashboard’s load time
- Removing the need to filter all records every time a table is loaded for queries that do not frequently change
- Improved scalability for a large amount of sensors and buoys
