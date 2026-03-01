Task 1: Static Web Hosting in EC2 (Ubuntu + Nginx)

Simple Definition:
Deploy a basic website on an EC2 Ubuntu server using Nginx.

Objective:
Learn EC2 setup, SSH, and web server deployment.

Steps Involved in Launching & Deployment
1. AMI Selection: Choose Ubuntu Server 22.04 LTS as the Machine Image.
2. Instance Type: Select t2.micro (Free Tier eligible).
3. Key Pair: Create and download 'hey.pem' for secure SSH access.
4. Network Security:
   - Add SSH rule (Port 22) for remote terminal access.
   - Add HTTP rule (Port 80) from 0.0.0.0/0 to allow public web traffic.
5. Nginx Installation: Update the repository and install the Nginx web server package.
6. Web Content Deployment:
   - Download the "Fireworks Composer" zip file using wget.
   - Unzip and move files to the default web root directory /var/www/html.
7. Verification: Confirm the site is live by browsing to the Public IP 13.57.197.161.

Proof Of Completion:
* EC2 Screenshot: Showing Instance ID i-09e221afdbb1abb76 and 'Running' state.
* Website Output: Showing the "Fireworks Composer" page rendered at the public IP.
* Command Proof: This Commands.txt file documenting the terminal execution.