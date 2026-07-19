# DigitalOcean-Java-App-Deployment

## Description

Create DigitalOcean server and deploy Java React Application to the server. The technologies used into this project are DigitalOcean, Linux, Java, and Gradle.

## Setup DigitalOcean server

### Create Droplet

  1. From Compute section, select Droplets
  2. Click on `Create` button
  3. Choose a datacenter region that is geographically closed to you (Frankfurt in my case)
  4. Choose an OS image (Ubuntu 24.04 (LTS) x64 in my case)
  5. Choose a Droplet Plan (Basic Shared CPU)
  6. Choose CPU Options (Regular SSD)
  7. Select a Plan (1 vCPU - 512 MB RAM - 10 GB SSD - 500 GB Transfer)
  8. Authenticate by SSH Key

     - generate ssh key on Mac:
     ```
     cd ~/.ssh
     ssh-keygen -t rsa -C "DigitalOcean-VM"
     cat id_rsa.pub
     ```
  9. Click on `Add SSH Key` button
  10. Paste SSH key into `SSH Key content` box
  11. Give your SSH Key a name (my-droplet-vm)
  12. Click on `Add SSH Key` button
  13. Review summary of droplet being created and click on `Create Droplet` button

### Configure firewall
We need to restrict access to the server (droplet) by allowing access through SSH only, so we need to add an inbound rule to restrict access to SSH port only.

  1. From Netowrking sectino, choose Firewalls
  2. Click on `Create Firewall` button
  3. In Inbound rules section, click on `Add inbound rule`
  4. Select type of rule `SSH`
  5. In `Sources`, remove `All IPv4` and `All IPv6` that were set by default, and restrict it to only your IP address. You can find your computer's IP adderss from [What Is My IP Address] (https://whatismyipaddress.com)



