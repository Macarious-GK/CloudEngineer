# AWS CloudOps 

## Table of Contents
- [IAM](#iam)
- [VPC](#vpc)
- [EC2](#ec2)
- [Elastic Load Balancer (ELB)](#elastic-load-balancer-elb)
- [Auto Scaling Group (ASG)](#auto-scaling-group-asg)
- [S3](#s3)
- [RDS](#rds)
- [Route 53](#route-53)
- [CloudFormation](#cloudformation)
- [CloudWatch](#cloudwatch)
- [Systems Manager](#systems-manager)
- [AWS Config](#aws-config)
- [CloudTrail](#cloudtrail)

## ***`Identity Access Management (IAM)`***
- IAM control **who** can do **what** on **which** resources
- Used to manage secure **authentication** and **authorization** for AWS resources.

### OverView & Concepts
- `Users`: User who interact with AWS Console or Using CLI/API

- `Groups`: Collection of users share same permissions

- `Roles`: identity with specific permissions that can be assumed by trusted entities (users, services, other accounts). 
    - no long-term credentials. Instead, AWS generates temporary security credentials (STS) when a role is assumed.
    - Components: 
        - Trusted Entity: 
        - Permission: permission of the role
        - Session Token Duration
        - Session Policies: 
            - Optional policies provided when assuming a role.
            - To further restrict permissions for that session.
            - Can't give more permissions
    - Use Cases: EC2 instance profiles, cross-account access, Lambda execution.

- `Policies`: JSON document tell which permissions granted for the user/group/role


- `Permissions`: the actual action that an entity can do. Ex: GetEc2

### Policies
- Policy Structure:
    - Version
    - Statement: list of policies elements (list(map)) defines a set of permissions
        - Sid
        - Effect
        - Action
        - Principal
        - Resources
        - Condition

```json
// Policy_1 Identity-Based Customer Managed Polices
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowS3ReadOnly",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ],
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "us-east-1"
        }
      }
    },
    {
        "Sid": "AllowEc2List_Customer_Made_policy",
        "Action": "ec2:DescribeInstances",
        "Effect": "Allow",
        "Resource": "ec2:*"
    }
  ]
}
// Policy_2 Resource Based Policy
{
    "Version": "2012-10-17",
    "Statement": [
    {
      "Sid": "S3_ResourceBased Policy",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111122223333:root"
      },
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ],
    }
  ]
}
// Policy_3:Trust Policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sts:AssumeRole"
            ],
            "Principal": {
                "AWS": "258049740213",
                "Service": [
                    "ec2.amazonaws.com"
                ]
            }
        }
    ]
}

```

<div style="text-align: center;">
<img src="../Images/policytree.jpg" width="900 " height="450" style="border-radius: 15px;"></div>


- `IAM Identity-Based Policies`
    - Types:
        - Managed Policies: Managed by AWS, No Edit
        - Customer Managed Polices: Created by customer, Editable 
        - Inline Policies: once for user, extend specific user permissions
- `Resource-Based Policies`
    - Used When sharing resources across accounts or services.
    - Use condition keys like aws:SourceIp, aws:PrincipalArn
    - Services That Support Resource-Based Policies:
        - ***S3 , Lambda, SNS, SQS, KMS & API Gateway***
    - Policy content:
        - *Principal* **→** Who can access the resource
        - *Action + Resource* **→** What they can do
- `Permissions Boundaries`
    - Restrict what IAM users or roles can do, even if a policy allows more.
    - An identity can only perform actions allowed by both its identity policy AND the permissions boundary
    - Ex: developers can create roles but cannot escalate beyond the boundary

- `Service Control Policies (SCPs)`
    - Organizational control over accounts.
    - ***Set Permission Boundaries, still need IAM to grand permissions***

- `Session Policies` 
    - Limit the existing permissions to specific level
    - only applied during a session that’s created via AWS STS (Security Token Service) — and STS sessions can only be created using a role or certain federated mechanisms.

- `Allow & Deny`

<div style="text-align: center;">
<img src="../Images/allowanddeny.jpg" width="900 " height="300" style="border-radius: 15px;"></div>

- Password Policy: policy for restricting how complex user passwords should be.
- Access Keys: Used for CLI/SDK access
- MFA: 
  - Enable for Root
  - For Users, they enable it on their own.

### IAM-Notes
- Assuming role:
    - we should have role with trust policy (who can use the role), and policy with right permission
    - we than can assume the role to generate temp token to use 
    - the Permission of this token based on permission of the role + Session policy permission
- session policy is a policy we can optionally use when assuming a role to have more restricted permissions than the role give 

### Interview Possible Scenarios
- Cross-Account S3 Access Without IAM User Creation
    - S3 resource-based bucket policy with Principal pointing to the external AWS account
- Temporary Access to S3 or EC2 for Contractors
    - S3 only: Use pre-signed URLs to provide temporary, time-limited access.
    - AWS account user: Use STS AssumeRole if allowed, with session policies to restrict permissions.
- Restricting S3 Access Based on IP Address
    - resource-based policy with Condition
- Cross-Account Lambda Invocation Without Role Creation
    - resource-based policy on Lambda


## VPC
- 
## EC2 
- 
## Elastic Load Balancer (ELB)
- 
## Auto Scaling Group (ASG)
- 
## S3
- 
## RDS
- 
## Route 53
- 
## CloudFormation
- 
## CloudWatch
- 
## System 
- 
## AWS Config
- 
## CloudTrail
