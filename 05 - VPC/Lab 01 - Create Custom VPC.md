Here's a detailed, structured step-by-step lab exercise to create a custom VPC with public and private subnets, an Internet Gateway, a NAT Gateway, deploy EC2 instances, and verify connectivity:

---

## **Lab Exercise: AWS VPC with Public & Private Subnets, IGW, NAT Gateway, and EC2 Instances**

### **Objective:**

Create a custom VPC with public and private subnets, configure an Internet Gateway and NAT Gateway, deploy EC2 instances in each subnet, and verify connectivity.

---

### **Architecture Overview:**

```
Custom VPC (10.0.0.0/16)
│
├── Public Subnet (10.0.1.0/24)
│   ├── EC2 Instance (Public Instance)
│   └── Internet Gateway (IGW)
│
├── Private Subnet (10.0.2.0/24)
│   ├── EC2 Instance (Private Instance)
│   └── NAT Gateway (in Public Subnet)
```

---

### **Prerequisites:**

* AWS Account with appropriate IAM permissions
* AWS Management Console access

---

## Step-by-step Lab Guide:

---

## **Step 1: Log in to AWS Management Console**

* Navigate to [AWS Management Console](https://console.aws.amazon.com/).

---

## **Step 2: Create a Custom VPC**

* Go to **VPC** service.
* Click **Create VPC**.

  * Name: `Lab-VPC`
  * IPv4 CIDR block: `10.0.0.0/16`
  * Leave other settings default.
* Click **Create VPC**.

---

## **Step 3: Create Public Subnet**

* In **VPC** dashboard, select **Subnets** → **Create subnet**.

  * VPC: `Lab-VPC`
  * Subnet name: `Public-Subnet`
  * Availability Zone: Select `us-east-1a`
  * IPv4 CIDR block: `10.0.1.0/24`
* Click **Create subnet**.

---

## **Step 4: Create Private Subnet**

* Select **Create subnet** again.

  * VPC: `Lab-VPC`
  * Subnet name: `Private-Subnet`
  * Availability Zone: Select `us-east-1a`
  * IPv4 CIDR block: `10.0.2.0/24`
* Click **Create subnet**.

---

## **Step 5: Create Internet Gateway (IGW)**

* Select **Internet gateways** → **Create internet gateway**.

  * Name: `Lab-IGW`
* Click **Create internet gateway**.
* After creation, select **Actions → Attach to VPC** and select `Lab-VPC`.

---

## **Step 6: Configure Route Table for Public Subnet**

* Select **Route tables**.
* Click **Create route table**.

  * Name: `Public-RT`
  * VPC: `Lab-VPC`
* Click **Create**.
* Select the route table, click **Edit routes**.

  * Add route:

    * Destination: `0.0.0.0/0`
    * Target: Select your created IGW (`Lab-IGW`)
* Click **Save changes**.
* Select the same route table, under **Subnet associations**, click **Edit subnet associations**, choose **Public-Subnet**, and click **Save associations**.

---

## **Step 7: Allocate Elastic IP for NAT Gateway**

* Go to **Elastic IPs** → Click **Allocate Elastic IP address**.
* Note down the allocated Elastic IP.

---

## **Step 8: Create NAT Gateway**

* Select **NAT Gateways** → **Create NAT gateway**.

  * Name: `Lab-NAT-GW`
  * Subnet: Select **Public-Subnet**
  * Elastic IP allocation: Select allocated Elastic IP.
* Click **Create NAT gateway** and wait until it reaches the state **Available**.

---

## **Step 9: Configure Route Table for Private Subnet**

* Go to **Route tables** → **Create route table**.

  * Name: `Private-RT`
  * VPC: `Lab-VPC`
* Click **Create**.
* Select created route table and click **Edit routes**.

  * Add route:

    * Destination: `0.0.0.0/0`
    * Target: Select the NAT Gateway (`Lab-NAT-GW`)
* Click **Save changes**.
* Under **Subnet associations**, click **Edit subnet associations**, select **Private-Subnet**, and click **Save associations**.

---

## **Step 10: Configure Security Groups**

* Go to **Security Groups** → **Create security group**.

  * Name: `Lab-SG`
  * VPC: `Lab-VPC`
  * Inbound rules:

    * SSH (Port 22) from your IP or `0.0.0.0/0` for lab purposes.
    * HTTP (Port 80) from `0.0.0.0/0`.
  * Outbound rules: Allow all.
* Click **Create security group**.

---

## **Step 11: Launch EC2 Instance in Public Subnet**

* Navigate to **EC2** → **Instances** → **Launch Instance**.

  * Name: `Public-EC2`
  * AMI: **Amazon Linux 2 AMI**
  * Instance Type: `t2.micro`
  * Key Pair: Create/choose existing key pair
  * Network settings:

    * VPC: `Lab-VPC`
    * Subnet: `Public-Subnet`
    * Auto-assign Public IP: `Enable`
    * Security group: Select `Lab-SG`
  * User data script (optional for connectivity tests):

```bash
#!/bin/bash
yum install -y httpd
systemctl enable httpd
systemctl start httpd
echo "<h1>Public EC2</h1>" > /var/www/html/index.html
```

* Click **Launch instance**.

---

## **Step 12: Launch EC2 Instance in Private Subnet**

* Repeat EC2 instance creation:

  * Name: `Private-EC2`
  * VPC: `Lab-VPC`
  * Subnet: `Private-Subnet`
  * Auto-assign Public IP: **Disable**
  * Security group: Select `Lab-SG`
  * User data script:

```bash
#!/bin/bash
yum install -y httpd
systemctl enable httpd
systemctl start httpd
echo "<h1>Private EC2</h1>" > /var/www/html/index.html
```

* Launch instance.

---

## **Step 13: Test Connectivity**

### Connect to **Public EC2 Instance**:

* SSH using your key pair:

```bash
ssh -i "your-key.pem" ec2-user@<Public-EC2-Public-IP>
```

### Test internet connectivity from Public EC2:

```bash
ping google.com
curl http://checkip.amazonaws.com
```

### Connect to **Private EC2 Instance via Public EC2 Instance**:

* Transfer your private key to Public EC2 (use SCP).
* From **Public EC2** instance, SSH into Private EC2 (using Private EC2's private IP):

```bash
ssh -i "your-key.pem" ec2-user@<Private-EC2-Private-IP>
```

### Test internet connectivity from Private EC2:

```bash
ping google.com
curl http://checkip.amazonaws.com
```

---

## **Lab Clean-up**

* Terminate EC2 instances.
* Delete NAT gateway and release Elastic IP.
* Detach and delete IGW.
* Delete subnets, route tables, and security groups.
* Finally, delete custom VPC.

---

## **Conclusion:**

You have successfully created a custom AWS VPC with public and private subnets, deployed EC2 instances, configured IGW and NAT Gateway, and tested connectivity between the subnets and internet.
