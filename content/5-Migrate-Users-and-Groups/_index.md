| title                      | date       | weight | chapter | prev |
|----------------------------|------------|--------|---------|------|
| Migrate-Users-and-Groups   | 2025-08-11 | 3      | false   | 1.   |
---
Step 3 - Migrate Users and Groups
---

## Objective
This step focuses on migrating existing on-premises Active Directory users and groups into AWS Managed Microsoft AD.  
The migration ensures that all identity objects are transferred accurately while maintaining group memberships, access rights, and password policies.

---

## Prerequisites
Before starting the migration process:
- AWS Managed Microsoft AD is deployed and reachable from the on-premises environment.
- Trust relationship between AWS Managed Microsoft AD and on-premises AD is configured and validated.
- Required migration tools installed, such as:
  - **Active Directory Migration Tool (ADMT)**.
  - **Password Export Server (PES)** if migrating passwords.
- Administrative credentials for both source (on-prem) and target (AWS AD) domains.

---

## Migration Process

### 1. Install and Configure ADMT
- Deploy ADMT on a Windows Server that is a member of the target AWS Managed AD domain.
- Ensure that the ADMT server can communicate with both domains.
- If migrating passwords, install **PES** on a domain controller in the source domain and configure encryption keys.

### 2. Plan the Migration
- Identify Organizational Units (OUs) to migrate.
- Create a migration batch plan:
  - Critical accounts first (administrators, service accounts).
  - Regular users.
  - Security and distribution groups.

### 3. Migrate User Accounts
- Use ADMT **User Account Migration Wizard** to:
  - Select source and target domains.
  - Choose accounts to migrate.
  - Enable “Migrate associated user groups”.
  - Optionally migrate passwords (requires PES).
- Validate migration logs to ensure no errors.

### 4. Migrate Groups
- Use ADMT **Group Migration Wizard** to:
  - Preserve group scope (Global, Universal, Domain Local).
  - Maintain group membership integrity.

### 5. Post-Migration Validation
- Log in with migrated accounts to confirm authentication in AWS AD.
- Verify that permissions and group memberships remain intact.
- Update any applications or services to use AWS Managed Microsoft AD.

---

## Best Practices
- Perform a **pilot migration** before full production migration.
- Take backups of both AD environments before starting.
- Schedule migrations during low-traffic hours.
- Document every migrated object for audit and rollback purposes.
