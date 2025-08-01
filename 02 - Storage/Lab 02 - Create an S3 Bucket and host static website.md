# Lab Exercise: Deploy a Static Website on AWS S3 Bucket

## Objective
Learn how to host a static website using Amazon S3.

---

## Prerequisites
- AWS account
- Basic HTML file (e.g., `index.html`)

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [AWS Console](https://aws.amazon.com/console/).
- Log in with your credentials.

### 2. Create an S3 Bucket
- Navigate to **Services** > **S3**.
- Click **Create bucket**.
- Enter a unique bucket name (e.g., `my-static-website-bucket`).
- Select a region.
- Leave other settings as default.
- Click **Create bucket**.

### 3. Upload Website Files
- Click your bucket name.
- Click **Upload**.
- Add your `index.html` and other static files.
- Click **Upload**.

### 4. Configure Bucket for Static Website Hosting
- Go to **Properties** tab.
- Scroll to **Static website hosting**.
- Click **Edit**.
- Select **Enable**.
- Enter `index.html` as the **Index document**.
- (Optional) Enter `error.html` as the **Error document**.
- Click **Save changes**.

### 5. Set Bucket Policy for Public Access
- Go to **Permissions** tab.
- Click **Bucket Policy**.
- Add the following policy (replace `YOUR_BUCKET_NAME`):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}
```
- Click **Save**.

### 6. Access Your Website
- Go to **Properties** > **Static website hosting**.
- Copy the **Bucket website endpoint** URL.
- Paste it in your browser to view your website.

---

## Cleanup
- Delete the S3 bucket if no longer needed to avoid charges.

---

## Summary
You have successfully deployed a static website using Amazon S3.