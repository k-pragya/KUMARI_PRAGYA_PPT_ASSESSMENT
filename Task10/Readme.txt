# Task 10: VPC 3-Tier Architecture

Simple Definition
Design a secure 3-tier architecture using public and private subnets within a VPC.

Objective
Understand AWS networking concepts including VPC, Subnets, Internet Gateway (IGW), NAT Gateway, Route Tables, NACL, and SSH tunneling.

Steps Involved

1. VPC Creation:
   - Navigated to VPC → Create VPC.
   - Name: UVACA
   - IPv4 CIDR block: 10.0.0.0/24
   - Created and saved the VPC.

2. Internet Gateway Creation:
   - Navigated to VPC → Internet Gateways → Create Internet Gateway.
   - Name: IG1
   - Attached IG1 to VPC: UVACA.

3. Subnet Creation:

   A) Presentation Layer (Public Subnet):
      - Name: PresentationLayer1
      - VPC: UVACA
      - CIDR: 10.0.0.0/27
      - Used for public-facing resources.

   B) Business Layer (Private Subnet):
      - Name: BusinessLayer2
      - VPC: UVACA
      - CIDR: 10.0.0.32/27
      - Used for application/business logic servers.

   C) Database Layer (Private Subnet):
      - Name: DatabaseLayer3
      - VPC: UVACA
      - CIDR: 10.0.0.64/26
      - Used for backend database servers.

4. Route Table Configuration:

   A) Public Route Table:
      - Name: RT1-Public
      - VPC: UVACA
      - Added Route:
          Destination: 0.0.0.0/0
          Target: IG1
      - Associated with PresentationLayer1 subnet.

   B) Private Route Table:
      - Name: MyRouteTable2-Private
      - VPC: UVACA
      - Initially created (NAT added later).
      - Associated with BusinessLayer2 and DatabaseLayer3 subnets.

5. Launch EC2 Instances:

   A) Public Instance (Presentation Layer):
      - Name: MyInst-1-Public
      - AMI: Ubuntu
      - VPC: UVACA
      - Subnet: PresentationLayer1
      - Auto-assign Public IP: Enabled
      - Connected via SSH using key pair.
      - Verified Internet access:
            sudo apt update
            ping google.com

   B) Private Instance (Business Layer):
      - Name: MyInst-1-Private
      - VPC: UVACA
      - Subnet: BusinessLayer2
      - Auto-assign Public IP: Disabled
      - Accessed via SSH tunneling:
            ssh -i "mikey.pem" ubuntu@<Public-IP>
            ssh ubuntu@<Private-IP>

6. NAT Gateway Creation:
   - Navigated to VPC → NAT Gateways → Create NAT Gateway.
   - Name: MyNATGateway
   - Subnet: PresentationLayer1 (Public Subnet)
   - Allocated Elastic IP automatically.
   - Created NAT Gateway.

7. Configure Private Route Table:
   - Edited MyRouteTable2-Private.
   - Added Route:
        Destination: 0.0.0.0/0
        Target: MyNATGateway
   - Saved configuration.

8. Verification:

   - Public EC2 instance accessed Internet directly via Internet Gateway.
   - Private EC2 instance accessed Internet through NAT Gateway.
   - SSH tunneling successfully established from Public to Private instance.
   - Connectivity between instances verified.

Architecture Diagram (Logical View)

                Internet
                    |
                Internet Gateway (IG1)
                    |
           -------------------------
           |                       |
   PresentationLayer1        NAT Gateway
     (Public Subnet)               |
           |                       |
      Public EC2 Instance     Private Route Table
                                   |
                         -------------------------
                         |                       |
                  BusinessLayer2         DatabaseLayer3
                  (Private Subnet)       (Private Subnet)
                         |
                 Private EC2 Instance

Proof of Completion

1) Screenshot of VPC and all three subnets.
2) Screenshot of Route Tables showing IGW and NAT Gateway routes.
3) Screenshot of EC2 instances and successful connectivity tests (ping, SSH, internet access).