---
layout: default
title: EMA Docs V0.1
parent: Cloud
has_children: false
permalink: /docs/cloud/docs_v01
has_toc: false
nav_order: 3
---

# EMA Cloud Architecture

Created: February 7, 2022 1:15 AM
Last Edited Time: April 6, 2022 12:30 AM
Status: In Progress 🙌
Type: Architecture Overview

# Description

The AWS ecosystem can be compatible with most technologies, but external vendors
require added complexity and sometimes a custom plugin. Application Programming
Interfaces (APIs) can be built using **AWS Lambda functions as wrappers for API requests if necessary.**

Database backend is managed by timestamp data, which defines the requirement for AWS
Timestream or Timescale DB, as they use timestamps as the primary index for data. This is
not necessarily a constraint, but should be recognised for further development.

### Project Completed Architecture

![Untitled](EMA%20Cloud%20%2069012/Untitled.png)

# IoT Core

Establishes a connection with data sensors to receive data and route them over to Amazon Web Services (AWS) cloud infrastructure.

# IoT Thing

Establishes a connection with data sensors to receive data and route them
over to Amazon Web Services (AWS) cloud infrastructure.

- JS programmed sensor
    - [https://us-west-2.console.aws.amazon.com/iot/home?region=us-west-2#/thing/YVR_water_sensor1](https://us-west-2.console.aws.amazon.com/iot/home?region=us-west-2#/thing/YVR_water_sensor1)
- Python programmed sensor
    - [https://us-west-2.console.aws.amazon.com/iot/home?region=us-west-2#/thing/YVR_water_sensor2](https://us-west-2.console.aws.amazon.com/iot/home?region=us-west-2#/thing/YVR_water_sensor2)

Both simulator sensors are stored as an AWS EC2 instance AMI.

> An Amazon Machine Image (AMI) provides the information required to **launch an instance**. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you need multiple instances with the same configuration. You can use different AMIs to launch instances when you need instances with different configurations.
> 

# IoT Core MQTT Protocol

![Untitled](EMA%20Cloud%20%2069012/Untitled%201.png)

A protocol used to establish connections with the end device through **AWS Greengrass.**
Both sensor simulators are posting data to an AWS topic “water_sensor1”.

### MQTT - Message Queue Telemetry Transport Protocol

![Untitled](EMA%20Cloud%20%2069012/Untitled%202.png)

> “MQTT is a Client Server publish/subscribe messaging transport protocol. It is light weight, open, simple, and designed so as to be easy to implement. These characteristics make it ideal for use in many situations, including constrained environments such as for communication in Machine to Machine (M2M) and Internet of Things (IoT) contexts where a small code footprint is required and/or network bandwidth is at a premium.“
> 

*Citation from the official **[MQTT 3.1.1 specification](http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html)***

An example of the publisher-subscriber protocol from AWS:

[https://github.com/aws/aws-iot-device-sdk-python-v2/blob/main/samples/pubsub.py](https://github.com/aws/aws-iot-device-sdk-python-v2/blob/main/samples/pubsub.py)

# Serving Data from Cloud through API gateway

Kinesis

- TL;DR: Its a pipeline
    - Uses Kinesis Producer Library
    - Follows a Producer/Consumer flow
        - Producers can be sensors, agents, lambda functions
        - Consumers can be data lakes, lambda functions, etc
- Kinesis Data Stream vs Kinesis Firehose
    - Data stream is a singular stream of data
        
        ![Untitled](EMA%20Cloud%20%2069012/Untitled%203.png)
        
    - Firehose is an aggregate of data streams
        
        ![Untitled](EMA%20Cloud%20%2069012/Untitled%204.png)
        
- Documentation Links
    
    [Creating and Managing Streams](https://docs.aws.amazon.com/streams/latest/dev/working-with-streams.html)
    
    [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)
    

## Creating Data Stream

In the AWS Console, head over to the Kinesis. You’ll be greeted with a quick dashboard/summary of existing Streams, Firehoses or Data Analytic applications.
Click on the “Create Data Stream”

![Untitled](EMA%20Cloud%20%2069012/Untitled%205.png)

After clicking, you’ll be brought to a new page where we will be customizing the data stream.
Here we can include the data stream name, data stream Capacity, and various other settings.

### Naming the Data Stream

Name your data stream in the appropriate box, it should look like below:

![Untitled](EMA%20Cloud%20%2069012/Untitled%206.png)

### Choosing Data Capacity

Here we can choose the data capacity. In our case, since we’re aware of our data bandwidth we can select Provisioned; However, if you’re unaware of your data usage, you can use on-demand, and then change the capacity mode afterwards to suit your needs.

![Untitled](EMA%20Cloud%20%2069012/Untitled%207.png)

After select our capacity mode, we need to provide number of “shards” or ordered streams of data. Please be aware, each shard has a maximum write and read capacity. If you don’t care about order you can just use one shard (assuming its within the read/write capacity). If you need help deciding how many “Shards” you require, AWS provides a Shard estimator.

![Untitled](EMA%20Cloud%20%2069012/Untitled%208.png)

### 

A important note to take into consideration: provisioned streams can be cheaper but are of fixed pricing while on-demand streams can vary dependent on usage. You can switch between the capacity modes twice every 24 hours.

The various settings will be set by default to the following and can be edited afterwards.

![Untitled](EMA%20Cloud%20%2069012/Untitled%209.png)

To finish creating the data stream Click on the orange “Create data stream” button

![Untitled](EMA%20Cloud%20%2069012/Untitled%2010.png)

### Configurations

Once the data stream is created; we’ll be brought to the data streams summary page. From here we can make configuration changes by clicking on the Configuration tab located below the Data Stream Summary.

![ARN is blacked out for privacy reasons.](EMA%20Cloud%20%2069012/Untitled%2011.png)

ARN is blacked out for privacy reasons.

### Pricing for On-Demand (Oregon Region)

![Untitled](EMA%20Cloud%20%2069012/Untitled%2012.png)

### Pricing for Provisioned (Oregon Region)

![Untitled](EMA%20Cloud%20%2069012/Untitled%2013.png)

## Dumping Data Stream to an Endpoint

To dump data in the data stream into an endpoint or to apply a transformation to the data has to be done through “Delivery Streams” or “Data Firehose”. To access the Delivery streams menu, you can find it on the left-hand side of Amazon Kinesis or in the dashboard via the Data firehose section and clicking on the number of existing delivery streams you have; in our case, 2.

![Left Navigation Menu](EMA%20Cloud%20%2069012/Untitled%2014.png)

Left Navigation Menu

![Main Amazon Kinesis Dashboard](EMA%20Cloud%20%2069012/Untitled%2015.png)

Main Amazon Kinesis Dashboard

### Creating Delivery Streams

From the Delivery Stream page we can see a quick summary of existing delivery streams and create new ones.

In the delivery Stream summary page, click on the orange “Create delivery stream”

![Untitled](EMA%20Cloud%20%2069012/Untitled%2016.png)

Upon entering the “Create a delivery stream page” you will be greeted with a quick infographic of how it works.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2017.png)

Scrolling down a little, we begin to see how to set a delivery stream up. We need to select a Source of data and a Destination for the data.
In our case we want the Source to be our data stream, and our destination a S3 bucket which we can select from the drop-down menus.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2018.png)

New options will be unlocked below allowing us to select our data stream. We select the data stream via the browse button, or if you don’t have one set up yet you can use the create button just right of the Browse button.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2019.png)

The next step (Transform and Convert Records) is optional, and is only used if you wish to transform the data via an AWS lambda function. There will be a more in-depth look into this in another section.
Once we’re done selecting out data stream, we get to name our delivery stream.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2020.png)

In the destination settings, we can select the S3 bucket we wish the data to flow into via the browse button. If it doesn’t exist, we can also create a new one via the create button.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2021.png)

Within the Destination settings, we can enable or disable Dynamic partitioning which creates targetable partitions in our data lake for specific AWS lambda functions to dump data into. This will incur more costs if enabled, and it cannot be disabled once set. For more information on costs visit: [https://aws.amazon.com/kinesis/data-firehose/pricing/](https://aws.amazon.com/kinesis/data-firehose/pricing/)

In our case we are only using the S3 bucket as a storage space for raw data and transformed data (in a later section)

Once all you’re happy with your configurations, click on the orange “create delivery stream” button

![Untitled](EMA%20Cloud%20%2069012/Untitled%2022.png)

### Transforming Data via the Delivery Stream

To transform data coming from the data stream before it goes to the delivery stream destination, we need to enable it in the Transform and Convert Records section mention earlier.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2023.png)

Once enabled, options to select our AWS Lambda function, buffer size, and buffer interval is made available.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2024.png)

Because the data is being ran through a lambda function there is a possibility that the resulting data may take up more space than the original data, buffer size is there to accommodate the data expansion.
Buffer interval is the time Kinesis Firehose buffers incoming data before invoking the lambda function. So In the screenshot above, it will buffer either 3MB of data or wait 60 seconds before invoking the lambda function.
If we run into issues with data being delayed in the parsed S3 bucket, we can change the buffer size to be smaller to increase the number of times the S3 bucket will have incoming data.

# Choosing The Appropriate Database

## Initial Phase

The initial phase of the EMA Research Project used **TimescaleDB**, a relational database management system built on top of PostgreSQL and accessible via SQL. Integration with AWS is simple as data can be pipelined and normalized from AWS IoT Core to TimescaleDB using AWS Lambda which is triggered through IoT Rules.

![https://www.timescale.com/blog/content/images/2019/09/architecture.png](https://www.timescale.com/blog/content/images/2019/09/architecture.png)

On the client (dashboard) side of things, libraries are available to connect the client-side to TimescaleDB because of its utilization of PostgreSQL. [Example code here.](https://github.com/timescale/examples/blob/master/clients/tsdb-node-client.js')

| Pros | Cons |
| --- | --- |
| Full SQL | Fixed schema |
| Fast data ingestion, in other words, movement of data from one more sources to a destination to be stored and analyzed | Security and data privacy can be at risk |
| IP access control, controlling network access to TimescaleDB instance |  |
| Better value at higher loads |  |

![Untitled](EMA%20Cloud%20%2069012/Untitled%2025.png)

## Phase 4

The architecture below has been remodeled based on the initial architecture above. 

![Untitled](EMA%20Cloud%20%2069012/Untitled%2026.png)

# AWS Timestream

Queries with projections and predicates including time ranges, measure names, and/or dimension names enable the query processing engine to prune a significant amount of data and help with lowering query costs. It is recommended for the dashboard team to use more filtered queries since it is priced according by bytes.

([https://docs.aws.amazon.com/timestream/latest/developerguide/metering-and-pricing.queries.html](https://docs.aws.amazon.com/timestream/latest/developerguide/metering-and-pricing.queries.html))

## Key Concepts

- Time series - a sequence of records over a time interval
- Record - a single data point
- Dimension - attribute describing metadata
- Timestamp - indicates when the measure was collected or ingested
- Table - container for related time series with timestamp, dimensions, and measures
- Database - container for all tables

## Potential Queries for Client

- Get all sensors’ data from a given start and end timestamp
    - What timestamp format should be followed?
- Get all records of a single sensor record (Historical data)
- The above without a start and end timestamp (if regularly queried given a frequency - weekly, monthly, etc. then this can be part of the query - frontend or backend?)
- Filter by a specific sensor attribute (i.e., pH, temperature, TDS, pressure) and sort by increasing/decreasing order
- Get a single measurement at the current time or at a specific time
- Get all readings from a specific sensor, grouped by sensor ID
- Get the latest readings, sort by max time (UNIX)
- Get all sensor IDs —> SELECT DISTINCT
- Best Practices: Queries
- Great outline to follow to optimize both performance and cost

[https://docs.aws.amazon.com/timestream/latest/developerguide/queries-bp.html](https://docs.aws.amazon.com/timestream/latest/developerguide/queries-bp.html)

- AWS Timestream Query Language Reference: [https://docs.aws.amazon.com/timestream/latest/developerguide/reference.html](https://docs.aws.amazon.com/timestream/latest/developerguide/reference.html)

## Best Practices: Data Modeling

As of November 30, 2021, AWS introduced an alternative to single-measure records called **multi-measure records**, as well as two new faster and more cost-effective capabilities called scheduled queries and magnetic storage writes.

**Multi-measure records:**

- Most suitable for multiple metrics that occur at the same timestamp
- All measures from the same timestamp appear as different columns stored in the same row

**Single-measure records:**

We are using single-measure records for guaranteed scalability when adding more sensors to the edge devices.

- Most suitable for when metrics occur at different time periods (ex. new record is written every time the pH dips below 6.5)
- Each measure has its own timestamp and is stored as its own record in Timestream
- Using multi-measure records and having both device and dashboard teams publish and subscribe to a general topic instead of a specific topic pertaining to a particular device id

[https://docs.aws.amazon.com/timestream/latest/developerguide/data-modeling.html](https://docs.aws.amazon.com/timestream/latest/developerguide/data-modeling.html)

## Sample Queries

The following queries can be tested directly in the AWS Timestream Query Editor.

![Untitled](EMA%20Cloud%20%2069012/Untitled%2027.png)

### Create SQL query to list all unique device IDs

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE time BETWEEN ago(365d) AND now()
```

```sql
SELECT distinct deviceSELECT	 *,
        MAX(time) as "most_recent_time"
FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE buoy_id = '1'
GROUP BY buoy_id,
		measure_name,
        time,
        measure_value::double,
        measure_value::booleanId
FROM "YVR_water_sensor"."EMA_C22_main_data"
```

### Create SQL query one device - all metrics - current

```sql
SELECT	*,
        MAX(time) as "most_recent_time"
FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE buoy_id = '1'
GROUP BY  buoy_id,
					measure_name,
	        time,
	        measure_value::double,
		      measure_value::boolean
```

### Create SQL query for all devices - all metrics - current

```sql
SELECT	*,
        MAX(time) as "most_recent_time"
FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
GROUP BY  buoy_id,
					measure_name,
	        time,
	        measure_value::double,
		      measure_value::boolean
```

### Create SQL query to display one device - one metric - historic

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE buoy_id = '1'
AND measure_name = 'ph'
```

### Create SQL query to list all devices - one metric - historic

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE measure_name = 'ph'
```

### Create SQL query to list some devices - one metric - historic

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE measure_name = 'ph'
AND buoy_id IN ('1', '2')
```

### Create SQL query to list all devices - all metrics- Time frame of DAYS

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE time BETWEEN ago(365d) AND now()
```

### Create SQL query to list all devices - one metric, limited of 5 records- Time frame of days

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00"
WHERE time BETWEEN ago(365d) AND now()
ORDER BY time DESC LIMIT 5
```

### Create SQL query to list all devices - all metrics- between 2 time frames of HOURS

```sql
--Get all data from 6 hours ago til now
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00" 
WHERE time BETWEEN ago(6h) and now()
```

### Create SQL query to list all devices - one metric- Time frame of HOURS

```sql
--Get all temperature data from the past 24 hours
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00" 
WHERE measure_name = 'temp' AND time >= ago(24h)
```

### Create SQL query to give back data within a time frame of MINUTES

```sql
SELECT * FROM "YVR_water_sensor"."EMA_C22_main_data_v00" 
WHERE time BETWEEN ago(10m) and now()
```

In the future, this can become a scheduled query depending on how often we want to receive data from the device team. We recommend specifying the names/attributes of the needed measures when more sensors are added to prevent adding unnecessary bytes to the queries

## Best Practices: Data Retention

AWS offers data storage tiering and supports two storage tiers: a **memory store** and a **magnetic store**.

- **Memory store:** Optimized for point-in-time queries; shows how data has changed over a period of time. Typically, these queries process small amounts of **recent** data that has been sent to Timestream
- **Magnetic store:** Optimized for fast analytical queries and its purpose is more for long-term data storage. These queries process medium to large volumes of data

| Memory Store | Magnetic Store |
| --- | --- |
| Optimized for point-in-time queries | Optimized for fast analytical queries |
|  |  |

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