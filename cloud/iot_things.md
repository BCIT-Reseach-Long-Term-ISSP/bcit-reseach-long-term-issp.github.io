---
layout: default
title: IoT Things
has_children: false
permalink: /docs/cloud/iot-core/iot-things
grand_parent: Cloud
parent: IoT-Core
has_toc: false
---
# IoT Things
AWS IoT provides a registry that helps you manage things. A thing is a representation of a specific device or logical entity. It can be a physical device or sensor (Buoy in EMA project with communication hat). It can also be a logical entity like an instance of an application or physical entity (EC2 generator instance).

### Cost
The main cost of registering is not really the act of registering a device but the services it uses as its connected. The 2 main costs are Connectivity pricing as well as Messaging pricing

#### Connectivity
Connectivity provides a secure, authenticated connection between devices and AWS IoT core. It is metered in 1 minute increments and is based on the total time your devices are connected to AWS IoT Core.

For example the current Cloud architecture is located in US West (Oregon). Where we only need to pay a measly \$0.042 per device per year (one connection * $0.08/1,000,000 minutes of connection * 525,600 minutes/year) for 24/7 connectivity. This is extremely efficient and cost effective!

![Connectivity Pricing May 2022](/cloud/assets/iot_things/1_connectivity_pricing.png)
<figcaption align="center"><b>May 2022 Oregon region Connectivity pricing</b></figcaption>

#### Messaging
Messages transport device data to and from AWS IoT Core. Messages are metered by the number of messages transmitted between your devices and AWS IoT Core. Since we are predominantly using MQTT this is the type of messaging service we fall under. Which again, is extremely cost effective and will scale to as many devices as we can support with little cost. 

![Messaging Pricing May 2022](/cloud/assets/iot_things/2_mqtt_http_messaging.png)
<figcaption align="center"><b>May 2022 Oregon region Messaging pricing</b></figcaption>

### Curent active Things
![Current active things](/cloud/assets/iot_things/3_active_things.png)
<figcaption align="center"><b>Current active things in the cloud</b></figcaption>

| Rule Name | Description | Term Created |
|-----------|-------------|--------------|
|YVR_water_sensor1|Registered thing for EC2 generator|CIT Sep-Dec 2021|
|YVR_water_sensor2|Registered thing for EC2 generator|CIT Sep-Dec 2021|
|ema2022-nbiot-1|IoT Communication hat for buoy|Power & Comm Dec Jan-May 2022|
|ema2022-nbiot-2|IoT Communication hat for buoy|Power & Comm Dec Jan-May 2022|
|ema2022_pc_aeden|Aeden pc testing connection|Power & Comm Dec Jan-May 2022|

# How to register an IoT Thing
### Things Dashboard
Once in the IoT Core AWS Service the things management dashboard should be located in the sidebar to the left under the "Manage" section.

![Things location in sidebar](/cloud/assets/iot_things/4_things_sidebar.png)
<figcaption align="center"><b>Things management location in sidebar</b></figcaption>

You will then be navigated to the Things management dashboard. Where you are able to edit, delete, or create things. Only by registering a thing will it be able to communicate with the private AWS IoT Network attached to the EMA AWS project account.

Security is a major concern for AWS IoT and can be read more about [here](https://docs.aws.amazon.com/iot/latest/developerguide/iot-security.html). Each client/device connected must have a credential to interact with AWS IoT. All traffic to and from AWS IoT is sent securely over TLS and a random device without the specific credentials unique to itself is not able to send or receive messages from the network. Security is abstracted for us by AWS. 

![Create things button](/cloud/assets/iot_things/5_create_thing.png)
<figcaption align="center"><b>List of all things and create a thing option</b></figcaption>

### Thing creation workflow
"Creating" a thing is simple, in a sense you are registering or issuing credentials to a device that allows it to authorize and communicate with our specific IoT Network in AWS. Depending on the device there should be an AWS SDK/library maintained by Amazon that provides the interfacing necessary to interact with AWS IoT Core. 

Some AWS IoT SDKs can be found [here](https://docs.aws.amazon.com/iot/latest/developerguide/iot-sdks.html) on their documentation page. 

**1. Create thing/s**
Upon clicking "Create things" you are then prompted to create a single or multiple things. For simplicity sake we are only going to cover creating a single thing but multiple things creation should be similar. 

![Create thing/s](/cloud/assets/iot_things/6_multiple_or_single.png)
<figcaption align="center"><b>Option to create a single or multiple things</b></figcaption>

**2. Specify Thing properties**
This section details the name of the new thing as well as descriptive properties to specify what the thing is reponsible for. The Power and Communication team somewhat overlaps with the cloud team in this section as they are usually the ones to issue the certificate and setup policies for their respective communication devices. 

For the EMA project there should already be a thing type (sensor) and thing group (WaterMonitoring) created for it. Please use the "non-searchable thing attributes" thoughtfully though to correctly version and categorize new things or devices to make future integrations easier in the future.

![Specify thing properties](/cloud/assets/iot_things/7_1_thing_filled_properties.png)
<figcaption align="center"><b>Thing properties with descriptive properties</b></figcaption>

**3. Configure Device Certificate**
Device certificates are very important and should be stored and shared carefully and thoughtfully. Unless you fully understand the different options specified you should almost always just auto-generate a new certificate and let AWS take care of it. AWS IoT Security is again detailed in their [documentation](https://docs.aws.amazon.com/iot/latest/developerguide/iot-security.html) but these certificates are very important and will be talked about again in a later step. 

![Device Certificates](/cloud/assets/iot_things/8_certificate_options.png)
<figcaption align="center"><b>Certificate options</b></figcaption>

**4. Attach policies to certificate**
Power and Communication team again mixes together in this step as they have kindly configured and provided policies for specific communication protocols. The current sensor as of May 2022 that is being used uses nbiot so we will be using that policy in this test example. Policies allow us to grant or deny access to AWS IoT resources on a per device basis and can be very powerful to section off certain resources from different devices. 

An AWS IoT Core policy is a JSON document that contains one or more policy statements. Each statement contains:
- `Effect`, which specifies whether the action is allowed or denied.
- `Action`, which specifies the action the policy is allowing or denying.
- `Resource`, which specifies the resource or resources on which the action is allowed or denied (resources = topic strings)

Further read up on policies can be read in the AWS [documentation](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html).

![Policy attachment](/cloud/assets/iot_things/9_policy_options.png)
<figcaption align="center"><b>Policy attachment to Certificate</b></figcaption>

**5. Create thing and Download certificates**
Once the "Create Thing" button is pressed in step 4 the IoT thing will then be registered in IoT Core and you will be prompted to download some files. 

**IMPORTANT**: THESE KEYS WILL ONLY BE AVAILABLE IN THIS PAGE AND EVERY FILE SHOULD BE DOWNLOADED AND KEPT SAFE.

These certificates and keys are **VERY IMPORTANT** and should be saved and kept safe. These files are necessary to connect or link a physical device or application to the "Thing" you just created in IoT core. If these credentials are lost you will not be able to connect to AWS IoT Core with the device associated with the key you lost. 

Think of these keys as a key to your house or locker, where the house/locker is the device Credential that you just created associated to IoT Core and your house key is are the files you just downloaded.

All SDK libraries maintained by amazon need a combination of key and certificate to authenticate you into your IoT core network. Some AWS IoT device SDKs can be found in their [documentation](https://docs.aws.amazon.com/iot/latest/developerguide/iot-sdks.html). In fact, the EC2 generator that cloud uses to mock data uses the Python AWS IoT device SDK to communicate with IoT Core. 

![Certificate download and files](/cloud/assets/iot_things/10_attached_certificates_keys.png)
<figcaption align="center"><b>Certificate download page with keys and other files</b></figcaption>

