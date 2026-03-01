Task 4: ASG and ELB in EC2

Simple Definition
Configure an Auto Scaling Group with a Load Balancer for high availability and automatic scaling

Objective
Understand high availability and scaling concepts by practicing Launch Templates, ASG, and ELB setup.



Steps Involved 

1. Security Setup: Created 'allowall' security group to facilitate seamless traffic between the LB and instances.
2. Base Image Creation: Launched an Ubuntu instance (EcomImage) and deployed the static website.
3. Launch Template: Configured 'ECOM_template' to define the configuration for new instances automatically launched by the ASG.
4. Target Group (TG1): Set up the target group with strict health check thresholds (Healthy/Unhealthy: 2) to ensure traffic only hits functioning instances.
5. Load Balancer (LB1): Deployed an internet-facing Application Load Balancer to distribute incoming traffic across the fleet.
6. Auto Scaling Group (ASG1): Implemented a scaling policy targeting 50% CPU utilization, maintaining a desired capacity of 2 instances and a maximum of 5.
7. Verification: Confirmed that the target group instances are 'InService' and accessed the website via the Load Balancer DNS URL.

 Proof Of Completion
*LB/ASG Screenshot: Showing the Load Balancer and Auto Scaling Group in an active state.
*Target Group Screenshot: Showing registered instances as "Healthy".
*Website Output: Showing the hosted content accessed via the Load Balancer URL.