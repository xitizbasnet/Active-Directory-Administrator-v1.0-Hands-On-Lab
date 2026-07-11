# Reference & Tools

## Overview

This section provides commonly used **PowerShell cmdlets**, **diagnostic commands**, and **network port references** for Active Directory administration and troubleshooting.

> [!TIP]
> Keep this section readily available during lab exercises and production troubleshooting. Many of these commands are frequently used by Active Directory administrators.

---

# Essential PowerShell Commands

## List All Users

Retrieves all Active Directory user accounts.

```powershell
Get-ADUser -Filter * | Select SamAccountName
```

---

## Create a User

Creates a new Active Directory user in the specified Organizational Unit (OU).

```powershell
New-ADUser -Name 'John Doe' -Path 'OU=Users,DC=yourdomain,DC=com'
```

---

## Reset a User Password

Resets the password for the specified Active Directory user.

```powershell
Set-ADUser -Identity username -AccountPassword (ConvertTo-SecureString 'P@ssw0rd!')
```

---

## List Group Members

Displays the members of an Active Directory security group.

```powershell
Get-ADGroupMember -Identity 'GroupName'
```

---

## Add Members to a Group

Adds one or more users to an Active Directory security group.

```powershell
Add-ADGroupMember -Identity 'GroupName' -Members user1, user2
```

---

## Check Replication Metadata

Displays replication partner metadata for a domain controller.

```powershell
Get-ADReplicationPartnerMetadata -Target DC1
```

---

## Force a Group Policy Update

Forces an immediate Group Policy update on a remote computer.

```powershell
Invoke-GPUpdate -Computer ComputerName -Force
```

---

## List All Organizational Units (OUs)

Displays all Organizational Units within the Active Directory environment.

```powershell
Get-ADOrganizationalUnit -Filter * | Select Name, Path
```

---

# Diagnostic Tools & Commands

The following commands are commonly used for troubleshooting and validating Active Directory services.

| Command                          | Description                                  |
| -------------------------------- | -------------------------------------------- |
| `dcdiag /v`                      | Comprehensive domain controller diagnostics  |
| `repadmin /replicate`            | Force replication between domain controllers |
| `repadmin /showrepl`             | Display Active Directory replication status  |
| `netdom query fsmo`              | Display FSMO role holders                    |
| `gpresult /h report.html`        | Generate a Group Policy Results report       |
| `gpupdate /force`                | Force an immediate Group Policy update       |
| `nltest /dsgetdc:yourdomain.com` | Test domain controller connectivity          |
| `klist`                          | Display Kerberos tickets                     |
| `adsi edit.msc`                  | Direct Active Directory schema modification  |

> [!WARNING]
> **ADSI Edit** provides direct access to the Active Directory database. Incorrect modifications can cause significant issues within the directory service. Use this tool only when necessary and with appropriate authorization.

---

# Useful Ports & Services

The following network ports are commonly used by Active Directory services.

|          Port | Service        | Purpose                |
| ------------: | -------------- | ---------------------- |
|        **53** | DNS            | Domain Name Service    |
|        **88** | Kerberos       | Authentication         |
|       **135** | RPC Mapper     | Remote Procedure Call  |
|       **389** | LDAP           | Directory Access       |
|       **636** | LDAPS          | Secure LDAP            |
| **3268–3269** | Global Catalog | Forest-wide search     |
|       **445** | SMB/CIFS       | File and Print Sharing |

> [!IMPORTANT]
> Ensure that required Active Directory ports are permitted through host-based and network firewalls to support authentication, replication, DNS resolution, Group Policy processing, and directory services.

---

## Quick Reference Checklist

Use the following checklist during routine administration and troubleshooting:

* ✅ Verify domain controller health using **dcdiag**.
* ✅ Check replication status with **repadmin**.
* ✅ Confirm FSMO role ownership using **netdom**.
* ✅ Validate Group Policy application with **gpresult**.
* ✅ Refresh policies using **gpupdate**.
* ✅ Test domain controller discovery with **nltest**.
* ✅ Review Kerberos tickets using **klist**.
* ✅ Audit Active Directory objects using the **ActiveDirectory PowerShell module**.

> [!TIP]
> Combine these PowerShell cmdlets and diagnostic tools with regular health checks, monitoring, and documentation to maintain a secure, reliable, and well-managed Active Directory environment.
