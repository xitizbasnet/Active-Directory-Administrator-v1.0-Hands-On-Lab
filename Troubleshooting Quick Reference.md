# Troubleshooting Quick Reference

## Overview

This quick reference guide provides common Active Directory troubleshooting procedures for frequently encountered operational issues.

Use these troubleshooting workflows to identify, diagnose, and resolve:

* Domain logon failures
* Group Policy processing issues
* Active Directory replication failures
* Slow domain logon performance

> [!TIP]
> Follow the troubleshooting steps in sequence. Validate each dependency before moving to the next step to isolate the root cause efficiently.

---

# Issue: Users Cannot Log On to Domain

## Symptoms

Users are unable to authenticate or log on to the Active Directory domain.

---

## Troubleshooting Steps

### 1. Verify Network Connectivity

Test connectivity to the domain controller IP address.

```cmd
ping <domain-controller-IP>
```

---

### 2. Check DNS Resolution

Verify that the domain name resolves correctly.

```cmd
nslookup yourdomain.com
```

---

### 3. Check Domain Controller Connectivity

Verify that the client can locate a domain controller.

```cmd
nltest /dsgetdc:yourdomain.com
```

---

### 4. Verify Kerberos Authentication

Check available Kerberos tickets.

```cmd
klist
```

---

### 5. Check Time Synchronization

Verify system time synchronization status.

```cmd
w32tm /query /status
```

> [!IMPORTANT]
> Kerberos authentication requires accurate time synchronization between clients and domain controllers.

---

### 6. Review Domain Controller Event Logs

Review **Event Viewer** on the domain controller for authentication-related errors.

Check:

* Security logs
* System logs
* Directory Service logs

---

# Issue: GPO Not Applying to Users or Computers

## Symptoms

Users or computers are not receiving expected Group Policy settings.

---

## Troubleshooting Steps

### 1. Generate Group Policy Results Report

Run:

```cmd
gpresult /h report.html
```

Review:

* Applied Group Policy Objects
* Denied Group Policy Objects
* Policy processing errors

---

### 2. Verify OU Placement

Confirm that the user or computer object exists in the correct Organizational Unit (OU).

---

### 3. Check Group Policy Inheritance

Verify that:

* **Block Inheritance** is not enabled.
* Required parent policies are being inherited correctly.

---

### 4. Verify Apply Group Policy Permission

Confirm that the appropriate user or security group has:

```text
Apply Group Policy
```

permission.

---

### 5. Force Group Policy Update

Run:

```cmd
gpupdate /force /logoff
```

---

### 6. Check for Conflicting GPOs

Review Group Policy priority and identify conflicting GPOs with higher precedence.

---

# Issue: Replication Failures Between Domain Controllers

## Symptoms

Active Directory replication failures occur between domain controllers.

---

## Troubleshooting Steps

### 1. Identify Replication Failures

Run:

```cmd
repadmin /showrepl
```

Review failed replication attempts and error messages.

---

### 2. Verify Network Connectivity

Confirm communication between domain controllers.

Check:

* Network connectivity
* Firewall rules
* Required Active Directory ports

---

### 3. Verify DNS Resolution

Confirm that domain controllers can resolve each other's hostnames correctly.

---

### 4. Test RPC Connectivity

Run:

```powershell
Test-NetConnection -ComputerName DC2 -Port 135
```

Verify RPC communication is available.

---

### 5. Review Event Logs

Review event logs on both domain controllers.

Check:

* Directory Service logs
* System logs
* DNS-related events

---

### 6. Force Replication

Run:

```cmd
repadmin /replicate
```

Verify that replication completes successfully.

---

# Issue: Slow Domain Logons

## Symptoms

Users experience extended wait times during domain authentication and logon processing.

---

## Troubleshooting Steps

### 1. Check Domain Controller Response Time

Run:

```cmd
dcdiag /v
```

Review domain controller health and performance information.

---

### 2. Analyze Logon Performance

Review:

**Event Viewer → Security → Logon Events**

Analyze authentication timing and related events.

---

### 3. Check Network Latency

Run:

```cmd
ping -w 100 <domain-controller>
```

Review response times between client systems and domain controllers.

---

### 4. Review Group Policy Processing Time

Analyze Group Policy processing duration in Event Viewer logs.

---

### 5. Review Number of Applied GPOs

Check the number of applied Group Policy Objects.

> [!WARNING]
> A large number of GPOs (more than 50) may negatively impact logon performance and should be reviewed.

---

### 6. Verify Group Membership Count

Confirm that users are not members of excessive numbers of groups.

Recommended:

```text
Less than 100 group memberships
```

---

# Quick Troubleshooting Checklist

| Issue                 | Primary Tools                                  |
| --------------------- | ---------------------------------------------- |
| Domain logon failures | `ping`, `nslookup`, `nltest`, `klist`, `w32tm` |
| GPO processing issues | `gpresult`, `gpupdate`, GPMC                   |
| Replication failures  | `repadmin`, Event Viewer, DNS tools            |
| Slow logons           | `dcdiag`, Event Viewer, GPO analysis           |

> [!TIP]
> Always document troubleshooting findings, commands executed, errors identified, and remediation steps for future reference and operational knowledge sharing.
