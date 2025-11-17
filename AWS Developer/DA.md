# AWS Certified Developer - Associate

## Domains:
Development with AWS Services (32% of scored content)
Security (26% of scored content)
Deployment (24% of scored content)
Troubleshooting and Optimization (18% of scored content)


## Development with AWS Services

### `Task 1: Develop code for applications hosted on AWS.`
- Well-arch framework
- Cloudformation
- Serverless 
- Design Patterns ( Event driven , Fanout, Orchestration, Sync & Async )
- Failure detection & automatic remediation (exponential backoff with jitter)
- Step Function & EventBridge 
- Stateless & Stateful Design
- AWS SDK
- API Gateway (UsagePlans, Api Keys)
- Write Unit test 
- Cognito Sync
- DynamoDb Hot Partition (Sharding ) 

### `Task 2: Develop code for AWS Lambda.`
- Concurrency execution
- Number of shards
- source Mapping 
- Errors (Invocation, Function)
- Invoke sync or async
- Permissions 
- lambda access private resources (elastic network interface + sec groups)
- Cold/Warm start -> using eventbridge rule to schedule invocation every minute .
- Memory,  Initialization, Function tuning
- velocity template languation in apigateway service integration

### `Task 3: Use data stores in application development.`

- Data Strategy
- Dynamodb (Global secondary Index)
- WCU & RCU
- efs lyfecycle 
- caching 

https://aws.amazon.com/elasticbeanstalk/faqs/?da=sec&sec=prep#topic-0
https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#topic-0
https://aws.amazon.com/api-gateway/faqs/?da=sec&sec=prep
https://aws.amazon.com/iam/faqs/?da=sec&sec=prep
https://aws.amazon.com/kms/faqs/?da=sec&sec=prep


## Security

### `Implement authentication and/or authorization for applications and AWS services.`
- AWS Account (IAM, Organization)
- Policies
- If we want ecs (has 4 tasks) to perform actions: Choses Iam roles not service linked roles 
- what is service link roles -> Linked to service  
- AWS Directory Service
- Federation
    - Cross account role
    - SAML/ OAuth
    - Web Identity Federation
- Diff between (STS Get Token, Get Federation Token, Get Session Token)
- lambda Authorizer types 

### `Implement encryption by using AWS services.`
- Encrypt Data At Rest
- Encrypt Data At Transit
- Encryption & Tokenization

- Encryption EBS, RDS 

- RDS:
    - Can i encrypt db after creation
    - Can you turn off encryption
    - Can you create encrypted snapshot from unencrypted DB
    - what kms key you use for encrypt readreplicas in same region
    - how to copy encrypted snapshot from region to another 

- Cloud HSM
- Local integral KMS FOR encryption data (Envelop)

- Serverless app use lambdas to read data from rds, These functoins need to share the same Connection Strings  (security Encryption) : sysmanger parm store

### `Manage sensitive data in application code.`

- For Containers : Secure Cred in Env Variables by referce secret Manger/Parameter Store
- In Patch we use it in task Defientaion

https://docs.aws.amazon.com/lambda/latest/dg/lambda-security.html
https://docs.aws.amazon.com/apigateway/latest/developerguide/security.html
https://docs.aws.amazon.com/ebs/latest/userguide/ebs-encryption.html
https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html
https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html



## Deployment
### `Task 1: Prepare application artifacts to be deployed to AWS.`
- Store: AWS CodeAritfact/ S3
- Deploy & Build: AWS CloudFormation
- Sam Commands !!! (transform section)

- File Organization: 
    - CodeCommit
- System manager:
    - Application Manager
    - AppConfig
    - Store parms
dependency: lambda sam cdk
how to prepare app aritfacts

### `Task 2: Test applications in development environments. `
- Deployment Strategies
- bluegreen, inplace , rolling all at onece
- aws sam
- step fuction local Mock api testing
- versioning/alias lambda functions
- alias arn of lambda 

### `Task 3: Automate deployment testing.`
- Config as code:
    - OpsWork
    - elastic beanstalk
- infrasture as code 
    - CloudFormation
liniar deployment 
canary deployment
codepipeline

### `Task 4: Deploy code by using AWS CI/CD services`

operational exclance 
codedeploy 
maping template and stage variable

https://docs.aws.amazon.com/codedeploy/latest/userguide/deployments-rollback-and-redeploy.html
https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-steps.html


## Troubleshooting and Optimization

### `Task 1: Assist in a root cause analysis.`
- CloudWatch, CloudTrail, Xray, OpenSearch

- Root Cause:
    - X-ray: Behavioral data
        - Filter, Permission, trace Request, UserData Script
    - CloudWatch: Metrics
    - CloudTrail: Logs

- TroubleShoot Deploy failure 
    - CodeDeploy
    - Lambda 

- Important metric to troubleshoot (responsive of lambda)

- Visualize data
    - Dashboard
    - Namespace
- Cloudwatch Embedded Metric format 

- Log Analytics: Athena, OpenSearch, Kinesis


### `Task 2: Instrument code for observability.`

- CloudWatch Alarms 
- Quota Limits



### `Task 3: Optimize applications by using AWS services and features.`


- Amazon CodeGuru, and it also provides different visualizations of profiling data to help identify what code is running, how much time is consumed, and performance improvements.

- determine minimum memory and compute power: AWS Lambda Power Tuning tool to automate this process and graph those results.

- AWS Compute Optimizer
- DynamoDB Streams,

- What if your application uses S3 behind a CloudFront distribution and has two new requirements to only allow its paying customers access with low latency? Which AWS services could you use for authentication and authorization? Lambda@Edge and Amazon Cognito can help to authenticate and authorize your paying customers' access. 

https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-publish.html
https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-deployments.html
https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-deploying.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-specification-template-anatomy.html
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html
https://docs.aws.amazon.com/opsworks/latest/userguide/welcome.html
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html
https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html




# Notes

stepfuctions attributes
store sessions state info 