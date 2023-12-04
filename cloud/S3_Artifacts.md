---
layout: default
title: S3 for Artifacts
has_children: false
permalink: /docs/cloud/s3art
parent: Cloud
has_toc: false
nav_order: 15
---

# Overview 

Smart device teams need to upload their code's version dependencies to ensure that they have control over updates, enabling them to manage versioning effectively and mitigate the risk of accidental updates.

## How it works

The version file or folder is uploaded to CodeCommit, and through the pipeline, it is then uploaded to the S3 bucket. This process allows for the future implementation of multiple necessary tests through the pipeline. Once uploaded, S3 version control is enabled, making it easy to identify any files that have been previously replaced.

To locate the files that is uploaded please go to this URL:
https://s3.console.aws.amazon.com/s3/buckets/yvr-artifactory?region=us-west-2&tab=objects

## Script to upload and download file

The script that you can use to upload and download file will be in the S3 bucket name menu_artifactory.sh

Prior to using the script you will first need to get your git credential and your account access key and secret.

How to get Git Credential Steps
1. Go to Users in IAM
2. Click your account
3. Click on Security credentials tab
4. Click generate credentials at HTTPS Git credentials for AWS CodeCommit
5. Save the username and password(download the csv file).

To get your account access key and secret please also get it at IAM console.

After that please use aws configure and add your access key and secret.

Now you can start using the script by ./menu_artifactory.sh
