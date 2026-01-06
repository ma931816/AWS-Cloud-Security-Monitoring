# AWS-Cloud-Security-Monitoring
# Project Overview:

<img width="737" height="1036" alt="Untitled Diagram drawio (3)" src="https://github.com/user-attachments/assets/fe8ed15e-acae-44ce-82f7-a62f9f07302a" />


This project demonstrates a secure, monitored, and compliant cloud storage system using AWS managed services.
Files uploaded to S3 are encrypted, immutable, and monitored for threats and sensitive data. Security Hub centralizes all findings, and alerts are sent to the security team automatically.

The project focuses on AWS cloud security best practices without using third-party workflow tools.

# AWS Services Used in this Project are:

Amazon S3

AWS IAM

AWS CloudTrail

Amazon GuardDuty

Amazon Macie

AWS Config

AWS Security Hub

Amazon EventBridge

Amazon SNS

Amazon S3 Glacier

# IAM Roles used in this Project:

1. FileUploaderRole

Purpose: Allow users/applications to upload files to S3

Permissions: s3:PutObject, s3:GetObject, s3:ListBucket

2. Service-linked Roles

Used by GuardDuty, Macie, Security Hub, and Config for monitoring and compliance

Allow AWS services to read logs and generate findings

# Step-by-Step Flow of the Enitre Usage Process of the Architecture:

User Uploads File: A user uploads files to S3 using IAM role. The bucket has encryption, object lock, and MFA delete enabled.

Logging: CloudTrail records all API activity and stores logs in a separate S3 bucket.

Log Archival: Old logs are automatically moved to Amazon Glacier to save cost.

Threat Detection: GuardDuty analyzes logs and access patterns to detect suspicious behavior.

Sensitive Data Discovery: Macie scans the S3 bucket for PII and other sensitive information.

Compliance Monitoring: AWS Config evaluates bucket configuration for compliance.

Central Security Dashboard: Security Hub collects findings from GuardDuty, Macie, and Config.

Alerts: EventBridge routes security findings to SNS, which sends email notifications to the security team.

# The Security Features Implemented in this Project are:

Encryption at rest using SSE-KMS

Object immutability using S3 Object Lock

MFA-protected deletion

Least-privilege IAM roles

Continuous monitoring and alerting
