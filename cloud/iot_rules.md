---
layout: default
title: IoT Rules
has_children: false
permalink: /docs/cloud/iot-core/iot-rules
grand_parent: Cloud
parent: IoT-Core
has_toc: false
---
# IoT Rules
AWS IoT Rules is gives devices the ability to interact with AWS services. Rules are analyzed and actions are performed based on the MQTT topic stream specified. These rules allow us to pipeline incoming data from buoy sensors and save them into the timestream database and/or other AWS services.

### Cost

![Rule Pricing May 2022](/cloud/assets/iot_rules/2_iot_rule_pricing.png)
<figcaption align="center"><b>May 2022 Oregon regions Rules engine pricing</b></figcaption>

Rules engine use is metered for each time a rule is triggered, and for the number of actions executed within a rule, with a minimum of one action per rule. The pricing is very generous and should add very little cost to the overall cloud architecture. 


### Current active rules 
![Current Active IoT Rules](/cloud/assets/iot_rules/1_active_iot_rules.png)
<figcaption align="center"><b>Current active rules in the cloud</b></figcaption>

| Rule Name | Description | Term Created |
|-----------|-------------|--------------|
|EMA_C22_kinesis_main_data_v00|Main sensor data entry point that saves incoming data into timestream|Cloud Jan-May 2022|
|EMA_C22_main_data_v00|Main kinesis data entry point that pipelines data into kinesis pipeline|Cloud Jan-May 2022|
|sensor_filltered_timestream|Used by EC2 Generator|CIT Sep-Dec 2021| 
|sensor_fulldata_timestream|Used by EC2 Generator|CIT Sep-Dec 2021| 
|YVR_water_sensor1|Used by EC2 Generator|CIT Sep-Dec 2021| 

# How to create Rules

### Rules Dashboard
Once in the IoT Core AWS Service the rules management dashboard should be located in the sidebar to the left under the "Act" section.

![Rules location in sidebar](/cloud/assets/iot_rules/3_rules_sidebar_location.png)
<figcaption align="center"><b>Rules location in sidebar under Act</b></figcaption>

Once navigated, this section is called the Rules dashboard where you will be able to activate/deactivate, update, delete, or create rules. A rule can either be active or deactivated and this section will also list all rules in either state. 

![Create a Rule button](/cloud/assets/iot_rules/4_create_rule.png)
<figcaption align="center"><b>List of all rules and create a rule option</b></figcaption>

### Rule Creation workflow
Creating a rule is simple and comes in 4 steps which we will go over the basics in this section.

**1. Rule Properties**
This section details the name of the new rule as well as descriptions and tags that you would like to attach. For the Cloud Jan-May 2022 term we decided to use a version naming system to keep all rules organized. 

Naming Outline: **\<Project Name>\_\<Term>\_\<Description>\_\<Version>**

Cloud Jan-May 2022 details:
Project: EMA
Term: Cloud 2022 -> (C22)
Detail: Main Data -> main_data
Version: 0.0 -> v00

This would lead us to use the following name for main data coming from the sensors.
Final Name: **EMA_C22_main_data_v00**

![Rule properties](/cloud/assets/iot_rules/5_1_filled_rule_properties.png)
<figcaption align="center"><b>Rule Properties following naming convention and using tags</b></figcaption>

**2. Configure SQL statement**
The next section involves using the customized SQL-like syntax to perform light message parsing before dispatch. MQTT messages support json in the message body so if you would like to trigger a rule based off the contents of the message or even transform the message this is where it would be applicable. 

AWS has a very detailed IoT SQL reference for rules that display some powerful uses of this section of the rule. [Reference here](https://docs.aws.amazon.com/iot/latest/developerguide/iot-sql-reference.html).

![SQL statement](/cloud/assets/iot_rules/6_configure_sql_statement.png)
<figcaption align="center"><b>SQL statement to parse the message before dispatching to an action</b></figcaption>

For example if the expected message has a json body as shown below.
```json
// JSON
{
    "color": "red",
    "temp": 100,
}
```
And the rule only needs to be triggered if the _"temp"_ is above a certain threshold a sample SQL statement could be the following:

Which outlines that the rule will take all values within the json but only trigger if the "temp" is above 50 and if the topic that it is being published to is from "test/topic"

![SQL statement](/cloud/assets/iot_rules/6_1_test_sql_statement.png)
<figcaption align="center"><b>Custom SQL statement to trigger rule based off temp</b></figcaption>

**3. Attach Rule actions**
Arguable the most important part of the rule are the actions that are available/attached to it. This allows the cloud to pipeline MQTT messages into other AWS services which allow us to operate on the data however we see fit if AWS supports it. 

![Attach rule actions](/cloud/assets/iot_rules/7_rule_actions.png)
<figcaption align="center"><b>Attack Rule actions</b></figcaption>

The main services that are used in the EMA project are lambda functions, kinesis, and timestream but there are a variety of services that we can see if we choose the dropdown action. Remember too that there can be up to **10** actions attached to a single rule which gives it the versatility to transform and pipe data to multiple services at once. 

![Rule actions available](/cloud/assets/iot_rules/7_1_rule_action_services.png)
<figcaption align="center"><b>Some of the available rule actions that can be attached</b></figcaption>

**4. Review and Create**
The fourth stage is a simple review stage which gives a bird's eye overview of the rule that you are about to create and prompts you to create it.  

![Review Rule](/cloud/assets/iot_rules/8_review_new_rule.png)
<figcaption align="center"><b>Some of the available rule actions that can be attached</b></figcaption>