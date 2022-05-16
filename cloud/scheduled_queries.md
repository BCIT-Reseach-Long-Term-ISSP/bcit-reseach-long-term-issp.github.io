---
layout: default
title: Timestream
parent: Cloud
has_children: false
permalink: /docs/cloud/ts-scheduled-queries
has_toc: false
nav_order: 4
---

# Introduction

This document will cover the costs, benefits, and potential downfalls that may come with using scheduled queries which were introduced in late 2021. 

The **schedule query feature** is a fully managed, serverless, scalable solution for computing and storing aggregates and other forms of preprocessed data. These scheduled queries are defined ourselves with specific inputs and the frequency the query must be run is included. Timestream will then automatically and periodically run the query and write the results into a destination table.

By implementing this feature in AWS, queries made from the dashboard team using SQL will be **faster** and **more affordable**. More details are outlined under the **Benefits** and **Cost** section.

# How To Use

1. Log in to AWS and navigate to the **Amazon Timestream** service.
2. On the left-hand navigation bar, select **Scheduled queries**.
    
    ![Untitled](Untitled%230.png)
    
3. Click **Create scheduled query** on the top right to create a new query.
4. Choose the preferred database to hold the destination table in and choose a table that the scheduled query results will be populated into. 
5. Provide a descriptive query name to identify the scheduled query. 

  ![Untitled](Untitled%231.png)
6. To be continued...

# Benefits

1. Using scheduled queries lowers the impact of unintentional, long-running queries. 
2. Because scheduled queries populate a destination table, not a source table, we can allow for better data security by only allowing access to source tables by scheduled queries, and allowing access to destination tables for developers. 
3. Destination tables containing aggregated data will contain much less data than the original source table. This results in faster queries and cheaper storage. 
4. Can query destination tables using SQL, just as you would with a regular Timestream table.
5. Such destination tables can have data retention policies attached to them as well to further optimize storage spending. 

# Cost

As mentioned in the **Benefits** section, destination tables that are populated by scheduled queries have cheaper storage than storing the data in the source table. Therefore, the data held within the destination table can be stored for much longer than if it were to be stored within the source table.

# Recommendations

On the dashboard, a possible recommendation for a feature implementation would be to allow users to refresh the map and query the destination table for the latest information on all or a selection of sensors. Maybe tag the map with a *Last Updated* timestamp?

# References

[https://docs.aws.amazon.com/timestream/latest/developerguide/scheduledqueries.html](https://docs.aws.amazon.com/timestream/latest/developerguide/scheduledqueries.html)

[https://awsapichanges.info/archive/changes/d05708-query.timestream.html](https://awsapichanges.info/archive/changes/d05708-query.timestream.html)