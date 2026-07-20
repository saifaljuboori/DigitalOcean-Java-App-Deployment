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
    java -jar /root/java-react-example.jar
```

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/

 :: Spring Boot ::                (v3.5.5)

2026-07-20T20:22:30.901Z  INFO 48381 --- [           main] com.coditorium.sandbox.Application       : Starting Application using Java 17.0.19 with PID 48381 (/root/java-react-example.jar started by root in /root)
2026-07-20T20:22:30.914Z  INFO 48381 --- [           main] com.coditorium.sandbox.Application       : No active profile set, falling back to 1 default profile: "default"
2026-07-20T20:22:31.101Z  INFO 48381 --- [           main] .e.DevToolsPropertyDefaultsPostProcessor : For additional web related logging consider setting the 'logging.level.web' property to 'DEBUG'
2026-07-20T20:22:34.557Z  INFO 48381 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 7071 (http)
2026-07-20T20:22:34.607Z  INFO 48381 --- [           main] o.apache.catalina.cor

### Navigate Java App through browser
  1. On droplet, select `Networking` section
  2. Add new inbound rule under `Firewalls` section
  3. Click on `Add inbound rule` button
  4. Select `Custom` in the dropdown type
  5. Select `TCP` in Protocol
  6. Enter java app port `7071`
  7. Click on `Add inbound rule` button
  8. Open browser and type `http://<droplet-public-ipv4-address>:7071`


