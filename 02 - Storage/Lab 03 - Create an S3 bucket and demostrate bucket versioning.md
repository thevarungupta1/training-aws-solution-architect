# Lab Exercise: Demonstrate AWS S3 Bucket Versioning

## Objective
Learn how to enable, use, and observe versioning in an Amazon S3 bucket.

---

## Prerequisites
- AWS account with permissions to create and manage S3 buckets
- AWS Management Console access

---

## Steps

### 1. Create an S3 Bucket

1. Sign in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **Services** > **S3**.
3. Click **Create bucket**.
4. Enter a unique **Bucket name** (e.g., `my-versioning-demo-bucket`).
5. Select a **Region**.
6. Leave other settings as default and click **Create bucket**.

---

### 2. Enable Versioning

1. In the S3 console, select your newly created bucket.
2. Go to the **Properties** tab.
3. Scroll to **Bucket Versioning**.
4. Click **Edit**.
5. Select **Enable**.
6. Click **Save changes**.

---

### 3. Upload an Object

1. Open your bucket.
2. Click **Upload**.
3. Add a file (e.g., `example.txt`).
4. Click **Upload**.

---

### 4. Upload a New Version of the Object

1. Modify `example.txt` locally (e.g., change its content).
2. In the bucket, click **Upload** again.
3. Select the updated `example.txt`.
4. Click **Upload**.
5. When prompted, choose to **replace** the existing file.

---

### 5. View Object Versions

1. In your bucket, click the **example.txt** file.
2. Click the **Versions** tab.
3. Observe multiple versions listed with different **Version IDs**.

---

### 6. Restore a Previous Version

1. In the **Versions** tab, select an older version.
2. Click **Download** to retrieve it.
3. Optionally, **Delete** the latest version to make the previous version current.

---

## Clean Up

1. Delete all objects and versions in the bucket.
2. Delete the bucket to avoid ongoing charges.

---

## Summary

You have enabled S3 bucket versioning, uploaded multiple versions of an object, and observed how versioning works in AWS S3.