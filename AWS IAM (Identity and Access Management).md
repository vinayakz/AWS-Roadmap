# AWS IAM (Identity and Access Management)

## Introduction

When you create an AWS account, you get a **Root User**. The root user has full access to all AWS services.

However, using the root account for daily work is **not recommended** because it is very powerful.

AWS provides **IAM (Identity and Access Management)** to securely manage users, permissions, and access to AWS resources.

---

# What is AWS IAM?

**AWS IAM (Identity and Access Management)** is a service that helps you control **who can access AWS resources** and **what actions they can perform**.

Think of IAM like a **security guard** for your AWS account.

It allows you to:

- Create users
- Create groups
- Assign permissions
- Control access to AWS services
- Improve account security

### Example

Suppose your company has:

- Developer
- Tester
- DevOps Engineer
- Manager

Not everyone needs full AWS access.

Using IAM:

- Developer → EC2 & S3 access
- Tester → Read-only access
- Manager → Billing access
- DevOps → Full infrastructure access

Everyone only gets the permissions they need.

---

# Why Do We Need IAM?

Without IAM:

- Everyone uses the Root Account ❌
- High security risk ❌
- Anyone can accidentally delete resources ❌

With IAM:

- Individual login for every user ✅
- Limited permissions ✅
- Better security ✅
- Easy access management ✅

---

# AWS IAM Functions

IAM provides several important features.

## 1. IAM Users

An IAM User represents a person or application that needs access to AWS.

Examples:

- Developer
- DevOps Engineer
- Automation Script

Each IAM user has:

- Username
- Password (Console Login)
- Access Keys (CLI/API)

---

## 2. IAM Groups

A Group is a collection of IAM users.

Instead of assigning permissions one by one, assign permissions to the group.

Example:

Developers Group

- John
- Rahul
- Priya

All developers automatically receive the same permissions.

---

## 3. IAM Policies

Policies define **what users are allowed to do**.

Policies are written in JSON.

Example:

```json
{
  "Effect": "Allow",
  "Action": "s3:*",
  "Resource": "*"
}
```

This policy allows full access to Amazon S3.

---

## 4. IAM Roles

Roles provide temporary access.

Roles are mostly used by:

- EC2
- Lambda
- ECS
- EKS
- Cross Account Access

Example:

Instead of storing AWS Access Keys inside an EC2 server, attach an IAM Role.

The EC2 instance automatically gets temporary credentials.

This is much more secure.

---

# How to Create an IAM User

Follow these steps:

### Step 1

Login to AWS Console.

---

### Step 2

Search for **IAM**.

---

### Step 3

Click

```
Users
```

---

### Step 4

Click

```
Create User
```

---

### Step 5

Enter Username

Example:

```
vinayak
```

---

### Step 6

Select

```
Provide User Access to AWS Management Console
```

(Optional if console login is required.)

---

### Step 7

Choose Password

- Auto-generated
- Custom password

---

### Step 8

Assign Permissions

Options:

- Add user to group
- Copy permissions
- Attach policies directly

Recommended:

Create a group and add the user to it.

---

### Step 9

Review and Create User.

Done!

Your IAM User is now ready.

---

# What is MFA in IAM?

**MFA (Multi-Factor Authentication)** adds an extra layer of security.

Instead of logging in with only a password,

AWS also asks for a verification code.

This code comes from:

- Google Authenticator
- Microsoft Authenticator
- Authy
- Hardware Security Key

---

## Without MFA

Login:

```
Username
↓

Password
↓

Access Granted
```

If someone steals your password, they can log in.

---

## With MFA

Login:

```
Username
↓

Password
↓

Verification Code
↓

Access Granted
```

Even if someone knows your password, they **cannot log in without the verification code**.

---

# Different Ways of Using AWS Services

There are three common ways to use AWS.

---

## 1. AWS Management Console

This is the graphical web interface.

Best for:

- Beginners
- Manual tasks

Example:

- Launch EC2
- Create S3 Bucket
- Configure IAM

---

## 2. AWS CLI (Command Line Interface)

AWS CLI lets you manage AWS using terminal commands.

Example:

```bash
aws s3 ls
```

List EC2 instances:

```bash
aws ec2 describe-instances
```

Best for:

- DevOps Engineers
- Automation
- Scripting

---

## 3. AWS SDK

SDK allows developers to control AWS using programming languages.

Supported languages:

- Python (Boto3)
- Java
- JavaScript
- Go
- C#
- PHP

Example:

Python:

```python
import boto3

s3 = boto3.client('s3')

print(s3.list_buckets())
```

Best for:

- Applications
- Backend development
- Automation

---

# AWS CLI Installation

## Windows

1. Download AWS CLI Installer.
2. Run the installer.
3. Finish installation.
4. Open Command Prompt.

Check installation:

```bash
aws --version
```

Example Output:

```bash
aws-cli/2.18.10 Python/3.12
```

---

## macOS

Install using Homebrew:

```bash
brew install awscli
```

Verify:

```bash
aws --version
```

---

# Configure AWS CLI with Access Keys

After installing AWS CLI, configure it.

Run:

```bash
aws configure
```

AWS asks for:

```
AWS Access Key ID
```

```
AWS Secret Access Key
```

```
Default Region
```

Example:

```
ap-south-1
```

```
Default Output Format
```

Example:

```
json
```

Done!

Now AWS CLI can access your AWS account.

---

# What are Access Keys?

Access Keys are used to access AWS from:

- AWS CLI
- SDK
- Scripts
- Applications

They contain:

- Access Key ID
- Secret Access Key

**Important:** Never share your Secret Access Key with anyone.

---

# AWS IAM Best Practices

Follow these best practices to keep your AWS account secure.

### ✅ Don't use the Root User for daily work

Use the root account only for account-level tasks.

---

### ✅ Create IAM Users

Give every person their own AWS account login.

---

### ✅ Use IAM Groups

Manage permissions through groups instead of assigning them individually.

---

### ✅ Follow the Principle of Least Privilege

Give users **only the permissions they need**, nothing more.

---

### ✅ Enable MFA

Always enable Multi-Factor Authentication, especially for the root user.

---

### ✅ Rotate Access Keys

Change Access Keys regularly to reduce security risks.

---

### ✅ Never Share Access Keys

Keep your Secret Access Key private.

Never upload it to:

- GitHub
- GitLab
- Bitbucket
- Public repositories

---

### ✅ Use IAM Roles

Instead of storing Access Keys inside EC2 or applications, use IAM Roles whenever possible.

---

### ✅ Remove Unused Users

Delete users who no longer need access.

---

### ✅ Review Permissions Regularly

Check IAM users, groups, roles, and policies to ensure they still have the correct access.

---

# Summary

AWS IAM is one of the most important AWS services because it controls access to your AWS resources.

With IAM, you can:

- Create users
- Create groups
- Assign permissions
- Use IAM Roles
- Secure accounts with MFA
- Access AWS using Console, CLI, or SDK

Following IAM best practices helps keep your AWS environment secure and organized.

---

# Quick Interview Questions

### Q1. What is AWS IAM?

IAM is a service used to securely manage users, permissions, and access to AWS resources.

---

### Q2. What is the difference between an IAM User and an IAM Role?

- IAM User: Permanent identity for a person or application.
- IAM Role: Temporary identity that provides temporary permissions.

---

### Q3. Why should we avoid using the Root User?

Because it has full access to all AWS resources and poses a higher security risk if compromised.

---

### Q4. What is MFA?

MFA (Multi-Factor Authentication) adds an extra layer of security by requiring a verification code in addition to a password.

---

### Q5. What are Access Keys used for?

Access Keys allow applications, scripts, SDKs, and AWS CLI to access AWS resources securely.

---

## Happy Learning! 🚀

If you found this guide helpful, feel free to ⭐ star the repository and share it with others learning AWS.
