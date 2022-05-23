---
layout: default
title: IoT to S3
has_children: false
permalink: /docs/cloud/iot-s3
parent: Cloud
has_toc: false
nav_order: 7
---

# Getting Data from IoT Core to S3 via Kinesis

## Setting up IoT Act Rule
In AWS IoT Core, on the left hand navigation menu, scroll down to click on "Act" and then click on "Rules". It should be highlighted in orange if you've already opened it.

![IoT to S3 - Navigation](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3.PNG)

### Creating the Rule
To create the required rule to dump the MQTT messages onto the Kinesis data stream, click on the "create" located on the right hand side.

![IoT to S3 - Create](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_create.PNG)

In the Create rule window, provide a name and description for the rule.

![IoT to S3 - Name](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_name.PNG)

We can select the SQL version you're most comfortable with in the Rule Query Statement. In our case we're using "2016-03-23"

![IoT to S3 - SQL](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_sql.PNG)

When providing the "Rule Query Statement" provide the follow:
```
SELECT *, topic(3) as buoy_id FROM 'aws/+/+/data/#'
```

We're adding in buoy_id into the message so we know which physical buoy the data is coming from.
Please refer to: https://bcit-reseach-long-term-issp.github.io/docs/smart-device/communication-protocol/mqtt#broker-namespace-topics for more information on the topic formatting.

Now continuing on, In the "Set one or more actions" click on "Add Action"
![IoT to S3 - Action](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_action.PNG)

More options will appear, we're looking for "Send a message to an Amazon Kinesis Stream". Select it and scroll down and click on the "Configure action" button.
![IoT to S3 - Kinesis](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_kinesis.PNG)

In the configure Action menu, select the Kinesis data stream you wish to dump data on, via the "Choose a resource" drop down. If you cannot find the AWS resource, you can always create a new data stream. Refer to https://bcit-reseach-long-term-issp.github.io/docs/cloud/kinesis#creating-data-stream if you require more information about setting up a new data stream.

![IoT to S3 - Configure Action](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IoT_to_S3_action2.PNG)

In the partition key, we can leave it as what they suggest:
```
${newuuid()}
```

In the roles section, change it to "EMA-C22-CloudServices"

Then finish up by clicking on add action

We can setup an optional error action but we haven't set it up yet. Perhaps this can be updated down the road.

Once done, click on the create rule button on the buttom. 

## Kinesis Data Stream and Delivery Stream
Refer to the Kinesis page for information on setting up data streams and delivery streams.
https://bcit-reseach-long-term-issp.github.io/docs/cloud/kinesis

### Setting up Data Transform
Refer to Transforming Data via the Delivery Stream from the following link:
https://bcit-reseach-long-term-issp.github.io/docs/cloud/kinesis#transforming-data-via-the-delivery-stream

When creating the delivery stream, in the optional "Transform and Convert Records" section, select the appropriate AWS Lambda function after enabling data transform, here we select "datatransform" which is a javascript that takes the data stream payload, converts it into a neatly formatted JSON. See the code snippet below.

```
'use strict';
console.log('Loading function');
exports.handler = (event, context, callback) => {
    /* Process the list of records and transform them */

    const output = event.records.map((record) => {
        console.log(record.recordId);
        const payload =JSON.parse((Buffer.from(record.data, 'base64').toString()))
        const resultPayLoad = {

            "do": payload.do,
            "ec": payload.ec,
            "liqlev": payload.liqlev,
            "ph": payload.ph,
            "tds": payload.tds,
            "tbd": payload.tbd,
            "wf": payload.wf,
            "wp": payload.wp, // remove as sensor doesn't exist
            "temp": payload.temp,
            "buoy_id": parseInt(payload.buoy_id), // will be str otherwise
        };
        
        return {
            recordId: record.recordId,
            result: 'Ok',
            data: (Buffer.from(JSON.stringify(resultPayLoad))).toString('base64'),
        };
    });
    console.log(`Processing completed.  Successful records ${output.length}.`);
    callback(null, { records: output });
};
```

We now have everything setup for data to flow from IoT Core through Kinesis to a S3 bucket.
