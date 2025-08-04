## Lab Exercise: Creating a Custom VPC with Public and Private Subnets and Deploying EC2 Instances

### Objective:

Create a custom VPC with a public and private subnet, deploy one EC2 instance in each subnet, and test connectivity.

### Prerequisites:

* AWS account with sufficient permissions.
* AWS Management Console access.

---

### Step 1: Login to AWS Console

* Log in to [AWS Management Console](https://console.aws.amazon.com).

---

### Step 2: Create Custom VPC

* Navigate to **VPC**.
* Click **Create VPC**.
* Select **VPC only**.
* Enter details:

  * Name tag: `Lab-VPC`
  * IPv4 CIDR block: `10.0.0.0/16`
* Click **Create VPC**.

---

### Step 3: Create Subnets

* Under **Subnets**, click **Create subnet**.

**Public Subnet:**

* VPC: Select `Lab-VPC`
* Subnet name: `Public-Subnet`
* Availability Zone: Choose one (e.g., `us-east-1a`)
* IPv4 CIDR block: `10.0.1.0/24`

**Private Subnet:**

* Click **Add new subnet**
* VPC: `Lab-VPC`
* Subnet name: `Private-Subnet`
* Availability Zone: same as public subnet (e.g., `us-east-1a`)
* IPv4 CIDR block: `10.0.2.0/24`
* Click **Create subnet**.

---

### Step 4: Create Internet Gateway and Attach to VPC

* Under **Internet Gateways**, click **Create internet gateway**.
* Name tag: `Lab-IGW`
* Click **Create**.
* Select the created IGW and click **Actions > Attach to VPC**.
* Select `Lab-VPC`, click **Attach**.

---

### Step 5: Create Route Tables

**Public Route Table:**

* Under **Route Tables**, click **Create route table**.
* Name tag: `Public-RT`
* VPC: Select `Lab-VPC`
* Click **Create**.
* Edit routes, click **Add route**:

  * Destination: `0.0.0.0/0`
  * Target: `Lab-IGW`
* Save.
* Under **Subnet associations**, select `Public-Subnet`.

**Private Route Table:**

* Create another route table `Private-RT`.
* No additional routes (leave default).
* Associate with `Private-Subnet`.

---

### Step 6: Create Security Groups

* Navigate to **Security Groups** > **Create security group**:

  * Name: `Lab-SG`
  * VPC: `Lab-VPC`
  * Rules:

    * Allow SSH (`port 22`) from your IP (`My IP`).
    * Allow ICMP (ping) from CIDR `10.0.0.0/16`.
* Click **Create security group**.

---

### Step 7: Launch EC2 Instances

Navigate to **EC2 Dashboard > Instances > Launch Instances**.

**Public Instance:**

* Name: `Public-Instance`
* AMI: **Amazon Linux 2**
* Instance type: `t2.micro`
* Key pair: create or select existing
* Network:

  * VPC: `Lab-VPC`
  * Subnet: `Public-Subnet`
  * Auto-assign Public IP: **Enable**
* Security Group: `Lab-SG`
* Launch Instance.

**Private Instance:**

* Name: `Private-Instance`
* AMI: **Amazon Linux 2**
* Instance type: `t2.micro`
* Key pair: same as above
* Network:

  * VPC: `Lab-VPC`
  * Subnet: `Private-Subnet`
  * Auto-assign Public IP: **Disable**
* Security Group: `Lab-SG`
* Launch Instance.

---

### Step 8: Test Connectivity

* SSH into `Public-Instance`:

```bash
ssh -i "keypair.pem" ec2-user@<Public-Instance-IP>
```

* From Public Instance, ping Private Instance:

```bash
ping <Private-Instance-Private-IP>
```

**You should see successful ping replies.**

---

### Clean-up:

* Terminate EC2 instances.
* Delete created VPC components to avoid unnecessary charges.

---

### Conclusion:

You've successfully set up a custom VPC with public and private subnets, deployed EC2 instances in each subnet, and tested connectivity.
