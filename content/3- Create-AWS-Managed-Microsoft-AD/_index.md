
| title       | date       | weight | chapter | prev |
|-------------|------------|--------|---------|------|
| Preparation | 2025-08-11 | 1      | false   | 1.   |

---
Step 1 - Create AWS Managed Microsoft AD
---

## Objective
In this step, you will create a new AWS Managed Microsoft Active Directory (AD) in your AWS account using the AWS Directory Service.

## Prerequisites
- An AWS account with sufficient permissions (AdministratorAccess recommended).
- A configured **VPC** with at least two private subnets in different Availability Zones.

## Steps
1. **Open the AWS Management Console** and navigate to **Directory Service**.

2. Click **Set up directory**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh1.png)

3. Select **AWS Managed Microsoft AD** and click **Next**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh2.png)

4. Choose the **Edition**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh3.png)
   - **Standard Edition**: Up to 30,000 objects, suitable for smaller environments.
   - **Enterprise Edition**: Up to 500,000 objects, suitable for large organizations.

5. Fill in **Directory details**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh4.png)
   - **Directory DNS name**: e.g., `corp.example.com`
   - **Directory NetBIOS name**: e.g., `CORP`
   - **Admin password**: Must meet complexity requirements.

6. **VPC Settings**:
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh5.png)
   - Choose your **VPC**.
   - Select **two subnets** in different Availability Zones.

7. Review all settings and click **Create directory**.
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh6.png)

8. Wait for the **Active** status (about 20–45 minutes).
![AWS Managed AD Step 1](D:\workshop\static\images\01\anh7.png)

## Expected Outcome
An AWS Managed Microsoft AD instance is provisioned, accessible within your VPC, and ready for further configuration.
