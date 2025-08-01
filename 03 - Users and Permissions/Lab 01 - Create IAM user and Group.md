# Lab Exercise: Create IAM User and Group in AWS

## Objective
Learn how to create an IAM user and group, assign permissions, and verify access in AWS.

---

## Prerequisites
- AWS account with administrative access
- Web browser

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [https://aws.amazon.com/](https://aws.amazon.com/)
- Click **Sign In to the Console**
- Enter your credentials

---

### 2. Navigate to IAM Service
- In the AWS Console, search for **IAM** in the search bar
- Click **IAM** to open the Identity and Access Management dashboard

---

### 3. Create a New IAM Group
1. In the left sidebar, click **User groups**
2. Click **Create group**
3. Enter a **Group name** (e.g., `Developers`)
4. (Optional) Attach policies to the group (e.g., `AmazonS3ReadOnlyAccess`)
5. Click **Create group**

---

### 4. Create a New IAM User
1. In the left sidebar, click **Users**
2. Click **Add users**
3. Enter a **User name** (e.g., `john.doe`)
4. Select **AWS Management Console access** or **Programmatic access** as needed
5. Set a custom password or auto-generate one
6. Click **Next**

---

### 5. Add User to Group
1. On the **Set permissions** page, choose **Add user to group**
2. Select the group created earlier (e.g., `Developers`)
3. Click **Next**

---

### 6. Review and Create User
1. Review the user details and permissions
2. Click **Create user**
3. Download or copy the credentials (if programmatic access was selected)

---

### 7. Verify User Access
- Log out of the AWS Console
- Log in with the new IAM user credentials
- Confirm access and permissions

---

## Cleanup (Optional)
- Delete the IAM user and group if no longer needed

---

## Summary
You have successfully created an IAM user and group, assigned permissions, and verified access in AWS.
