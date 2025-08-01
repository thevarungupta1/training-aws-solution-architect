# Lab Exercise: Create an S3 Bucket, Upload an Image and Set Public Access

## Prerequisites
- AWS account
- AWS Management Console access
- An image file to upload

---

## Step 1: Create an S3 Bucket

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **Services** > **S3**.
3. Click **Create bucket**.
4. Enter a unique **Bucket name** (e.g., `my-public-image-bucket`).
5. Select the desired **AWS Region**.
6. Leave other settings as default and click **Create bucket**.

---

## Step 2: Upload an Image File

1. Click on your newly created bucket name.
2. Click **Upload** > **Add files**.
3. Select your image file (e.g., `sample-image.jpg`).
4. Click **Upload**.

---

## Step 3: Modify Bucket Policy for Public Access

1. In your bucket, go to the **Permissions** tab.
2. Scroll to **Bucket policy** and click **Edit**.
3. Paste the following policy, replacing `YOUR_BUCKET_NAME` with your bucket name:

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

4. Click **Save changes**.

---

## Step 4: Enable Public Access Settings

1. In the **Permissions** tab, scroll to **Block public access (bucket settings)**.
2. Click **Edit**.
3. Uncheck **Block all public access**.
4. Confirm changes and save.

---

## Step 5: Get the Public URL of the Image

1. Go to the **Objects** tab in your bucket.
2. Click on your uploaded image file.
3. Copy the **Object URL** (e.g., `https://YOUR_BUCKET_NAME.s3.amazonaws.com/sample-image.jpg`).

---


## Cleanup (Optional)

- Delete the image or bucket if no longer needed to avoid charges.

---

**End of Lab**