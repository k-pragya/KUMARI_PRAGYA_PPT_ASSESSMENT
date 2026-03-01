# Task 11: S3 Upload Email Notification (Lambda + SNS)

Simple Definition
Automatically send an email notification when a file is uploaded to an S3 bucket using Lambda and SNS.

Objective
Understand event-driven architecture in AWS using S3, Lambda, and SNS integration.

Steps Involved

1. Create Lambda Function:
   - Navigated to AWS Lambda → Create Function.
   - Selected: Author from scratch.
   - Function Name: HITFunction.
   - Runtime: Python 3.x (latest supported).
   - Created/used IAM Role:
        Role Name: HITRole1
        Attached Policies:
            - AWSLambdaBasicExecutionRole
            - SNS Full Access
   - Created and saved the function.

2. Create S3 Bucket:
   - Navigated to S3 → Create Bucket.
   - Bucket Name: HITBucket (unique name).
   - Enabled versioning (optional).
   - Created the bucket.

3. Create SNS Topic:
   - Navigated to SNS → Create Topic.
   - Type: Standard.
   - Topic Name: HITTopic.
   - Display Name: HITOfficial.
   - Created the topic.

4. Subscribe Email to SNS Topic:
   - Opened HITTopic → Subscriptions → Create Subscription.
   - Protocol: Email.
   - Endpoint: Entered email address.
   - Confirmed subscription from received email.

5. Configure S3 Event Notification:
   - Opened S3 → HITBucket → Properties.
   - Selected Event Notifications → Create Event Notification.
   - Event Name: HITEvent.
   - Event Type: All Object Create Events.
   - Destination: SNS Topic → HITTopic.
   - Saved configuration.

6. Add Lambda Trigger:
   - Opened Lambda → HITFunction → Add Trigger.
   - Selected S3.
   - Bucket: HITBucket.
   - Event Type: All Object Create Events.
   - Saved trigger.

7. Add Lambda Code:
   - Opened Lambda code editor.
   - Pasted Python script to publish message to SNS topic when S3 object is created.
   - Clicked Deploy to save changes.

   Example Code:

   import json
   import boto3

   sns = boto3.client('sns')

   def lambda_handler(event, context):
       message = "File uploaded to S3 bucket."
       sns.publish(
           TopicArn='YOUR_SNS_TOPIC_ARN',
           Message=message,
           Subject='S3 Upload Notification'
       )
       return {
           'statusCode': 200,
           'body': json.dumps('Notification sent successfully!')
       }

8. Testing:
   - Uploaded a file to HITBucket.
   - Verified email notification received from SNS.
   - Checked Lambda → Monitor → CloudWatch Logs for successful execution.

9. Verification:

   - Screenshot of Lambda Function (HITFunction).
   - Screenshot of S3 Event Notification configuration.
   - Screenshot of SNS Topic, Subscription confirmation, and received email.
   - Screenshot of successful Lambda execution logs.

Expected Outcome

- When a file is uploaded to HITBucket, Lambda function is triggered.
- Lambda publishes a message to HITTopic.
- Subscribed email receives notification automatically.