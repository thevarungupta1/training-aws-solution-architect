# Lab Exercise: Enable MFA for IAM User

## Objective
Learn how to enable Multi-Factor Authentication (MFA) for an AWS IAM user.

---

## Prerequisites
- AWS account with administrative access
- IAM user credentials
- MFA device (smartphone with authenticator app or hardware MFA device)

---

## Steps

### 1. Sign in to AWS Management Console
- Go to [https://console.aws.amazon.com/](https://console.aws.amazon.com/)
- Log in with your IAM user or root account.

### 2. Navigate to IAM Service
- In the AWS Console, search for **IAM** and select it.

### 3. Select Users
- In the left navigation pane, click **Users**.

### 4. Choose the User
- Click the username for which you want to enable MFA.

### 5. Open Security Credentials Tab
- Select the **Security credentials** tab.

### 6. Manage MFA Device
- Scroll to **Multi-Factor Authentication (MFA)** section.
- Click **Manage**.

### 7. Choose MFA Device Type
- Select **Virtual MFA device** (recommended for smartphones) or **Hardware MFA device**.
- Click **Continue**.

### 8. Set Up Virtual MFA Device
- If using a smartphone, install an authenticator app (e.g., Google Authenticator, Authy).
- Click **Show QR code**.
- Open the authenticator app and scan the QR code.

### 9. Enter MFA Codes
- The app will generate a 6-digit code.
- Enter two consecutive MFA codes from the app into the AWS Console.
- Click **Assign MFA**.

### 10. Confirm MFA Assignment
- You should see a success message.
- MFA is now enabled for the IAM user.

---

## Verification

1. Sign out of the AWS Console.
2. Sign in again as the IAM user.
3. After entering your password, you will be prompted for an MFA code.
4. Enter the code from your authenticator app to complete login.

---

## Cleanup (Optional)
- To remove MFA, go back to the **Security credentials** tab and click **Remove** next to the MFA device.

---

## Summary
You have successfully enabled MFA for an IAM user, adding an extra layer of security to your AWS account.
