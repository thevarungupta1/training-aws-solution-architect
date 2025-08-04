# Lab 05: Launch EC2 Linux Instance with User Data Script to Install Apache HTTPD

## Objective

Launch an EC2 Linux instance using the AWS Management Console, configure it with a user data script to install the Apache HTTPD server, and access the web server using the instance's public IP.

---

## Prerequisites

- AWS account with permissions to create EC2 instances and security groups
- Basic familiarity with AWS Console

---

## Steps

### 1. Log in to AWS Management Console

1. Open [AWS Console](https://console.aws.amazon.com/).
2. Navigate to **EC2** service.

---

### 2. Launch a New EC2 Instance

1. Click **Launch Instance**.
2. Enter a name (e.g., `Lab05-EC2-HTTPD`).

#### a. Choose Amazon Machine Image (AMI)

- Select **Amazon Linux 2 AMI (HVM), SSD Volume Type**.

#### b. Choose Instance Type

- Select **t2.micro** (Free Tier eligible).

#### c. Configure Key Pair

- Choose an existing key pair or create a new one.
- Download and save the private key file (`.pem`).

#### d. Network Settings

- Select default VPC and subnet.
- Under **Firewall (security groups)**, click **Edit**.

##### Add Inbound Rule:

- Type: **HTTP**
- Protocol: **TCP**
- Port Range: **80**
- Source: **Anywhere (0.0.0.0/0)**
- (Optional) Add **SSH** rule for remote access.

---

### 3. Add User Data Script

1. Expand **Advanced details**.
2. In **User data**, paste the following script:

```bash
#!/bin/bash
# Use this for your user data (script from top tom bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

---

### 4. Launch the Instance

1. Click **Launch Instance**.
2. Wait for the instance state to become **running**.

---

### 5. Access the Apache HTTPD Server

1. In the EC2 dashboard, select your instance.
2. Copy the **Public IPv4 address**.
3. Open a web browser and enter:  
   `http://<Public-IP>`

4. You should see:  
   `Welcome to Apache HTTPD on EC2!`

---

## Cleanup

- Terminate the EC2 instance to avoid charges.

---

## Summary

You have successfully launched an EC2 Linux instance, installed Apache HTTPD using a user data script, and accessed the web server via the public IP.
