# Lab 04: Create an S3 Bucket and Demonstrate Encryption

## Objective
Learn how to create an Amazon S3 bucket and enable encryption for objects stored in the bucket.

---

## Prerequisites
- AWS account
- IAM user with permissions to manage S3

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [https://aws.amazon.com/](https://aws.amazon.com/) and log in.

### 2. Navigate to S3 Service
- In the AWS Console, search for **S3** and select it.

### 3. Create a New S3 Bucket
- Click **Create bucket**.
- Enter a unique **Bucket name** (e.g., `my-encrypted-bucket-lab`).
- Select an **AWS Region**.
- Leave other settings as default.
- Click **Create bucket**.

### 4. Enable Default Encryption
- In the S3 console, select your new bucket.
- Go to the **Properties** tab.
- Scroll to **Default encryption**.
- Click **Edit**.
- Choose **Enable**.
- Select an encryption type:
    - **Amazon S3 managed keys (SSE-S3)**
    - **AWS Key Management Service keys (SSE-KMS)**
- For SSE-KMS, select a KMS key or create a new one.
- Click **Save changes**.

### 5. Upload an Object to the Bucket
- Go to the **Objects** tab.
- Click **Upload**.
- Add a file from your computer.
- Click **Upload**.

### 6. Verify Encryption
- Select the uploaded object.
- Click **Properties**.
- Under **Encryption**, confirm the encryption type matches your selection.

---

## Clean Up
- Delete the uploaded object.
- Delete the S3 bucket to avoid charges.

---

## Summary
You have created an S3 bucket, enabled encryption, uploaded an object, and verified encryption settings.
