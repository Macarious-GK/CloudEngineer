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
- Policy Structure:


- `Permissions`: the actual action that an entity can do. Ex: GetEc2

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
- `Permissions Boundaries`
    - Restrict what IAM users or roles can do, even if a policy allows more.

- `Service Control Policies (SCPs)`
    - Organizational control over accounts.
    - ***Set Permission Boundaries, still need IAM to grand permissions***

- `Session Policies` 
    - Limit the existing permissions to specific level
    - only applied during a session that’s created via AWS STS (Security Token Service) — and STS sessions can only be created using a role or certain federated mechanisms.

- `Allow & Deny`

<div style="text-align: center;">
<img src="../Images/allowanddeny.jpg" width="900 " height="300" style="border-radius: 15px;"></div>


### 


### Notes
- Assuming role:
    - we should have role with trust policy (who can use the role), and policy with right permission
    - we than can assume the role to generate temp token to use 
    - the Permission of this token based on permission of the role + Session policy permission
- session policy is a policy we can optionally use when assuming a role to have more restricted permissions than the role give 

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
