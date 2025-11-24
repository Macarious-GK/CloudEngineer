```bash
aws configure
aws configure --profile myprofile
aws sts get-caller-identity
aws sts assume-role --role-arn arn:aws:iam::123456789012:role/MyExampleRole --role-session-name MyAppSession

aws sts assume-role \
  --role-arn arn:aws:iam::222222222222:role/ReadOnlyRole \
  --role-session-name "LimitedSession" \
  --policy '{"Version":"2012-10-17","Statement":[{"Effect":"Deny","Action":"s3:ListAllMyBuckets","Resource":"*"}]}'


aws s3 ls
aws ec2 describe-instances 
aws iam list-users
aws cloudwatch describe-alarms

```