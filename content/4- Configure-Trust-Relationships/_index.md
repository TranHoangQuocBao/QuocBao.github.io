| title       | date       | weight | chapter | prev |
|-------------|------------|--------|---------|------|
| Preparation | 2025-08-11 | 2      | false   | 1.   |
---
Step 2 – Configure Trust Relationships
---

## Overview
In this step, we will establish **trust relationships** between AWS Managed Microsoft AD and your existing on-premises Active Directory. This enables seamless authentication, resource sharing, and Single Sign-On (SSO) across environments.

## Objectives
- Enable secure user authentication between AWS and on-prem AD.
- Allow users to access AWS resources using existing credentials.
- Facilitate hybrid identity management.

## Prerequisites
Before configuring trust relationships, ensure that:
- AWS Managed Microsoft AD has been successfully created in Step 1.
- You have administrative credentials for both AWS Managed AD and your on-prem AD.
- Network connectivity (VPC peering or VPN/Direct Connect) between AWS and on-premises is established.
- Required ports for Active Directory trust (e.g., TCP/UDP 88, 389, 445, etc.) are open.

## Procedure

### 1. Access AWS Directory Service
1. Sign in to the AWS Management Console.
2. Navigate to **Directory Service** → select your AWS Managed Microsoft AD.
![Configure Trust Relationships](D:\workshop\static\images\1\01.png)

### 2. Create Trust Relationship
1. In the AD console, choose **Networking & security** → **Trust relationships**.
![Configure Trust Relationships](D:\workshop\static\images\1\02.png)

2. Click **Add trust**.
![Configure Trust Relationships](D:\workshop\static\images\1\03.png)

3. Select the trust direction:
   - **One-way incoming** – On-prem AD trusts AWS Managed AD.
   - **One-way outgoing** – AWS Managed AD trusts on-prem AD.
   - **Two-way** – Both directories trust each other.
4. Choose **Forest trust** type for cross-domain authentication.
![Configure Trust Relationships](D:\workshop\static\images\1\04.png)

### 3. Configure Trust Settings
![Configure Trust Relationships](D:\workshop\static\images\1\04.png)
- Enter the **Fully Qualified Domain Name (FQDN)** of the trusted domain.
- Set trust password (must be the same on both sides).
- Enable **Selective authentication** for better security, or **Forest-wide authentication** for ease of access.

### 4. Confirm and Validate Trust
![Configure Trust Relationships](D:\workshop\static\images\1\05.png)
- Click **Create** and wait for trust creation.
- From the on-prem AD, configure the corresponding trust using Active Directory Domains and Trusts.
- Validate the trust from both sides to ensure connectivity.

## Best Practices
- Use **two-way trust** for seamless integration unless security policy dictates otherwise.
- Apply **conditional access policies** to limit access based on user groups.
- Monitor trust health regularly using AWS Directory Service logs and CloudWatch.

## Outcome
At the end of this step, AWS Managed Microsoft AD and your on-premises AD will be securely connected, allowing authenticated resource sharing across environments.
