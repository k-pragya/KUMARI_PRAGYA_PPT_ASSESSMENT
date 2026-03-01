# Task 7: Create EFS and Connect to Multiple Ubuntu Instances

Simple Definition
Mount shared storage across multiple EC2 instances.

Objective
Learn scalable file systems in AWS.

Steps Involved
1.EFS Provisioning: Created a Regional EFS named MyEFS with backup off and lifecycle management set to transition to IA after 30 days and Archive after 90 days.
2.Network Configuration: Established mount targets in all required Availability Zones and configured security groups to permit NFS traffic on port 2049.
3.Instance Setup: Launched two Ubuntu instances within the same VPC and assigned security groups allowing NFS traffic.
4.Client Installation: Connected via SSH and installed the nfs-common package to enable NFS mounting[cite: 49].
5.Shared Mounting: Created a mount directory /MyMount and successfully mounted the EFS using the NFSv4.1 protocol.
6.Data Persistence Testing: Created a test file a.txt on the first instance and confirmed its visibility on the second instance to verify shared access.

## Proof of Completion
*EFS Dashboard Screenshot: Showing the file system configuration and lifecycle settings.
*Terminal Command Screenshot: Showing the successful mount commands and file creation.
*File Visibility Screenshot: Showing the test file visible on multiple instances simultaneously.