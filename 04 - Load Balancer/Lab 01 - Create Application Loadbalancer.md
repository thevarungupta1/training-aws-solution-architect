# Lab Exercise: Deploying Two EC2 Instances with HTTP Server Behind AWS Load Balancer

## Prerequisites

* AWS Account
* IAM user with permissions to manage EC2, Security Groups, and ELB
* Default or Custom VPC configured

## Step-by-Step Guide

### Step 1: Log into AWS Management Console

Navigate to [AWS Console](https://console.aws.amazon.com).

### Step 2: Create a Security Group

* Go to **EC2 → Security Groups**
* Click **Create Security Group**
* **Name**: `WebServerSG`
* **Inbound Rules**:

  * HTTP (Port 80) from `0.0.0.0/0`
  * SSH (Port 22) from your IP address
* **Outbound Rules**: Allow all (default)
* Click **Create**

### Step 3: Launch Two EC2 Instances

#### EC2 Configuration:

* Navigate to **EC2 → Instances → Launch Instances**
* Choose **Amazon Linux 2 AMI**
* Select **t2.micro**
* Configure Instance Details:

  * **Network**: Choose your default/custom VPC
  * **Auto-assign Public IP**: Enable

#### Add User Data (Under Advanced details):

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Welcome to $(hostname -f)</h1>" > /var/www/html/index.html
```

* Click **Next: Add Storage** (accept defaults)
* Click **Next: Add Tags** (optional)
* Click **Next: Configure Security Group** and select existing `WebServerSG`
* Click **Review and Launch**
* Use an existing key pair or create one
* Click **Launch**
* **Repeat this step** to create the second EC2 instance

### Step 4: Verify Instances

* After both instances show as **Running**, copy their public IP addresses
* Open your browser and navigate to `http://<public-ip>` for both instances
* You should see: **Welcome to ip-xxx-xxx-xxx-xxx**

### Step 5: Create Target Group

* Go to **EC2 → Load Balancing → Target Groups**
* Click **Create Target Group**
* **Target Type**: Instances
* **Target Group Name**: `WebServerTG`
* **Protocol**: HTTP, Port 80
* Select your VPC
* Click **Next**
* Register both EC2 instances
* Click **Create Target Group**

### Step 6: Create Application Load Balancer (ALB)

* Go to **EC2 → Load Balancers**
* Click **Create Load Balancer → Application Load Balancer**
* **Name**: `WebServerALB`
* **Scheme**: Internet-facing
* **IP address type**: IPv4
* **Listeners**: HTTP on port 80
* **Availability Zones**: Choose at least two AZs
* Click **Next**
* Choose existing Security Group `WebServerSG`
* Click **Next**
* Select **Existing target group**: `WebServerTG`
* Click **Next**, review and click **Create**

### Step 7: Test Load Balancer

* Wait until the ALB state is **active**
* Copy the ALB DNS name from the console
* Open your browser and navigate to `http://<ALB-DNS-name>`
* Refresh multiple times to observe traffic routed between the two EC2 instances

### Cleanup

* Terminate EC2 instances
* Delete Load Balancer and Target Group
* Delete Security Group

## Outcome

You've successfully:

* Launched two EC2 instances with Apache HTTP server using user data
* Configured an Application Load Balancer
* Verified load-balanced web access.
