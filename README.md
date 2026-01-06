# AWS-Cloud-Security-Monitoring
# Project Overview:

This project demonstrates a secure, monitored, and compliant cloud storage system using AWS managed services.
Files uploaded to S3 are encrypted, immutable, and monitored for threats and sensitive data. Security Hub centralizes all findings, and alerts are sent to the security team automatically.

The project focuses on AWS cloud security best practices without using third-party workflow tools.

<img width="737" height="1036" alt="Untitled Diagram drawio (3)" src="https://github.com/user-attachments/assets/fe8ed15e-acae-44ce-82f7-a62f9f07302a" />


# AWS Services Used in this Project are:

# Amazon S3

Two S3 Buckets are Created 

- secure-file-sharing-immutable-smah for the Storing of the Files
- secure-file-logs-smah for storing the logs ( can be used to visualize the data on AWS Quicksight or can be used by AWS Athena to perform analytics on it )

<img width="1874" height="864" alt="S3 Buckets Created" src="https://github.com/user-attachments/assets/fccdc35d-856a-4f6a-ab0f-f6032ff16c7b" />

# AWS IAM

- By using IAM Roles, the File Uploader Role was Created that is attached with Custom S3 Policy having premissions for successfully putting object in the bucket, to get the object and to list the buckets
<img width="1877" height="899" alt="File Uploader Role Created with s3 custom policy attached" src="https://github.com/user-attachments/assets/f3ddb789-fa78-45f2-a35b-2814ba9ddf6a" />

- By using IAM Roles, the Security Monitoring Role was Created that have the Premissions policy attached having full access to Amazon GuardDuty, Amazon Macie, Amazon S3 Read Only Access and AWS Security Hub Full Access
<img width="1876" height="902" alt="Security Monitoring Role with custom policy premissions attached" src="https://github.com/user-attachments/assets/1e11fb96-6b82-4b5b-addb-32b6e4457297" />

# AWS CloudTrail

- Cloud Trail was Created for Logging all the activity
<img width="1876" height="901" alt="Cloud Trail Multi Region Enabled For Audit Trail stored in existing S3 Bucket for logs" src="https://github.com/user-attachments/assets/3b92b9c2-133d-4360-9d59-d6a5f6c4752e" />

# Amazon GuardDuty

- Amazon GuardDuty was Enabled to Monitor the S3, API Calls and the Suspicious Behavior
<img width="1877" height="903" alt="Guard Duty Enabled That monitors s3,api calls, and suspicious behavior" src="https://github.com/user-attachments/assets/b5220f67-2442-4c8d-849c-6b945f0833a5" />

# Amazon Macie

- Amazon Macie Created to Scans S3 Bucket for Any Sensitive Information
<img width="1877" height="949" alt="Amazon Macie with Job Created for s3" src="https://github.com/user-attachments/assets/3b2812b6-1ed8-483a-a351-2a6e8ef18abf" />

# AWS Config

- AWS Config Rule 1 was Created that is Assuring the S3 Bucket Server Side Encryption
<img width="1876" height="912" alt="AWS Config Rule 1" src="https://github.com/user-attachments/assets/c7e2b3bb-006b-4231-bb66-71e073e1bb9b" />

- AWS Config Rule 2 was Created that is Assuring the Prohibition of Public Read to the S3 Bucket 
<img width="1876" height="945" alt="AWS Config Rule 2" src="https://github.com/user-attachments/assets/c7604148-cc81-4da6-850e-82fb9d5e5eef" />

- AWS Config Rule 3 was Created that is Assuring Prohibition of Public Write to the S3 Bucket
<img width="1877" height="955" alt="AWS Config Rule 3" src="https://github.com/user-attachments/assets/9a9cf905-9123-4837-aed8-f90c6555dac5" />

# AWS Security Hub

- AWS Security Hub was Enabled that will provide Central View of Security Condition of your Resources and Available Threats to the Resources
<img width="1876" height="901" alt="Security Hub Enabled" src="https://github.com/user-attachments/assets/fe025ca8-cdf5-4f7b-b496-8bb962382043" />

# Amazon EventBridge

- In the Amazon EventBridge, the Rule was Created to Send Notification of Security Events coming from GuardDuty to the Users through Amazon SNS
<img width="1875" height="951" alt="EventBridge Rule to send notification from guard duty to sns email" src="https://github.com/user-attachments/assets/921e8b95-3a40-4e5d-8b82-1ab60f3dbcb4" />

- In the Amazon EventBridge, the Rule was Created to Send Notification of Security Events coming from GuardDuty to the Users through Amazon SNS
<img width="1876" height="950" alt="Eventbridge rule to send notifications from Amazon Macie to SNS " src="https://github.com/user-attachments/assets/c0110062-28f5-4029-bace-231222845cbb" />

# Amazon SNS

- SNS Alert was Created to Send the Security Events Info coming from EventBridge to Specific Users subscribed to the Topic 
<img width="1876" height="954" alt="SNS Security Alerts Topic" src="https://github.com/user-attachments/assets/3f46dabd-a19e-4dd5-9158-a8f9cb776bb0" />

# Amazon S3 Glacier

- The S3 Lifecycle Policy Configured to move the Logs from S3 to S3 Glacier Flexible Reterive to Achieve Cost-Efficiency
<img width="1877" height="948" alt="Configure Lifecycle Policy to move to Glacier Flexible Reterive after 30 days" src="https://github.com/user-attachments/assets/bd28d960-8a0c-4235-8b68-02045a3806ee" />

# IAM Roles used in this Project:

# FileUploaderRole

<img width="1877" height="899" alt="File Uploader Role Created with s3 custom policy attached" src="https://github.com/user-attachments/assets/d540e819-5ea9-41fd-a57f-b17a372b393f" />

- Purpose: Allow users/applications to upload files to S3

- Permissions: s3:PutObject, s3:GetObject, s3:ListBucket

# Service-linked Roles

<img width="1876" height="902" alt="Security Monitoring Role with custom policy premissions attached" src="https://github.com/user-attachments/assets/aa5020e3-86f9-4a42-9718-d6f21ee98a15" />

- Used by GuardDuty, Macie, Security Hub, and Config for monitoring and compliance

- Allow AWS services to read logs and generate findings

# Step-by-Step Flow of the Enitre Usage Process of the Architecture:

- User Uploads File: A user uploads files to S3 using IAM role. The bucket has encryption, object lock, and MFA delete enabled.

- Logging: CloudTrail records all API activity and stores logs in a separate S3 bucket.

- Log Archival: Old logs are automatically moved to Amazon Glacier to save cost.

- Threat Detection: GuardDuty analyzes logs and access patterns to detect suspicious behavior.

- Sensitive Data Discovery: Macie scans the S3 bucket for PII and other sensitive information.

- Compliance Monitoring: AWS Config evaluates bucket configuration for compliance.

- Central Security Dashboard: Security Hub collects findings from GuardDuty, Macie, and Config.

- Alerts: EventBridge routes security findings to SNS, which sends email notifications to the security team.

# The Security Features Implemented in this Project are:

- Encryption at rest using SSE-KMS

- Object immutability using S3 Object Lock

- MFA-protected deletion

- Least-privilege IAM roles

- Continuous monitoring and alerting

# Results

- Security Hub Initial Scan 

<img width="1877" height="904" alt="Security Hub Initial Scan Condition" src="https://github.com/user-attachments/assets/d1f307d4-d90c-4544-b43e-c88da8a00d6b" />

- Amazon Macie After Detecting Issue

<img width="1878" height="575" alt="After Detecting issue then Amazon Macie" src="https://github.com/user-attachments/assets/30e3bfdc-a77e-49b5-85d9-9ceff175367b" />

- SNS Email from GuardDuty ( by Using Sampling Data Generated by GuardDuty )

<img width="1875" height="954" alt="SNS Notifications From Guarduty and Macie upon Detection of Sample Populated Data by guard duty" src="https://github.com/user-attachments/assets/d38f7fdf-9e44-439e-911e-df3dc8c28cc8" />


