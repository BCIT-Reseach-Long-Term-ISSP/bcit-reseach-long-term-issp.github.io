---
layout: default
title: IoT Core to Timestream
has_children: false
permalink: /docs/cloud/iot-timestream
parent: Cloud
has_toc: false
nav_order: 7
---

# Getting Data from IoT Core to Timestream

## IoT Core Service
Login to AWS and search for the service AWS IoT. In order to see data flowing from device to the cloud, the user needs to subscribe to a topic. To view individual sensor value, the user needs to subscribe to each sensor topic. A screenshot below shows subscription to the Turbidity 'tbd' sensor.

![Subscribe Topic](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_CORE_SUBSCRIBE.png)

Next in order for the topics to persist after the user logs out, the user needs to add it to favourite by click on the heart picture under the section 'All subscriptions' then it will be in the 'Favorites' section. Here is the picture of all sensors as favourite. If the user wants to see all data, they will only have to select the '#' topic. A screenshot below shows the left side of all favourite topics and some of values can be seen.

![Favourite Topics and data seen from device](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_CORE_FAVOURITES.png)

In order to route the information coming into IoT core, we need to setup a "message routing rule".

## Setting up an IoT Message Routing Rules
In AWS IoT Core, on the left hand navigation menu under "Manage", scroll down to click on "Message routing" and then click on "Rules".

![Message Routing Rule](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_CORE_MSG_ROUTING.png)

This will open a new Rules page where a orange button "Create rule" on the right hand side is visible. Click on that button.

![Message Routing Rule](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_CORE_CREATE_BUTTON.png)

It will open a new page, where the user have to fill in the information by giving a rule name and description. Click on Next.

![Message Routing Create Rule Step1](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_MSG_ROUTING_RULE_STEP1.png)

For step 2 update the SQL statement using the following: <SELECT *, topic() as topic FROM 'device/reading/sensor/#'>. Breaking down the SQL statement we have first we will retrun '*' which is just the value given by the topic. Next topic() value is equivalent to 'device/reading/sensor/<TOPIC>' and the '#' denotes a wildcard so it query for any sensor topic data the device sends to IoT core. Click on next. Below is a screenshot of step 2.

![Message Routing Create Rule Step2](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_MSG_ROUTING_RULE_STEP2.png)

Disclaimer: We asked the device team to give us a deviceID instead just called it 'device' and a sensorID instead a generic abbreviation of the sensor name 'flw' (Water Flow sensor) but despite our push, I assume they did not have enough time to make the change.

On step 3, under the "Rule actions" section select Lambda as the action and select the lambda function. For this example I already made a lambda function but the user will click on the "Create a Lambda Function" if it does not exist. I will go more in depth about the lambda function responsiblity in the next section but the main point of this lambda function is to take the raw sensor value from the deivce, apply two calibration data point formula, and send the data to the timestream. Below is the screenshot of step 3. Click Next

![Message Routing Create Rule Step3](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/IOT_MSG_ROUTING_RULE_STEP3.png)

For the fourth step, click on Create button to create the Message Routing Rule.

## Lambda Function
Lambda Function code is stored in GitHub: https://github.com/BCIT-Reseach-Long-Term-ISSP/cloud-2023/blob/main/src/lambda_functions/calibration.py

Lambda Function has three main responsiblity. First responsiblity is to grab the two data points in dynamodb that is used for the calibration formula. The cloud team had to mock the data for calibration as the dashboard team did not have the values for all sensors. It is also stored in the North Viginia as the other cloud team (BBY) did not migrate our data to west-2 which was agreed upon.

Below is the screenshot of item we created
![Dynamodb item containing calibration point data of each sensor](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_DYNAMODB_ITEM.png)

Screenshot shows the JSON view of the item data format
![Dynamodb item in detail using JSON view](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_DYNAMODB_ITEM_JSONVIEW.png)

The retrival of this data is done through a lambda layer by calling the function configretriver.config_handler. The lambda layer code can be found in github also: https://github.com/BCIT-Reseach-Long-Term-ISSP/cloud-2023/blob/main/src/lambda_layers/python/configretriever.py. This function will return the json object of the following values needed for calibration formula.

![Lambda Layer JSON object return](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_LAYER.png)

It will then parse the json object returned and apply the calibration formula using two points. Below is the screenshot.

![Lambda function calibration formula](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_CALIBRATION_FORMULA.png)

The next main responsiblity is to send the calibrated value along with other information such as "device name", "sensor name", and "sensor_unit" to the Timestream DB. Below is the screenshot of the code snippet.

![Lambda function writing to TimeStream DB](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_TIMESTREAM.png)

The final main responsibility is to check the calibrated data exceed either the min or max value of the sensor threshold. If it does, a user setup for email notification would be notify of the anomaly value which is used to check if there is abnormal weather pattern incoming or device needs to be check on. Below is the screenshot of the lambda function calling the 'should_alert' function to determine if email notication is called.

![Lambda function alert](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_ALERT.png)

The email notification is using another lambda layer. The Github code can be found at: https://github.com/BCIT-Reseach-Long-Term-ISSP/cloud-2023/blob/main/src/lambda_layers/python/emailnotifier.py.

## CloudWatch Logs
Cloud Watch logs is a good way to debug any issues found in the lamda function. There are log levels which can spot ERRORS and see any logical errors. To access it through the lambda function, click on 'Monitor' section and then click on 'View CloudWatch Logs'.

![Lambda Cloud Watch Access](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/LAMBDA_CLOUD_WATCH.png)

Here is an example of what information is contained in these logs:

![Cloud Watch Logs](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/CLOUD_WATCH_LOGS.png)

## Timestream Database
To ensure that the lambda function is functional correctly and send data to the timestream, we check the 'Amazon TimeStream service'. On left hand side, enter Management Tools, the user can select 'Query Editor'.

![Timestream Query Editor](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/TIMESTREAM_QUERY_EDITOR.png)

The user will be redirected to they query editor page. Choose 'yvr-stage-db' to query and there is only one table. In the query. Use the following query:

```
SELECT *
FROM "yvr-stage-db"."calibrated_device_data"
WHERE time BETWEEN '<YYYY>-<MM>-<DD> <HH>:<MM>:<SS>' AND '<YYYY>-<MM>-<DD> <HH>:<MM>:<SS>'
ORDER BY time desc
```

Below is the screenshot of the query editor in action:

![Timestream Query Editor SQL](https://raw.githubusercontent.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/master/cloud/assets/TIMESTREAM_QUERY_EDITOR_SQL.png)
