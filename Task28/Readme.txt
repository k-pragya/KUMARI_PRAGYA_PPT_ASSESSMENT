TASK 4 — Azure Hybrid Architecture Simulation

Objective:
Simulate a secure on-prem to Azure cloud architecture using Azure Bastion, Private Subnet, Route Tables, and controlled network access.

Environment Setup:

A new Resource Group was created in the selected Azure region.
A Virtual Network was created with address space 10.1.0.0/16 to logically isolate the environment.

Three subnets were configured inside the Virtual Network:

Public Subnet
Address range: 10.1.1.0/24
Used for internet-facing resources if required.

Private Subnet
Address range: 10.1.2.0/24
Used to host the private virtual machine without public exposure.

AzureBastionSubnet
Address range: 10.1.3.0/26
Mandatory subnet required for Azure Bastion deployment.

Network Security Configuration:

Two Network Security Groups (NSGs) were created.

Public NSG
Configured to allow SSH (Port 22) only from “My IP address”.
Ensures restricted administrative access.

Private NSG
Configured to allow SSH (Port 22) only from the Virtual Network.
Prevents direct internet access to private resources.

Each NSG was associated with its respective subnet to enforce subnet-level security controls.

Private Virtual Machine Deployment:

A Linux virtual machine was deployed inside the Private Subnet.
Authentication method used: SSH public key.
Public inbound ports: None.
Public IP address: Not assigned.

The VM received a private IP address
This confirms it is isolated inside the private subnet and not accessible directly from the internet.

Azure Bastion Deployment:

Azure Bastion was deployed in the same Virtual Network inside AzureBastionSubnet.
A Public IP address was created for Bastion.
Bastion enables secure browser-based SSH connectivity without exposing the VM to the internet.

Secure Connectivity Validation:

Connection was successfully established to the Private VM using Azure Bastion.
The hostname command confirmed login into private-vm4.
The ip a command showed the private IP address 10.1.2.4.
The curl internet test returned no response, confirming restricted outbound internet access.

Architecture Flow:

User Laptop
→ Azure Bastion (Public IP)
→ AzureBastionSubnet
→ Private Subnet 
→ Private Virtual Machine 

Security Characteristics:

The private VM has no public IP address.
SSH access is not exposed to the internet.
Access is allowed only through Azure Bastion.
Subnet segmentation provides network isolation.
NSGs enforce controlled inbound access.
Outbound internet access is restricted.

Conclusion:

This architecture successfully simulates a secure hybrid cloud design where private workloads are isolated inside a private subnet and accessed securely using Azure Bastion. The environment demonstrates subnet segmentation, network security enforcement, controlled administrative access, and enterprise-level secure cloud design principles.