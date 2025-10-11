
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