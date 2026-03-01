Task 3: Attach EBS Volume from Different AZ using Snapshot

Simple Definition
Create a snapshot and attach a volume across different Availability Zones (AZ). 

Objective
To learn EBS snapshots and the process of cross-AZ storage handling for disaster recovery or migration.

Steps Involved 
1. Identify Source : Located the source EBS volume and noted its Availability Zone.
2. Snapshot Generation : Created a snapshot of the live volume to capture data state.
3. Cross-AZ Restoration : Created a new volume from the snapshot in a different Availability Zone (restoring data to a new location).
4. Volume Attachment: Attached the restored volume to an EC2 instance residing in the target AZ.
5. OS Verification: Connected via SSH and used `lsblk` to confirm the volume is recognized and data is accessible.

Proof Of Completion
* Snapshot Screenshot : Showing the snapshot ID and "Completed" status.
* Volume AZ Screenshot : Showing the new volume residing in a different AZ than the original.
* Verification Screenshot : Terminal output of `lsblk` showing the attached device. 