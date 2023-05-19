---
layout: default
title: AWS Secret Manager
has_children: false
permalink: /docs/cloud/aws-secret-manager
parent: Cloud
has_toc: false
nav_order: 15
---

## Overview:

Amazon Web Services (AWS) Secrets Manager is integral to our secure, compliant operations. This tool safeguards access to our resources by encrypting and storing sensitive credentials and API keys. We use Secrets Manager for managing confidential data, including authorization keys and database credentials like username, password, database engine, host, port, and dbInstanceIdentifier. 

## Current Usage

<!-- <show diagram > -->

## How to Use

### Store a New Secret

1. Natigate to Secret Manager Panel and click “Store a new Secret”
2. Choose a secret type
    
    Note: 
    
    - if you choose the type as “Credentials for Amazon RDS database”, the secret can only store values for “username” and “passowrd”
        
        ![secret_m_1](cloud/assets/secretmanager/secret_m_1.png)
        
    
    - if you choose Other type of secret, you can customize your own key value pairs
        
        ![secret_m_2](cloud/assets/secretmanager/secret_m_2.png)
        
3. config the secret with it’s name and description, with no tags and no permission policies 

 

### Retrive Secret Values from a Secret

- **From Lambda Functions**
    1. Create policy to allow access to the secret
        
        ```yaml
        {
        	"Version": "2012-10-17",
        	"Statement": [
        		{
        			"Effect": "Allow",
        			"Action": [
        				"secretsmanager:GetSecretValue"
        			],
        			"Resource": "*" #replace it with ARN of the secret 
        		}
        	]
        }
        ```
        
    2. Attach this policy to the role that excutes the lamda funtion 
    3. Define `get_secret` in the lambda function to retrive secret values 
        - sample code
            
            ```yaml
            
            import boto3
            from botocore.exceptions import ClientError
            
            def get_secret():
            
                secret_name = "XXXXXX" # replace it with your own secret name
                region_name = "us-west-2" #replace it with your own secret region
            
                # Create a Secrets Manager client
                session = boto3.session.Session()
                client = session.client(
                    service_name='secretsmanager', 
                    region_name=region_name 
                )
            
                try:
                    get_secret_value_response = client.get_secret_value(
                        SecretId=secret_name
                    )
                except ClientError as e:
                    # For a list of exceptions thrown, see
                    # https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_GetSecretValue.html
                    raise e
            
                # Decrypts secret using the associated KMS key.
                secret = get_secret_value_response['SecretString']
            
                # Your code goes here.
            ```
            
    
    **Note:**
    
    We have created a **layer** in Lambda function, named **secretm**, that is used from retrive secret values from a secret, using the sample code provided previously, to avoid code repitition in every lambda function. 
    

### Modify Secret Values

1. click into the secret you want to retrive the value from
2. scrolling donw to “Secret value” section and click “Retrieve secret value”
    
    ![secret_m_3](cloud/assets/secretmanager/secret_m_3.png)
    
3. click “edit” to edit secret values orr add new entry 
    
    ![secret_m_4](cloud/assets/secretmanager/secret_m_4.png)
    

## Benifits:

- **Enhanced Security**: AWS Secrets Manager ensures that sensitive information such as credentials and API keys are securely encrypted and stored, reducing the risk of unauthorized access or breaches.
- **Improved Compliance**: The service aids in meeting regulatory compliance requirements by providing a secure method to manage and rotate secrets, offering detailed auditing capabilities via AWS CloudTrail.
- **Operational Efficiency**: Secrets Manager simplifies the process of rotating, managing, and retrieving secrets, eliminating the overhead of manual secret management and reducing potential human error.

## Costs:

**PER SECRET PER MONTH**

$0.40 per secret per month. A replica secret is considered a distinct secret and will also be billed at $0.40 per replica per month. For secrets that are stored for less than a month, the price is prorated (based on the number of hours.)

**PER 10,000 API CALLS**

$0.05 per 10,000 API calls.

## References:

**AWS Secrets Manager User Guide**

**[https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)**

**AWS Secrets Manager with Python**

**[https://www.bogotobogo.com/python/python_AWS_Amazon_S3_SecretsManager.php](https://www.bogotobogo.com/python/python_AWS_Amazon_S3_SecretsManager.php)**

**Storing and Retrieving a Secret - AWS Secrets Manager**

**[https://docs.aws.amazon.com/secretsmanager/latest/userguide/manage_create-basic-secret.html](https://docs.aws.amazon.com/secretsmanager/latest/userguide/manage_create-basic-secret.html)**
