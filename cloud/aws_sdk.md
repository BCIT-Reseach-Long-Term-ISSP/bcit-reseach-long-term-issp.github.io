---
layout: default
title: AWS SDK
has_children: false
parent: Cloud
permalink: /docs/cloud/aws_sdk
has_toc: false
nav_order: 10
---
# AWS SDKs & Accessing Timestream

We can use the AWS SDK to access Timestream outside of the console - ie. to serve the data so that the dashboard team is able to get and display data for the dashboard. Specifically, Timestream supports two SDKS: the Write SDK and the Query SDK (see [Using the AWS SDKs](https://docs.aws.amazon.com/timestream/latest/developerguide/getting-started-sdks.html) ). 

### Write SDK

- used to perform CRUD operations
- insert timeseries data into Timestream

### Query SDK

- query existing data that is already stored in Timestream

### Installing the AWS JS SDK

We used the [node.js SDK](https://docs.aws.amazon.com/timestream/latest/developerguide/getting-started.node-js.html) in this iteration, but there are other SDKs available in different languages. Timestream documentation provides a link to this sample repo with a [working sample.](https://github.com/awslabs/amazon-timestream-tools/tree/mainline/sample_apps) A barebone repo with just the code required for the EMA project can also be found on github - [link here](https://github.com/BCIT-Reseach-Long-Term-ISSP/cloud2022/tree/master/timestream-query-sample). For both examples, ensure that you have configured your AWS Credentials (links below).

The general steps are listed below, with links to the detailed AWS documentation pages.

1. Install [node](https://nodejs.org/en/) if not yet installed
2. In a new node.js app, install the AWS SDK for JS with your preferred package manager. 
    1. [Installing AWS JS SDK Documentation](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/installing-jssdk.html)
    2. For example, with npm:
        1.  `npm install @aws-sdk/client-timestream-query` ([docs](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-timestream-query/index.html#aws-sdkclient-timestream-query))
        2.  `npm install @aws-sdk/client-timestream-write` ([docs](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-timestream-write/index.html#aws-sdkclient-timestream-write))
3. Configure AWS Credentials
    1. [Getting your AWS Credentials](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-credentials-node.html) (*note: this link leads to an older v2 of the SDK, but worked for our sample) 
    2. [Loading your AWS Credentials](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/loading-node-credentials-shared.html)
4. Create Package.json as needed (or just install the required packages if using samples)
5. Write the node.js code, which includes the new instances of the Timestream clients for both Write and Query SDKs, SQL queries to query the specific data you’re looking for, and the code to use the functions provided by the SDKs to retrieve data from the database ([docs](https://docs.aws.amazon.com/timestream/latest/developerguide/code-samples.html)).


{: .fs-6 .fw-300 }