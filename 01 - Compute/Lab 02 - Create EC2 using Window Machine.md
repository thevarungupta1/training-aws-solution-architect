# Lab Exercise: Create a Windows EC2 Instance and Connect via RDP

## Objective
Deploy a Windows EC2 instance on AWS and connect to it using Remote Desktop Protocol (RDP).

---

## Prerequisites
- AWS account
- IAM user with permissions to launch EC2 instances
- RDP client (e.g., Remote Desktop Connection on Windows)

---

## Steps

### 1. Log in to AWS Management Console
- Open [AWS Console](https://console.aws.amazon.com/).
- Sign in with your credentials.

### 2. Launch a Windows EC2 Instance
1. Navigate to **EC2** service.
2. Click **Launch Instance**.
3. Enter a name for your instance (e.g., `WindowsLabInstance`).
4. Choose an Amazon Machine Image (AMI):
    - Select **Microsoft Windows Server** (e.g., Windows Server 2019 Base).
5. Choose an Instance Type:
    - Select `t2.micro` (eligible for free tier).
6. Configure Key Pair:
    - Create a new key pair or select an existing one.
    - Download and save the `.pem` file securely.
7. Network Settings:
    - Select default VPC and subnet.
    - Allow RDP traffic by adding a rule to the security group:
      - Type: `RDP`
      - Port: `3389`
      - Source: `My IP` (recommended) or `Anywhere` (not secure)
8. Click **Launch Instance**.

### 3. Retrieve Administrator Password
1. Go to **Instances** in EC2 dashboard.
2. Select your running Windows instance.
3. Wait until the instance state is **running** and status checks are passed.
4. Right-click the instance, select **Get Windows Password**.
5. Upload your key pair `.pem` file.
6. Click **Decrypt Password**.
7. Copy the displayed password.

### 4. Connect to the Instance via RDP
1. Note the **Public IPv4 address** of your instance.
2. Open your RDP client.
3. Enter the public IP address.
4. Username: `Administrator`
5. Password: Paste the decrypted password.
6. Click **Connect**.

---

## Cleanup
- Terminate the EC2 instance to avoid charges:
  - Select the instance, click **Instance State > Terminate**.

---

## Summary
You have successfully launched a Windows EC2 instance and connected to it using RDP.
