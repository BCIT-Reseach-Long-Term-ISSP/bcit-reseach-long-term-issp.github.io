---
layout: default
title: DynamoDB
has_children: false
permalink: /docs/cloud/dynamodb
parent: Cloud
has_toc: false
nav_order: 13
---

# DynamoDB Documentation

DynamoDB is a fully managed NoSQL database service provided by AWS. It offers seamless scalability and low-latency performance, making it suitable for a wide range of applications.

## Basics of DynamoDB

DynamoDB operates on the principles of:

- **Tables**: The basic unit of storage.
- **Items**: Individual records in a table.
- **Attributes**: Data elements within an item.
- **Primary Key**: A unique identifier for each item in the table.

## Getting Started

To create a new table, you can use the AWS Management Console or the AWS CLI:

```bash
aws dynamodb create-table --table-name YourTableName --attribute-definitions AttributeName=YourKey,AttributeType=S --key-schema AttributeName=YourKey,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5

```


# Device Table

The Device Table in DynamoDB is designed to store information about devices in a scalable and flexible manner. It serves as a central repository for managing device-related data.

## Table Structure

The Device Table consists of the following components:

- **Primary Key**: The primary key uniquely identifies each item (device) in the table. It comprises a single attribute:
  - **Partition Key**: Used to distribute data across multiple partitions.

- **Attributes**: Data elements representing various properties of a device. These can include:
  - id
  - Name
  - Description
  - Device Status
  - Location
  - Sensors

## Example Operations

### 1. Creating a Device Item

To add a new device to the table, you can use the `add` operation. 

```json request body
{
    "operation": "add",
    "id": 123,
    "Name": "Device Expo Line",
    "Description": "Device Description",
    "Device Status": true,
    "location": {
        "latitude": 40.7128,
        "longitude": -74.0060
    },
    "sensors": [
        {
            "id": 2,
            "measurement": "ph",
            "power": false,
            "min": 1,
            "max": 7,
            "units": "pH units",
            "alerts": false,
            "calibration": {
                "dateLastCalibrated": "2023-11-04",
                "physicalValue": [1.3, 1.4],
                "digitalValue": [4, 5.9]
            }
        }
        // Add additional sensors as needed
    ]
}
```
### View DynamoDB Table in AWS Console

**1. Open AWS Management Console:**
   - [Go to AWS Management Console](https://aws.amazon.com/console/).
   - Sign in with your AWS account credentials.

**2. Navigate to DynamoDB:**
   - Search for "DynamoDB" in the services search bar.
   - Click on "DynamoDB" in the search results.

**3. View Tables:**
   - In DynamoDB console's left navigation pane, click on "Tables."
![image](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/assets/70176847/b5fd6b91-7b98-48c9-935c-92410e779ffb)

**4. Select Your Table:**
   - Look for the table named "DeviceTable" (or your table's name. In the photo above, it is bby23-device).
   - Click on the table name to open its details page.
![image](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/assets/70176847/c17cac9d-76fd-46dc-938d-b57c2371bcd5)

**5. View Items:**
   - On the table details page, go to the "Explore Table Items" tab.
   - ![image](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/assets/70176847/a3e9b3da-54a1-419b-8de9-93c189fa6fa5)

   - You'll see a list of items (devices) in the table.
   - ![image](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/assets/70176847/54120ec2-9c6e-4028-a2b6-5cf0b592a0d7)


**6. Explore Other Tabs:**
   - Check other tabs for more details, e.g., "Overview" for metrics, "Indexes" for indexes.

You've successfully navigated to the DynamoDB console and can now view your "DeviceTable."
