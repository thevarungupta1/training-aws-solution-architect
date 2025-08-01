# Lab Exercise: Create a Custom IAM Role and Assign to a User

## Objective
Learn how to create a custom IAM role in AWS and assign it to an IAM user.

---

## Prerequisites
- AWS account access
- IAM administrative permissions

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [AWS Console](https://console.aws.amazon.com/).
- Log in with your credentials.

### 2. Navigate to IAM Service
- In the AWS Console, search for **IAM**.
- Click **IAM** to open the Identity and Access Management dashboard.

### 3. Create a Custom IAM Role
1. In the left sidebar, click **Roles**.
2. Click **Create role**.
3. **Select trusted entity**:
    - Choose **AWS service** (e.g., EC2) or **Another AWS account** as needed.
    - Click **Next**.
4. **Add permissions**:
    - Search for and select the required policies (e.g., `AmazonS3ReadOnlyAccess`).
    - Click **Next**.
5. **Name and tag the role**:
    - Enter a **Role name** (e.g., `CustomS3ReadOnlyRole`).
    - (Optional) Add tags for identification.
    - Click **Create role**.

### 4. Create an IAM User (if needed)
1. In the left sidebar, click **Users**.
2. Click **Add users**.
3. Enter a **User name**.
4. Select **AWS Management Console access** or **Programmatic access** as required.
5. Click **Next** and assign permissions (skip if assigning via role).
6. Click **Create user**.

### 5. Assign Role to IAM User
> **Note:** Roles are typically assumed by AWS services or federated users. To allow an IAM user to assume a role:
1. Edit the **Trust policy** of the role:
    - Go to **Roles**, select your role.
    - Click **Trust relationships** > **Edit trust policy**.
    - Add the following to the `Principal` section:
      ```json
      {
         "Effect": "Allow",
         "Principal": { "AWS": "arn:aws:iam::<account-id>:user/<username>" },
         "Action": "sts:AssumeRole"
      }
      ```
2. Provide the **Role ARN** to the user.
3. The user can assume the role using the AWS CLI:
    ```sh
    aws sts assume-role --role-arn arn:aws:iam::<account-id>:role/CustomS3ReadOnlyRole --role-session-name MySession
    ```

---

## Verification
- Log in as the IAM user.
- Assume the role and verify permissions by accessing resources (e.g., list S3 buckets).

---

## Cleanup
- Delete the role and user if no longer needed.

---

**End of Lab**