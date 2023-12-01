# Lambda_s3_project
Created a Lambda function and a  S3 event trigger to execute the Lambda logic to notify on-call teams when a certain alarming action occurs any application.

1AM role for lambda:
aws iam create-role --role-name LambdaIAMRole --description "Lambda Role" --assume-role-policy-document file://lambda_assume_role_policy.json

Lambda policy:
aws iam create-policy --policy-name LambdaRolePolicy --policy-document file://lambda_execution_policy.json

SNS Topic creation to subscribe to email:
aws sns subscribe --protocol "email" --topic-arn <TOPIC_ARN> --notification-endpoint <EMAIL_ADDRESS> --region us-east-1

Lambda permission for the s3 service to invoke function:
aws lambda add-permission --action lambda:InvokeFunction --principal s3.amazonaws.com --statement-id LabS3Trigger --function-name my-lambda --source-arn arn:aws:s3:::<S3_BUCKET_NAME>

Notification configuration:
aws s3api put-bucket-notification-configuration --bucket <S3_BUCKET_NAME> --notification-configuration file://bucket-trigger-notification.json
