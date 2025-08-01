# Lab Exercise: Create Linux EC2 Instance and Deploy Web Server

## Objective
Learn how to launch a Linux EC2 instance, configure a security group, install a web server, modify the default index page, and test access via a browser.

---

## Prerequisites
- AWS account
- Basic knowledge of AWS Management Console

---

## Steps

### 1. Launch a Linux EC2 Instance

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **EC2** service.
3. Click **Launch Instance**.
4. Enter a name (e.g., `WebServerLab`).
5. Choose **Amazon Linux 2 AMI** (or preferred Linux AMI).
6. Select an instance type (e.g., `t2.micro` for free tier).
7. Click **Next** until you reach **Configure Security Group**.

---

### 2. Configure Security Group

1. Create a new security group (e.g., `WebServerSG`).
2. Add the following inbound rules:
    - **SSH**: TCP, Port 22, Source: Your IP
    - **HTTP**: TCP, Port 80, Source: Anywhere (0.0.0.0/0)
3. Review and launch the instance.
4. Download the key pair (`.pem` file) for SSH access.

---

### 3. Connect to the EC2 Instance

1. Open a terminal.
2. Run:
    ```bash
    chmod 400 your-key.pem
    ssh -i your-key.pem ec2-user@<Public-IP>
    ```
   Replace `your-key.pem` and `<Public-IP>` with your values.

---

### 4. Install Apache Web Server

1. Update packages:
    ```bash
    sudo yum update -y
    ```
2. Install Apache:
    ```bash
    sudo yum install httpd -y
    ```
3. Start Apache:
    ```bash
    sudo systemctl start httpd
    sudo systemctl enable httpd
    ```

---

### 5. Modify Default Index Page

1. Edit the index page:
    ```bash
    sudo nano /var/www/html/index.html
    ```
2. Replace content with:
    ```html
    <html>
      <head><title>My Web Server</title></head>
      <body>
        <h1>Welcome to My Linux EC2 Web Server!</h1>
      </body>
    </html>
    ```
3. Save and exit.

---

### 6. Test Web Server in Browser

1. Copy the **Public IPv4 address** of your EC2 instance.
2. Open a browser and navigate to:
    ```
    http://<Public-IP>
    ```
3. You should see your custom index page.

---

## Cleanup

- Terminate the EC2 instance to avoid charges.

---

## Summary

You have launched a Linux EC2 instance, configured security, installed Apache, customized the index page, and verified access via a browser.
