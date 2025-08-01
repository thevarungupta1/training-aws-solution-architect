# Lab Exercise: Create an AWS EC2 Instance (Linux)

## Objective
Learn how to launch a Linux-based EC2 instance on AWS.

---

## Prerequisites
- AWS account
- Basic knowledge of AWS Management Console

---

## Steps

### 1. Log in to AWS Console
- Go to [https://aws.amazon.com/](https://aws.amazon.com/)
- Sign in with your credentials.

### 2. Navigate to EC2 Dashboard
- In the AWS Console, search for **EC2**.
- Click **EC2** to open the dashboard.

### 3. Launch Instance
- Click **Launch Instance**.
- Enter a name for your instance (e.g., `LinuxLabInstance`).

### 4. Choose an Amazon Machine Image (AMI)
- Select **Amazon Linux 2023** (or preferred Linux AMI).
- Click **Select**.

### 5. Choose Instance Type
- Select **t2.micro** (eligible for free tier).
- Click **Next**.

### 6. Configure Instance Details
- Leave default settings for basic setup.
- (Optional) Adjust network/subnet if needed.

### 7. Add Storage
- Default storage is usually sufficient.
- Modify size/type if required.

### 8. Add Tags
- Click **Add Tag**.
- Key: `Name`, Value: `LinuxLabInstance`.

### 9. Configure Security Group
- Create a new security group.
- Add rule: **SSH**, Port **22**, Source: `My IP` (for secure access).

### 10. Review and Launch
- Review all settings.
- Click **Launch**.

### 11. Select/Create Key Pair
- Select an existing key pair or create a new one.
- Download the `.pem` file and store it securely.

### 12. Access Your Instance
- Go to **Instances** in EC2 dashboard.
- Wait for status to become **running**.
- Copy the **Public IPv4 address**.

#### Connect via SSH:
```bash
ssh -i /path/to/your-key.pem ec2-user@<Public-IP>
```
- Replace `/path/to/your-key.pem` with your key file path.
- Replace `<Public-IP>` with your instance's public IP.

---

## Cleanup
- To avoid charges, terminate the instance after use:
    - Select the instance.
    - Click **Instance State > Terminate Instance**.

---

## Summary
You have successfully launched and connected to a Linux EC2 instance on AWS.
