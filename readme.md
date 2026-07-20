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

  1. From Netowrking section, choose Firewalls
  2. Click on `Create Firewall` button
  3. Select type of rule `SSH`
  4. In `Sources`, remove `All IPv4` and `All IPv6` that were set by default, and restrict it to only your IP address. You can find your computer's IP adderss from [What Is My IP Address](https://whatismyipaddress.com)
  5. Click on `Add inbound rule` button
  6. Give a name for your firewall
  7. Apply the firewall you configured to your newly created droplet.

## Connect to DigitalOcean Server

  1. Copy the public IPv4 address of your droplet
  2. Connect via SSH, via your local machine's terminal
  ```
     ssh root@<droplet-public-ipv4-address>
  ```

### Install Java on Droplet
```
    apt update
    apt install openjdk-17-jre-headless
```

### Deploy Java app on Droplet
*on your local machine:*
```
    git clone https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/java-react-example
    cd java-react-example
    gradle build
    cd build/libs/
    scp java-react-example.jar root@<droplet-public-ipv4-address>:/root
```

*on your droplet server:*
```
    root@ubuntu-s-1vcpu-512mb-10gb-fra1:~# java -jar /root/java-react-example.jar
```

