Task 14: CloudWatch Alarm (75% CPU → Auto Stop + Email)

Objective
Monitor EC2 CPU usage and automatically stop the instance with email notification when usage exceeds 75%.

Steps
1. Create Alarm

Opened AWS CloudWatch → Alarms → Create Alarm.
Selected EC2 → Per-Instance Metrics → CPUUtilization.
Threshold: Static ≥ 75%.
Period: 5 minutes (default evaluation).
Alarm Name: HITAlarm.

2. Configure Actions

EC2 Action: Stop Instance.
Notification: Selected SNS Topic HITTopic.
Created the alarm.

3. Test Alarm

Connected to EC2 via SSH.
Installed stress tool:
sudo apt update

4. Generated CPU load:

sudo apt install stress-ng -y
sudo stress-ng -c 1 -p 0 --cpu-load 80 --timeout 300s

Verified:

CPU > 75%
Alarm state changed to ALARM
EC2 instance stopped
Email received via SNS

Outcome

Alarm triggers at 75% CPU.
Instance stops automatically.
Email notification sent successfully.