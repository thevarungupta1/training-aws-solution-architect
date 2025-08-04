# Lab Exercise: Deploying AWS Network Load Balancer (NLB)

## Prerequisites

* AWS Account
* IAM permissions to manage EC2, Security Groups, and Elastic Load Balancing (ELB)
* Default or custom VPC setup

## Step-by-Step Guide

### Step 1: Log into AWS Management Console

Navigate to [AWS Console](https://console.aws.amazon.com).

### Step 2: Create a Security Group

* Navigate to **EC2 → Security Groups**
* Click **Create Security Group**
* **Name**: `NLB-SG`
* **Inbound Rules**:

  * HTTP (Port 80): `0.0.0.0/0`
  * SSH (Port 22): Your IP address
* **Outbound Rules**: Allow all (default)
* Click **Create**

### Step 3: Launch Two EC2 Instances

* Go to **EC2 → Instances → Launch Instances**
* Select **Amazon Linux 2 AMI**
* Choose instance type **t2.micro**
* Configure Instance:

  * Network: Choose your default/custom VPC
  * Enable auto-assign public IP

#### Add User Data (Advanced Details):

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>NLB instance: $(hostname -f)</h1>" > /var/www/html/index.html
```

* Attach `NLB-SG` Security Group
* Launch both instances

### Step 4: Verify EC2 Instances

* After instances are **Running**, test their public IPs in your browser:

  ```
  http://<public-ip>
  ```
* Confirm each instance shows its unique hostname

### Step 5: Create Target Group

* Go to **EC2 → Load Balancing → Target Groups**
* Click **Create Target Group**
* **Target type**: Instances
* **Name**: `NLB-TG`
* **Protocol**: TCP, Port 80
* Select your VPC
* Click **Next** and register both EC2 instances
* Click **Create**

### Step 6: Create Network Load Balancer

* Navigate to **EC2 → Load Balancers → Create Load Balancer**
* Choose **Network Load Balancer**
* **Name**: `MyNLB`
* **Scheme**: Internet-facing
* **Listeners**: TCP on port 80
* Select two or more AZs
* Click **Next**
* Select your existing Target Group: `NLB-TG`
* Click **Create Load Balancer**

### Step 7: Test Network Load Balancer

* Wait until NLB is **active**
* Copy the NLB DNS name
* Open your browser:

  ```
  http://<NLB-DNS-name>
  ```
* Refresh multiple times; the requests should alternate between your EC2 instances

### Cleanup

* Terminate EC2 instances
* Delete Load Balancer and Target Group
* Delete Security Group

## Outcome

You've successfully:

* Created two EC2 instances with HTTP servers via user data
* Configured and tested an AWS Network Load Balancer
