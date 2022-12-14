#  IaC - Sceptre - CloudFormation 
This repository contains Sceptre/CloudFormation code (IaC) to accomplish various tasks.

## Features

- Different mini projects with YAML file to create AWS resources

### CDNwithPrivateS3asOrigin
- Creates CloudFront distribution with S3 as origin
- IAM User that can access to read from and write to S3 bucket and create Cache Invalidation in CDN. It's access key is stored in SSM
- Create 'A' record in Route 53 with HostedZoneId: Z2FDTNDATAQYW2 - This is always the hosted zone ID when you create an alias record that routes traffic to a CloudFront distribution
- Dummy SSM parameters assuming the application reads the latest version from the SSM parameters
- Private S3 bucket that will host the application and a logging bucket that stores the logs of application bucket

### Lambda@Edge
- Create S3 Bucket to store Lambda Function
- IAM User that has access to read and write to Lambda and update Cloud Front Distribution
- Create Lambda@edge with source code stored in previously created S3 bucket

### EC2WithCodeDeployAgent
- Creates EC2 instance with the following features:
    - Security Group that allows specified local network
    - IAM Instance Profile with Code Deploy Role attached
    - Wait Handle and Condition for installation of CloudWatch and CodeDeploy Agent
    - 100GB additional EBS attached and logical volumes created for the same
    - CloudWatch Agent installed and configured
    - CodeDeploy Agent installed via UserData
- Creates IAM Role with the following policies:
    - Allow CloudFormation 
    - Allow sample S3 bucket with read and write access
    - Allow sample S3 bucket 2 with read access
    - Receive and Delete messages from SQS
    - Publish to SNS Topic
    - Get SSM Parameters
    - Read and Write to CloudWatch Logs
    - Read Volumes
