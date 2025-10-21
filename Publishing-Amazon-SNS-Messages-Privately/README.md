README: Secure and private patient report delivery with AWS

Introduction

This project demonstrates a secure, serverless architecture for a healthcare application to privately publish patient reports and notify patients via mobile push notifications. The solution leverages AWS services to handle sensitive data in a HIPAA-eligible manner. An EC2 instance within an Amazon VPC privately publishes messages to an Amazon SNS topic, ensuring data never travels over the public internet. This architecture meets critical healthcare industry requirements for security and privacy.

Architecture overview

The solution uses the following AWS services:

Amazon Virtual Private Cloud (VPC): A logically isolated network that provides control over network settings, including IP address range, subnets, and route tables.

Amazon EC2: A virtual server to host the application logic that processes and publishes the reports.

Amazon SNS: A pub/sub messaging service that sends push notifications to the patient's mobile app.

AWS PrivateLink (via VPC Endpoints): A service that establishes a private connection between the VPC and Amazon SNS, so traffic stays within the AWS network.

AWS CloudFormation: An infrastructure-as-code service for provisioning all necessary resources in a repeatable manner.
