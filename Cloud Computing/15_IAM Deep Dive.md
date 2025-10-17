
IAM is used for security purpose.
With IAM, you can control AWS resources centrally.
Root user gives full permissions.
IAM User has Limited permissions
IAM is free and Global.
For IAM users, we can anytime attach and detach permissions/policies.
It's not recommended to use ROOT account for daily activities or work, instead use IAM user. 
MFA --> Multi-factor Authentication
MFA is highly recommended for ROOT and IAM account as well.
We need to setup MFA for every individual IAM user.

There are two ways to access AWS
- AWS console Website (GUI). Using Root and IAM user.
- Programmatic access. (CLI, SDKs, Developer tools). We login using  KEYs, (Access key and Secret Key)

![[15_IAM.png]]


You can access **AWS** in several ways — depending on what you want to do (manage services, code, automate, etc.). Here’s a clear breakdown 👇

---

### 🖥️ 1. **AWS Management Console**

- The **web interface** for managing all AWS services.
    
- URL: **[https://aws.amazon.com/console/](https://aws.amazon.com/console/)**
    
- You log in with your **root account** or **IAM user credentials**.
    
- Best for: beginners, visual management, quick tasks.
    

🪄 Example: Launch an EC2 instance, create an S3 bucket, or view CloudWatch metrics.

---

### 💻 2. **AWS CLI (Command Line Interface)**

- Tool to manage AWS from your terminal or PowerShell.
    
- Install from: [https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)
    
- Configure it using:
    
    ```bash
    aws configure
    ```
    
    Then enter your:
    
    - Access key ID
        
    - Secret access key
        
    - Default region
        
    - Output format (e.g., json)
        

🪄 Example:

```bash
aws s3 ls
aws ec2 describe-instances
```

---

### 💾 3. **AWS SDKs (Software Development Kits)**

- Lets you use AWS **in your code**.
    
- Available for: Python (`boto3`), JavaScript (`aws-sdk`), Java, Go, etc.
    

🪄 Example (Python):

```python
import boto3

s3 = boto3.client("s3")
for bucket in s3.list_buckets()["Buckets"]:
    print(bucket["Name"])
```

---

### 🤖 4. **AWS CloudShell**

- A **browser-based terminal** built right into the AWS Console.
    
- No setup needed — it already has the AWS CLI and SDKs preinstalled.
    
- Great for quick automation or testing CLI commands.
    

---

### 🧱 5. **AWS Mobile or Desktop Apps**

- **AWS Console Mobile App** (iOS/Android) lets you monitor and manage resources on the go.
    
- Limited functionality but great for monitoring or stopping instances quickly.
    

---

✅ **Summary Table**

|Method|Best For|Access Type|
|---|---|---|
|**AWS Console**|Visual management|Browser|
|**AWS CLI**|Automation, scripting|Terminal|
|**AWS SDKs**|Programming with AWS|Code|
|**CloudShell**|Quick in-console commands|Browser shell|
|**Mobile App**|Monitoring|Mobile device|

---
