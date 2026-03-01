Task 13: Start/Stop EC2 using Lambda + API Gateway

Objective
Automate EC2 start/stop using AWS Lambda integrated with API Gateway.

Steps
1. Create IAM Role

IAM → Roles → Create Role → AWS Service → Lambda.
Attached policies:
AmazonEC2FullAccess
AWSLambdaBasicExecutionRole
Role Name: LambdaEC2Role.

2. Create Lambda Function

Lambda → Create Function (Author from scratch).
Name: EC2ControlFunction
Runtime: Python 3.x
Execution Role: LambdaEC2Role.

3. Add Code
import boto3

def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    action = event.get('action')
    instance_id = 'Your-EC2-Instance-ID'

    if action == 'start':
        ec2.start_instances(InstanceIds=[instance_id])
        return f"Started instance {instance_id}"
    elif action == 'stop':
        ec2.stop_instances(InstanceIds=[instance_id])
        return f"Stopped instance {instance_id}"
    else:
        return "Invalid action."

Clicked Deploy.

4. Test Function

Created test event: {"action": "start"} → Verified instance started.
Tested with {"action": "stop"} → Verified instance stopped.

5. Add API Gateway Trigger

Added API Gateway (HTTP API) trigger.
Security: Open (testing).
Copied endpoint URL.

6. Test via API

Used browser/Postman:
?action=start
?action=stop
Confirmed EC2 state changes.

Outcome

Lambda controls EC2 instance successfully.
API Gateway exposes public endpoint.
EC2 starts/stops via API call.
CloudWatch logs confirm execution.