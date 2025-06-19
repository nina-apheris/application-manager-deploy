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

# 🔐 Manual IAM Setup for Application Manager

This CloudFormation template assumes that the IAM role and instance profile already exist. This section guides you through creating them manually with the necessary permissions.

---

## 1. Create an IAM Role for EC2

1. Go to the [IAM Console](https://console.aws.amazon.com/iam).
2. Navigate to **Roles** → **Create role**.
3. **Trusted entity type**: Select **AWS service**.
4. **Use case**: Choose **EC2**.
5. Skip attaching policies for now.
6. Name the role: `application-manager-ec2-role`.
7. Click **Create role**.

---

## 2. Attach Inline Policy for SSM Parameter Read Access

1. Go to the role: `application-manager-ec2-role`.
2. Select the **Permissions** tab → **Add inline policy**.
3. Go to the **JSON** tab.
4. Paste the following policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ssm:GetParameter",
        "ssm:GetParameters"
      ],
      "Resource": "arn:aws:ssm:eu-central-1:049125108544:parameter/application-manager/docker-token"
    }
  ]
}
```

5. Click Next, give the policy a name like ReadDockerTokenSSM, and click Create policy.

## 3. Create an Instance Profile

You can create the instance profile either through the AWS Console or CLI.

### Option A – Using AWS CLI
```bash
aws iam create-instance-profile \
  --instance-profile-name application-manager-instance-profile

aws iam add-role-to-instance-profile \
  --instance-profile-name application-manager-instance-profile \
  --role-name application-manager-ec2-role
```

### Option B – Using AWS Console

1. Go to **IAM** → **Instance Profiles**.

2. Click **Create instance profile**.

3. Enter the name: `application-manager-instance-profile`.

4. Attach the role: `application-manager-ec2-role`.

## 🔒 Security Notes

The EC2 role has minimal permissions (read-only access to one SSM parameter).

All other permissions (e.g., SG) are controlled by CloudFormation.
