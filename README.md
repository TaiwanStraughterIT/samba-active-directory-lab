# Samba Active Directory & User Management Lab

**Project Status: COMPLETED — October 12, 2026**

**Deliverables:** Configured Samba AD domain controller, completed user and security group administration exercises, and prepared an illustrated lab report.

## Overview
Deployed a **Samba Active Directory Domain Controller (AD DC)** on **Debian 13 ARM64** using **UTM on an Apple Silicon Mac**, then practiced entry-level IT support workflows for account and security group administration.

> This is an **Active Directory-compatible Samba lab**, not a Microsoft Windows Server or Active Directory Users and Computers (ADUC) lab. All users are fictional.

## Environment

| Component | Details |
| --- | --- |
| Host | macOS, Apple Silicon |
| Virtualization | UTM |
| Server OS | Debian 13 ARM64 |
| Directory service | Samba AD DC |
| Server hostname | `dc01` |
| Domain | `corp.example.test` |
| Kerberos realm | `CORP.EXAMPLE.TEST` |
| NetBIOS domain | `CORP` |
| Test users | `jsmith`, `sjohnson` |
| Security groups | `IT-Support`, `HR-Department` |

## Objectives
- Configure and verify an Active Directory-compatible domain controller.
- Onboard fictional employee accounts and inspect directory users.
- Practice a password reset and disabling/re-enabling an account.
- Create department security groups and verify membership.
- Run a directory database consistency check and document results.

## Implementation and verification

### 1. Domain controller configuration
Installed Samba/Kerberos components, provisioned the domain, enabled and started `samba-ad-dc`, and checked service and domain details.

```bash
systemctl status samba-ad-dc
samba-tool domain info 127.0.0.1
```

### 2. User account management
Created `jsmith` and `sjohnson`, verified the directory user list, performed a password reset, and demonstrated disabling and re-enabling `jsmith`.

```bash
samba-tool user create jsmith
samba-tool user list
samba-tool user setpassword jsmith
samba-tool user disable jsmith
samba-tool user show jsmith
samba-tool user enable jsmith
samba-tool user show jsmith
samba-tool user create sjohnson
```

### 3. Group administration
Created departmental groups and assigned fictional users.

```bash
samba-tool group add IT-Support
samba-tool group addmembers IT-Support jsmith
samba-tool group listmembers IT-Support
samba-tool group add HR-Department
samba-tool group addmembers HR-Department sjohnson
samba-tool group listmembers HR-Department
```

Group membership alone does not grant permissions to a file share or other resource.

### 4. Database verification

```bash
samba-tool dbcheck
```

This checks directory database consistency, not complete DNS, Kerberos, or client-join functionality.

## Evidence
The completed Word report, **[Samba_Active_Directory_Lab_Report.docx](Samba_Active_Directory_Lab_Report.docx)**, documents the lab with 11 labeled screenshots and explanations. The report is the final evidence deliverable for this project.

## Skills demonstrated
- Virtual machine and Linux server setup
- Samba AD DC provisioning and service verification
- Employee account onboarding and password reset
- Account enable/disable lifecycle tasks
- Security group creation and membership verification
- Technical documentation and evidence collection

## Final project outcomes
- Provisioned and verified `corp.example.test` on the Debian Samba AD DC.
- Practiced creating two fictional user accounts and managing password and account status.
- Created `IT-Support` and `HR-Department` groups and assigned their respective users.
- Documented the directory database check and other key steps in the lab report.
- Completed the hands-on exercises and project documentation.

## Optional future extensions
- Verify DNS SRV records and Kerberos ticket issuance.
- Join a compatible client to the domain.
- Configure resource permissions and test group-based access.

## Scope and security
Local educational lab only. No production credentials or real employee information are used.
