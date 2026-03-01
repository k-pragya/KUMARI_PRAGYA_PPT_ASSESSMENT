This task implements automated website monitoring using AWS serverless services. The solution leverages AWS Lambda, Amazon SNS, and Amazon CloudWatch to detect downtime and send email alerts. An IAM role (LambdaWebsiteMonitorRole) was created with required permissions for Lambda execution, SNS publishing, and CloudWatch metrics. A Python-based Lambda function (WebsiteMonitor) checks website availability and publishes a custom metric (WebsiteUp) to CloudWatch. The function is scheduled using an EventBridge rule with rate(5 minutes) for continuous monitoring.

An SNS topic (WebsiteDownAlert) was configured with an email subscription for notifications. A CloudWatch Alarm (WebsiteDownAlarm) monitors the custom metric and triggers the SNS topic when the value falls to 0 or below. Testing was performed by modifying the target URL to an invalid address, successfully triggering the alarm and email alert.

Lambda code provided to deploy was:

import boto3
import urllib.request
import os
from datetime import datetime

# Environment Variables
WEBSITE_URL = os.environ.get('WEBSITE_URL', 'https://example.com')
SNS_TOPIC_ARN = os.environ.get('SNS_TOPIC_ARN', 'your-sns-arn-here')

# AWS clients
cloudwatch = boto3.client('cloudwatch')
sns = boto3.client('sns')

def lambda_handler(event, context):
    try:
        # Check website using built-in urllib
        with urllib.request.urlopen(WEBSITE_URL, timeout=10) as response:
            status_code = response.getcode()
            if status_code == 200:
                website_up = 1
                message = f"Website is UP: {WEBSITE_URL}"
            else:
                website_up = 0
                message = f"Website returned status {status_code}: {WEBSITE_URL}"
            
    except Exception as e:
        website_up = 0
        message = f"Website DOWN: {WEBSITE_URL}. Error: {e}"

    # Push custom metric to CloudWatch
    cloudwatch.put_metric_data(
        Namespace='WebsiteMonitor',
        MetricData=[
            {
                'MetricName': 'WebsiteUp',
                'Value': website_up,
                'Unit': 'Count'
            }
        ]
    )

    # Send SNS alert if website is down
    if website_up == 0:
        sns.publish(
            TopicArn=SNS_TOPIC_ARN,
            Subject='Website Down Alert!',
            Message=message
        )

    return {'statusCode': 200, 'body': message}