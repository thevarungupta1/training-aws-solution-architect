# Lab Exercise: Create and Test a Custom Inline Policy in AWS

## Objective
Learn how to create a custom inline policy for an IAM user and test its permissions.

---

## Prerequisites
- AWS account access
- IAM administrative privileges

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
- Log in with your credentials.

### 2. Navigate to IAM Service
- In the AWS Console, search for **IAM** and select it.

### 3. Create a New IAM User (Optional)
- Click **Users** in the sidebar.
- Click **Add users**.
- Enter a username (e.g., `InlinePolicyUser`).
- Select **Programmatic access** and/or **AWS Management Console access** as needed.
- Click **Next** until you reach **Review**, then click **Create user**.

### 4. Attach a Custom Inline Policy
- Click on the username you created or select an existing user.
- Go to the **Permissions** tab.
- Click **Add inline policy**.

#### a. Choose a Service
- Select a service (e.g., **S3**).

#### b. Set Permissions
- Choose **Actions** (e.g., `ListBucket`, `GetObject`).
- Specify **Resources** (e.g., select a specific bucket ARN).

#### c. Review Policy
- Click **Review policy**.
- Name your policy (e.g., `S3ReadOnlyInlinePolicy`).
- Click **Create policy**.

### 5. Test the Inline Policy

#### a. Sign in as the IAM User
- Log out and sign in with the IAM user's credentials.

#### b. Access the Service
- Try to perform allowed actions (e.g., list objects in the specified S3 bucket).
- Try to perform restricted actions (e.g., delete objects) to confirm denial.

#### c. Verify Permissions
- Confirm that only the actions specified in the inline policy are permitted.

---

## Cleanup (Optional)
- Remove the inline policy or delete the test IAM user to avoid unnecessary permissions.

---

## Summary
You have created a custom inline policy, attached it to an IAM user, and verified its effect by testing allowed and denied actions.
