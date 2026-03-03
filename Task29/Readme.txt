TASK 5 — Serverless + Event-Driven Architecture (AWS + Azure)

Objective: Implement event-driven serverless pipelines using storage triggers, serverless compute, managed NoSQL databases, and monitoring/logs.

AWS Pipeline: S3 → Lambda → DynamoDB → CloudWatch

Architecture Flow:
S3 Bucket → Lambda Function → DynamoDB → CloudWatch Logs

Steps:

1. Create S3 Bucket:
Name: event-driven-bucket-demo
Region: your choice
Purpose: Upload triggers Lambda

2. Create DynamoDB Table:
Table Name: S3EventsTable
Partition Key: id (String)
Capacity: On-demand

3. Create IAM Role for Lambda:

Trusted Entity: AWS Service → Lambda

Policies:

     AmazonS3ReadOnlyAccess
     AmazonDynamoDBFullAccess
     CloudWatchLogsFullAccess

Role Name: LambdaS3DynamoRole

4. Create Lambda Function:

Name: S3EventProcessor
Runtime: Python 3.10
Execution Role: LambdaS3DynamoRole

5. Lambda Code (Store file info in DynamoDB):

import json
import boto3
import uuid

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('S3EventsTable')

def lambda_handler(event, context):
    for record in event['Records']:
        file_name = record['s3']['object']['key']
        table.put_item(
            Item={
                'id': str(uuid.uuid4()),
                'filename': file_name
            }
        )
    return {
        'statusCode': 200,
        'body': json.dumps('Data stored successfully')
    }

6. Configure S3 Trigger:

Lambda → Configuration → Triggers → Add trigger → S3
Bucket: event-driven-bucket-demo
Event Type: All object create events

7. Enable & Verify CloudWatch Logs:

CloudWatch → Log Groups → /aws/lambda/S3EventProcessor
Upload a file to S3 → Check logs for execution

Azure Pipeline: Blob Storage → Azure Function → Cosmos DB

Create Storage Account:

Azure Portal → Storage Accounts → Name & Region

2. Create Azure Function:

Function App → Add Function → Trigger: Blob
Runtime: Python/Node.js

3. Create Cosmos DB:

SQL API → Database + Container

4. Connect Function to Cosmos DB:

Use Cosmos DB output binding

5. Test Event:
Upload file to Blob Storage → Function triggers
Verify logs and database entries