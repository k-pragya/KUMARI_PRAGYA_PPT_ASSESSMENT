Task 2: 
Disk Partitioning (Ubuntu - MBR & Windows - GPT)

Simple Definition
Create and manage disk partitions using MBR and GPT storage structures.

Objective
Understand storage management, filesystem creation, and mounting in both Linux and Windows environments.

Steps Performed
Linux (Ubuntu)
1. Identification : Used `lsblk` to identify the raw 8GB EBS volume (`/dev/nvme1n1`).
2. Partitioning: Utilized `fdisk` to create a new primary MBR partition.
3. Formatting : Formatted the partition using the `mkfs.ext4` command.
4. Mounting : Created a directory `/mnt/myvol` and mounted the partition for use.
5. Testing: Verified data persistence by creating `a.txt` and `b.txt`.

Windows Server
1. Disk Management : Initialized the 15GB Disk 1 as a GPT disk. [cite: 31]
2. Volume Creation : Created a 4.88GB New Simple Volume (D:) using the NTFS filesystem.
3. Verification : Confirmed the volume status as "Healthy (Basic Data Partition)" in the Disk Management console.

Proof Of Completion
* Linux Screenshot : Terminal output showing successful `mkfs.ext4` execution and file creation.
* Windows Screenshot : Disk Management window showing Disk 1 with its allocated partitions.