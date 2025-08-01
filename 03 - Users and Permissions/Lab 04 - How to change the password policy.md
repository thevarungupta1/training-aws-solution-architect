# Lab Exercise: Change the Password Policy for IAM Users

## Objective
Learn how to modify the password policy for AWS IAM users to enhance account security.

---

## Prerequisites
- AWS Management Console access with administrative privileges.

---

## Steps

### 1. Sign in to AWS Management Console
- Open [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
- Log in with your administrator account.

### 2. Navigate to IAM Service
- In the top search bar, type **IAM**.
- Click on **IAM** to open the Identity and Access Management dashboard.

### 3. Access Account Settings
- In the left navigation pane, click **Account settings**.

### 4. Edit Password Policy
- Under **Password policy**, click **Edit**.

### 5. Configure Password Policy Options
- Set the desired password requirements, such as:
    - Minimum password length (e.g., 8 characters)
    - Require at least one uppercase letter
    - Require at least one lowercase letter
    - Require at least one number
    - Require at least one non-alphanumeric character
    - Enable password expiration (optional)
    - Prevent password reuse (optional)

### 6. Save Changes
- Review your selections.
- Click **Save changes**.

---

## Verification

1. **Test with an IAM User:**
     - Sign in as an IAM user.
     - Attempt to change the password and verify the new policy is enforced.

2. **Review Policy:**
     - Return to **Account settings** to confirm the updated policy is displayed.

---

## Cleanup (Optional)
- Revert any changes if required for your environment.

---

## Summary
You have successfully changed the password policy for IAM users in AWS.
