---
layout: default
title: AWS Timestream
parent: Back-end Server Architecture
grand_parent: Dashboard
permalink: /docs/dashboard/backend/aws-timestream
nav_order: 4
---
# AWS Timestream
The Timestream database is owned by the Cloud Team.
{: .fs-6 .fw-300 }

The AWS timestream is a server-less time series database optimized for IoT, edge, and operational applications. The pricing details are found at [AWS](https://aws.amazon.com/timestream/pricing/).

Of particular note is that **AWS does not charge by the amount of queries sent**; rather it is the **weight of the queries** that are considered for billing. The minimum size of a query is 10MB rounded to the nearest MB. 

Due to the fact that the timestream database is unidirectional (only accepting data from the device), the application needs to send SQL queries into the AWS cloud along with the credentials for the particular database and table. To achieve this, the application uses a custom query builder to build and package the query with credentials. Below is the implementation for the query builder which every request to the API uses to send AWS:

```jsx
// This function creates and initializes the query and querystring objects.
// Returns an array to be destructured into the seperate objects.
const createTSQuery = (
  queryString: string,
  clientToken?: string,
  maxRows?: number,
  nextToken?: string
): any => {
  //Configure the region
  AWS.config.update({ region: queryInfo.REGION });
  //Create credentials
  const credentials = new Credentials({
    accessKeyId: `${process.env.AWS_API_ACCESS_KEY}`,
    secretAccessKey: `${process.env.SECRET_ACCESS_KEY}`,
  });
  //Create the query object
  const timeStreamQuery = new TimestreamQuery({
    apiVersion: queryInfo.API_VERSION,
  });
  //Configure the query objects using credentials.
  timeStreamQuery.config.update({
    credentials,
    region: queryInfo.REGION,
  });
  //Create the query object.
  const queryParams: QueryParams = {
    ClientToken: clientToken,
    MaxRows: maxRows,
    NextToken: nextToken,
    QueryString: queryString,
  };
  //Pack query and query string objects into array.
  return [timeStreamQuery, queryParams] as const;
};
```

Note that clientToken, maxRows, and nextToken are values that can be used to optimize queries for example through scheduled queries that are run at intervals. The optimization will be left to the incoming teams to implement.