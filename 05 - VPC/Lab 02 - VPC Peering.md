Here's a structured, step-by-step lab exercise to create and configure a **VPC Peering Connection** between two separate VPCs, launch EC2 instances in each, and verify connectivity:

---

# **Lab Exercise: AWS VPC Peering Connection**

## Objective:

* Create two separate VPCs with different CIDR blocks.
* Launch EC2 instances in both VPCs.
* Set up a VPC Peering Connection between the VPCs.
* Test connectivity by SSH-ing between EC2 instances in different VPCs.

---

## Lab Architecture:

```
VPC-1 (CIDR: 10.10.0.0/16)
│
└── EC2 Instance (10.10.1.0/24 - Public Subnet)

<--- VPC Peering Connection --->

VPC-2 (CIDR: 10.20.0.0/16)
│
└── EC2 Instance (10.20.1.0/24 - Public Subnet)
```

---

## Step-by-Step Instructions:

---

## **Step 1: Log in to AWS Console**

* Access the [AWS Management Console](https://console.aws.amazon.com/ec2/).

---

## **Step 2: Create Two VPCs**

* Go to **VPC** → **Your VPCs** → **Create VPC**:

### **Create VPC-1:**

* **Name Tag:** `VPC-1`
* **IPv4 CIDR:** `10.10.0.0/16`
* Click **Create VPC**.

### **Create VPC-2:**

* **Name Tag:** `VPC-2`
* **IPv4 CIDR:** `10.20.0.0/16`
* Click **Create VPC**.

---

## **Step 3: Create Public Subnets**

* Navigate to **Subnets** → **Create subnet**.

### **Subnet for VPC-1:**

* **VPC:** `VPC-1`
* **Subnet name:** `VPC-1-Public-Subnet`
* **Availability Zone:** Select `us-east-1a`
* **CIDR:** `10.10.1.0/24`
* Click **Create subnet**.

### **Subnet for VPC-2:**

* **VPC:** `VPC-2`
* **Subnet name:** `VPC-2-Public-Subnet`
* **Availability Zone:** Select `us-east-1a`
* **CIDR:** `10.20.1.0/24`
* Click **Create subnet**.

---

## **Step 4: Create and Attach Internet Gateways (IGWs)**

* Go to **Internet Gateways** → **Create internet gateway**.

### **IGW for VPC-1:**

* **Name:** `VPC-1-IGW`
* Click **Create internet gateway**.
* Select created IGW, choose **Actions → Attach to VPC → `VPC-1`**.

### **IGW for VPC-2:**

* Repeat same steps for `VPC-2`:
* Name it `VPC-2-IGW` and attach it to `VPC-2`.

---

## **Step 5: Create Route Tables & Configure Public Subnets**

### **Route Table for VPC-1:**

* Go to **Route Tables** → **Create route table**.

  * Name: `VPC-1-RT`
  * VPC: `VPC-1`
* Add route: `0.0.0.0/0` → `VPC-1-IGW`
* Associate route table with `VPC-1-Public-Subnet`.

### **Route Table for VPC-2:**

* Create another route table:

  * Name: `VPC-2-RT`
  * VPC: `VPC-2`
* Add route: `0.0.0.0/0` → `VPC-2-IGW`
* Associate with `VPC-2-Public-Subnet`.

---

## **Step 6: Configure Security Groups**

* Navigate to **Security Groups** → **Create security group**.

### **Security Group VPC-1:**

* Name: `SG-VPC-1`
* VPC: `VPC-1`
* Inbound rules:

  * SSH (port 22) from `0.0.0.0/0`
  * ICMP (ping) from `0.0.0.0/0`
* Outbound: Allow all.

### **Security Group VPC-2:**

* Repeat for `VPC-2`:
* Name: `SG-VPC-2`
* Same inbound/outbound rules.

---

## **Step 7: Launch EC2 Instances**

* Navigate to **EC2** → **Instances** → **Launch Instance**.

### **Instance in VPC-1:**

* Name: `VPC-1-Instance`
* AMI: **Amazon Linux 2**
* Instance Type: `t2.micro`
* Key Pair: Create or select an existing one
* Network settings:

  * VPC: `VPC-1`
  * Subnet: `VPC-1-Public-Subnet`
  * Auto-assign Public IP: **Enable**
  * Security group: `SG-VPC-1`
* Click **Launch Instance**.

### **Instance in VPC-2:**

* Repeat steps, name as `VPC-2-Instance`:

  * VPC: `VPC-2`
  * Subnet: `VPC-2-Public-Subnet`
  * Security group: `SG-VPC-2`
* Launch.

---

## **Step 8: Establish VPC Peering Connection**

* Navigate to **VPC → Peering connections**.
* Click **Create peering connection**:

  * Name: `VPC-1-to-VPC-2`
  * Requester VPC: Select `VPC-1`
  * Accepter VPC: Select `Another VPC in your account`, choose `VPC-2`
* Click **Create peering connection**.

### **Accept VPC Peering Request:**

* Select created peering connection, click **Actions → Accept Request**.

---

## **Step 9: Update Route Tables for Peering**

* Add peering routes in both route tables:

### **For VPC-1-RT:**

* Edit routes, add:

  * Destination: `10.20.0.0/16`
  * Target: VPC Peering Connection (`pcx-xxxxxxx`)

### **For VPC-2-RT:**

* Edit routes, add:

  * Destination: `10.10.0.0/16`
  * Target: VPC Peering Connection (`pcx-xxxxxxx`)

---

## **Step 10: Testing Connectivity**

* SSH into **VPC-1-Instance** using public IP:

```bash
ssh -i your-key.pem ec2-user@<VPC-1-Instance-Public-IP>
```

* From **VPC-1-Instance**, SSH into **VPC-2-Instance** using its private IP:

```bash
ssh -i your-key.pem ec2-user@<VPC-2-Instance-Private-IP>
```

* Test ping connectivity:

```bash
ping <VPC-2-Instance-Private-IP>
```

* Similarly, verify from **VPC-2-Instance** to **VPC-1-Instance**.

---

## **Lab Cleanup (Important):**

To avoid charges, delete all created resources:

* Terminate EC2 instances.
* Delete Security Groups.
* Delete Route Tables.
* Detach & Delete Internet Gateways.
* Delete VPC Peering Connection.
* Delete Subnets.
* Delete VPCs.

---

## **Lab Completion:**

You have successfully configured a VPC Peering Connection between two AWS VPCs and tested connectivity.

---
