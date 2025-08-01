# Lab 04: Create EC2 Using Linux and Deploy Python Application

## Objective
Learn how to launch a Linux EC2 instance, configure security groups, deploy a simple Python web application, and test it in your browser.

---

## Prerequisites

- AWS account
- Basic knowledge of AWS Console
- SSH client (e.g., PuTTY, Terminal)

---

## Steps

### 1. Launch a Linux EC2 Instance

1. **Log in to AWS Console**
2. Navigate to **EC2** service.
3. Click **Launch Instance**.
4. Enter a name (e.g., `PythonAppServer`).
5. Choose **Amazon Linux 2 AMI** (x86_64).
6. Select an instance type (e.g., `t2.micro` for free tier).
7. Click **Next** until you reach **Configure Security Group**.

---

### 2. Configure Security Group

1. Create a new security group.
2. Add the following inbound rules:
    - **SSH**: TCP, Port 22, Source: Your IP
    - **HTTP**: TCP, Port 80, Source: Anywhere (0.0.0.0/0)
3. Review and launch the instance.
4. Download the key pair (`.pem` file) and save it securely.

---

### 3. Connect to Your EC2 Instance

1. Open your terminal.
2. Run:
    ```bash
    chmod 400 your-key.pem
    ssh -i "your-key.pem" ec2-user@<EC2-Public-IP>
    ```

---

### 4. Install Python and Flask

1. Update packages:
    ```bash
    sudo yum update -y
    ```
2. Install Python3:
    ```bash
    sudo yum install python3 -y
    ```
3. Install Flask:
    ```bash
    pip3 install flask
    ```

---

### 5. Deploy a Simple Python Application

1. Create a new file:
    ```bash
    nano app.py
    ```
2. Paste the following code:
    ```python
    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_world():
         return 'Hello from AWS EC2!'

    if __name__ == '__main__':
         app.run(host='0.0.0.0', port=80)
    ```
3. Save and exit (`Ctrl+X`, then `Y`).

---

### 6. Run the Application

1. Start the app:
    ```bash
    sudo python3 app.py
    ```
    *(Use `sudo` to bind to port 80)*

---

### 7. Test the Application

1. Open your browser.
2. Enter your EC2 public IP (e.g., `http://<EC2-Public-IP>/`).
3. You should see: **Hello from AWS EC2!**

---

## Cleanup

- Stop or terminate the EC2 instance to avoid charges.

---

## Summary

You launched a Linux EC2 instance, configured security groups, deployed a Python Flask app, and tested it in your browser.
