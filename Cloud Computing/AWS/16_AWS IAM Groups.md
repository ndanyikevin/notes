In **AWS IAM (Identity and Access Management)**, a **Group** is simply a **collection of IAM users** that share the same permissions.

Think of it like this:

> Instead of giving each user permissions one by one, you assign permissions to a **group**, and every user in that group automatically inherits them.

---

### 🧩 Example:

You might have:

- **Admins** → Full access to everything
    
- **Developers** → Access to EC2, Lambda, S3
    
- **Viewers** → Read-only access only
    

So if a new developer joins your team, you just **add them to the “Developers” group**, and they instantly get all the right permissions.

---

### ⚙️ How it works

- You **create a group** (e.g., “Developers”).
    
- You **attach IAM policies** to that group (like `AmazonS3FullAccess`, `AWSLambdaReadOnlyAccess`, etc.).
    
- You **add users** to that group.
    
- Each user gets all permissions from the group’s policies.
    

---

### 🧠 Notes

- Groups **cannot contain other groups** — only users.
    
- A user **can belong to multiple groups**.
    
- Groups make **access management and audits much easier**.
    

---

### 💡 Example (CLI)

```bash
aws iam create-group --group-name Developers
aws iam attach-group-policy \
  --group-name Developers \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
aws iam add-user-to-group --group-name Developers --user-name Alice
```

---

✅ **In short:**  
**IAM Group = A set of users + shared permissions.**  
They help you manage access control efficiently and consistently.

### Policy Documents
---
An **AWS policy document** is a **JSON file that defines permissions** — it tells AWS **who** can do **what actions** on **which resources**, and under **what conditions**.

Think of it as a **rulebook** for access control in AWS.

---

### 🧩 Structure of a policy document

A policy is written in **JSON** and contains:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow" | "Deny",
      "Action": "service:operation",
      "Resource": "arn:aws:service:region:account-id:resource",
      "Condition": { ... }  // optional
    }
  ]
}
```

---

### 🧠 Key parts explained

|Field|Meaning|
|---|---|
|**Version**|Policy language version (always `"2012-10-17"`).|
|**Statement**|The actual rule(s) inside the policy.|
|**Effect**|Either `"Allow"` or `"Deny"`.|
|**Action**|The AWS actions being controlled (e.g. `s3:PutObject`, `ec2:StartInstances`).|
|**Resource**|The specific AWS resources (e.g. S3 bucket, EC2 instance ARN).|
|**Condition** _(optional)_|Extra rules — e.g. “only allow from specific IP” or “only if MFA is enabled.”|

---

### 💡 Example 1 — Allow user to read objects in one S3 bucket

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

---

### 💡 Example 2 — Deny EC2 stop/start unless MFA is used

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": ["ec2:StartInstances", "ec2:StopInstances"],
      "Resource": "*",
      "Condition": {"BoolIfExists": {"aws:MultiFactorAuthPresent": "false"}}
    }
  ]
}
```

---

### 🧱 Types of policy documents

1. **Identity-based policies** – attached to users, groups, or roles.
    
2. **Resource-based policies** – attached directly to resources (like S3 buckets, SQS queues, etc.).
    
3. **Permission boundaries** – limit the maximum permissions a user or role can have.
    
4. **Service control policies (SCPs)** – used in AWS Organizations to control permissions across multiple accounts.
    

---

✅ **In short:**

> A **policy document** is a JSON file that defines **who can do what, on which resources, under which conditions** in AWS.

## Types of Policies
---
- Managed policy
- Inline policy

A **managed policy** in AWS is a **predefined or reusable permission policy** that you can **attach to multiple IAM users, groups, or roles** — instead of writing a new JSON policy for each one.

### 🧩 Two types of managed policies

1. **AWS Managed Policies**
    
    - Created and maintained **by AWS**.
        
    - Automatically updated when AWS adds new features or services.
        
    - Great for common roles (e.g., admins, developers, read-only users).
        
    
    💡 Examples:
    
    - `AdministratorAccess`
        
    - `AmazonS3FullAccess`
        
    - `AmazonEC2ReadOnlyAccess`
        
    - `AWSLambdaExecute`
        

---

2. **Customer Managed Policies**
    
    - Created and managed **by you** (your organization).
        
    - You write the JSON policy document and can update or version it anytime.
        
    - More control and customization than AWS-managed ones.
        
    
    💡 Example:
    
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": ["s3:ListBucket", "s3:GetObject"],
          "Resource": ["arn:aws:s3:::project-data", "arn:aws:s3:::project-data/*"]
        }
      ]
    }
    ```
    

---

### 🧠 Why managed policies are useful

- **Reusable** — attach one policy to many users/roles.
    
- **Easier maintenance** — change it once, applies everywhere.
    
- **Best practice** — helps keep your access management consistent.
    
- **Automatic updates** (for AWS-managed ones).
    

---

### ⚙️ Compared to inline policies

|Type|Attached To|Reusability|Managed By|Best For|
|---|---|---|---|---|
|**Managed Policy**|Users, Groups, Roles|Reusable|AWS or You|Shared permissions|
|**Inline Policy**|Single user/group/role|One-time use|You|Unique permissions|

---

✅ **In short:**

> A **managed policy** is a reusable, attachable permission set — created by AWS or by you — that defines what actions users or roles can perform on AWS resources.



An **inline policy** in AWS is a **permission policy that’s embedded directly into a single IAM user, group, or role** — instead of being reusable like a managed policy.

Think of it as a **custom, one-off rule** that belongs **only** to that entity.

---

### 🧩 Example

Let’s say you have a user named **“Kevin”**, and you want only him to have read access to one specific S3 bucket.  
You can attach this **inline policy** directly to Kevin’s IAM user:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::kevin-private-bucket/*"
    }
  ]
}
```

This policy exists **inside Kevin’s user** — it’s not reusable for anyone else.

---

### ⚙️ Key traits

|Feature|Description|
|---|---|
|**Attached to**|One IAM entity (user, group, or role)|
|**Reusability**|❌ Not reusable|
|**Ownership**|Deleted automatically if the user/role is deleted|
|**Control**|You fully manage and edit it manually|
|**Use case**|Unique, special permissions for one entity|

---

### 🧠 Inline vs Managed Policy

|Feature|**Inline Policy**|**Managed Policy**|
|---|---|---|
|**Scope**|Attached to one user/group/role|Can be attached to many|
|**Reusability**|No|Yes|
|**Ownership**|Belongs to the entity|Separate, independent object|
|**Use Case**|Unique access needs|Shared access patterns|

---

✅ **In short:**

> An **inline policy** is a **custom, one-to-one permission policy** written directly into a specific IAM user, group, or role — used when you want **tight, unique control** over that entity’s access.


### Amazon Resource Name (ARN)
---
An **ARN (Amazon Resource Name)** is a **unique identifier** for any AWS resource.  
It tells AWS _exactly which resource_ you’re referring to — like a precise address for a specific item in your AWS account.

---

### 🧩 ARN structure

The general format looks like this:

```
arn:partition:service:region:account-id:resource
```

Example for an S3 bucket:

```
arn:aws:s3:::my-example-bucket
```

---

### 📖 Breakdown of parts

|Part|Description|Example|
|---|---|---|
|**arn**|Literal prefix for all ARNs|`arn`|
|**partition**|AWS environment|`aws` (standard), `aws-cn` (China), `aws-us-gov` (GovCloud)|
|**service**|AWS service name|`s3`, `ec2`, `lambda`|
|**region**|AWS region (some services are global)|`us-east-1`, `eu-west-1`|
|**account-id**|AWS account number (12 digits)|`123456789012`|
|**resource**|Resource type and name|`bucket/my-bucket`, `instance/i-12345`, `function:MyLambda`|

---

### 💡 Examples

|Resource|Example ARN|
|---|---|
|**S3 bucket**|`arn:aws:s3:::my-bucket`|
|**EC2 instance**|`arn:aws:ec2:us-east-1:123456789012:instance/i-0abcd1234efgh5678`|
|**Lambda function**|`arn:aws:lambda:us-east-1:123456789012:function:ProcessData`|
|**IAM user**|`arn:aws:iam::123456789012:user/Kevin`|

---

### 🧠 Why ARNs matter

- Used in **IAM policies** to specify what resources a user or role can access.
    
- Used in **API calls** and **CloudFormation templates**.
    
- Makes automation and permissions **precise and consistent**.
    

---

✅ **In short:**

> An **ARN** is AWS’s way of uniquely identifying any resource — like a full address that includes the service, region, account, and specific resource name.


![[16_IAMGroups.png]]

### IAM Roles
---
An **IAM Role** in AWS is a **set of permissions** that defines **what actions** are allowed or denied on AWS resources — but unlike a user, it **does not belong to a specific person**.

Instead, **roles are meant to be assumed** temporarily by:

- AWS services (like EC2, Lambda, etc.)
    
- Other AWS accounts
    
- Applications
    
- Users (for temporary access)
    

---

### 🧩 Think of it like this:

A **role** is like a **uniform with specific access rights** — whoever wears it gets the permissions it grants.  
When they take it off, the permissions go away.

---

### 🧠 Example use cases

|Use Case|Example|
|---|---|
|**EC2 accessing S3**|An EC2 instance assumes a role to read/write files in an S3 bucket (without storing AWS keys).|
|**Lambda accessing DynamoDB**|A Lambda function uses a role to query a DynamoDB table securely.|
|**Cross-account access**|A user in Account A assumes a role in Account B to perform tasks.|
|**Temporary credentials**|AWS STS (Security Token Service) issues short-lived access tokens via a role.|

---

### ⚙️ Structure of a Role

1. **Trust Policy** – defines _who can assume the role_.  
    Example:
    
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": { "Service": "ec2.amazonaws.com" },
          "Action": "sts:AssumeRole"
        }
      ]
    }
    ```
    
2. **Permission Policy** – defines _what actions_ the role can perform.  
    Example:
    
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": ["s3:GetObject"],
          "Resource": "arn:aws:s3:::my-bucket/*"
        }
      ]
    }
    ```
    

---

### 🔐 Key differences from IAM Users

|Feature|**IAM User**|**IAM Role**|
|---|---|---|
|Identity type|Permanent person/app|Temporary assumed identity|
|Access keys|Has long-term credentials|Uses temporary credentials|
|Ownership|One specific entity|Shared/assumed by many|
|Best for|Human users|AWS services, apps, cross-account access|

---

✅ **In short:**

> An **IAM Role** is a **temporary identity with defined permissions** that AWS services, users, or applications can **assume** to perform specific tasks — securely and without needing permanent credentials.


### Identity Provider /Federation / IAM Identity Center
---
**Federation** in AWS means letting users **from outside AWS** (like from your company’s existing system, Google Workspace, or Microsoft Active Directory) **log in and access AWS** — **without creating separate IAM users** for them.

---

### 🧩 In simple terms:

Federation = **“Bring your own identity”** to AWS.

Instead of managing multiple AWS accounts and passwords, users can use their **existing corporate or third-party credentials** to sign in and get **temporary AWS access**.

---

### ⚙️ How it works

1. A user signs in to their **organization’s identity provider (IdP)** (like Google, Okta, Azure AD, or Active Directory).
    
2. The IdP authenticates the user.
    
3. The IdP tells AWS: “This user is verified.”
    
4. AWS **issues temporary credentials** via **STS (Security Token Service)** that allow access based on an IAM **role**.
    

---

### 🧠 Example

Let’s say your company uses **Microsoft Azure AD**.  
You can:

- Set up **federation** between Azure AD and AWS.
    
- Create an **IAM role** in AWS that trusted users from Azure AD can assume.
    
- When employees log in via the company portal, they automatically get access to AWS — with the permissions defined in that role.
    

---

### 🔐 Benefits

- **No need to create IAM users** for everyone.
    
- **Centralized authentication** (one password system).
    
- **Temporary credentials** → more secure.
    
- Works with **Single Sign-On (SSO)**.
    

---

### 💡 Related AWS services

- **AWS IAM Identity Center (formerly AWS SSO)** – easiest way to set up federation and manage access.
    
- **AWS STS (Security Token Service)** – issues the temporary credentials used in federation.
    

---

✅ **In short:**

> **Federation** allows external users (like employees or partners) to **log in to AWS using their existing identity system**, by temporarily assuming an IAM role — no separate AWS accounts or passwords needed.

![[16_IAMRoles.png]]