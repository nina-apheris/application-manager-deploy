# 🚀 Application Manager - CloudFormation Launch

This project deploys the Application Manager AMI on AWS using a single-click CloudFormation stack.

## 🔧 Prerequisites

- Your own AWS account
- An existing EC2 Key Pair (for SSH access)
- AMI ID provided by the Application Manager team

## 🚀 Launch Now

Click the link below to deploy:

👉 [Launch in AWS (eu-central-1)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?templateURL=https://application-manager-cf-templates.s3.eu-central-1.amazonaws.com/application-manager.yaml&stackName=apheris-application-manager&param_AmiId=ami-068e657c26a322e1b
)

## 📥 Parameters

- **AmiId** – Provided by the Apheris team
- **KeyName** – Your EC2 key pair name
- **InstanceProfile** – IAM profile with SSM read permissions
- **VpcId** and **SubnetId** – Choose based on your AWS environment
