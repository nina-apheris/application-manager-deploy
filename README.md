# 🚀 Application Manager - CloudFormation Launch

This project deploys the Application Manager AMI on AWS using a single-click CloudFormation stack.

## 🔧 Prerequisites

- Your own AWS account
- An existing EC2 Key Pair (for SSH access)
- AMI ID provided by the Application Manager team

## 🚀 Launch Now

Click the link below to deploy:

👉 [Launch in AWS (eu-central-1)](https://console.aws.amazon.com/cloudformation/home#/stacks/create/review?templateURL=https://raw.githubusercontent.com/nina-apheris/application-manager-deploy/main/application-manager.yaml&stackName=application-manager&param_AmiId=ami-0417292ed08db20bc
)

## 📥 Parameters

- **AmiId** – Provided by the Apheris team
- **KeyName** – Your EC2 key pair name
- **InstanceProfile** – IAM profile with SSM read permissions
- **VpcId** and **SubnetId** – Choose based on your AWS environment
