# Lab 2.3: Replication Monitoring & Issue Resolution

## Overview

**Objective:** Monitor Active Directory replication and resolve replication failures.

**Estimated Time:** 55 minutes

---

## Scenario

Replication is failing between domain controllers. Diagnose the root cause of the replication issue and implement the appropriate resolution.

> [!NOTE]
> This lab focuses on monitoring Active Directory replication, identifying replication failures, validating network and DNS dependencies, and restoring replication between domain controllers.

---

## Lab Procedure

### Step 1 – Open the Repadmin Tool

On **DC1**:

1. Open **Command Prompt** as **Administrator**.

---

### Step 2 – Check Replication Status

Run the following command to generate a replication status report:

```cmd
repadmin /showrepl * /csv > repl.csv
```

Review the generated **repl.csv** file.

---

### Step 3 – Analyze the Replication Report

Review the CSV report and identify any replication failures.

Look for:

* Red **X** indicators
* Failed replication attempts
* Replication error messages
* Affected naming contexts

---

### Step 4 – Identify the Failing Domain Controller and Partition

Run the following command to identify the affected replication partner and directory partition:

```cmd
repadmin /replicate DC2 DC1 "CN=Configuration,DC=yourdomain,DC=com"
```

Determine:

* The failing domain controller
* The affected directory partition
* The reported replication error

---

### Step 5 – Verify Network Connectivity

Confirm network communication between the domain controllers.

Verify connectivity for the following ports:

| Port | Service                 |
| ---: | ----------------------- |
|  135 | RPC                     |
|  139 | NetBIOS Session Service |
|  389 | LDAP                    |
|  445 | SMB                     |

---

### Step 6 – Verify DNS Resolution

From **DC1**, run:

```cmd
nslookup DC2.yourdomain.com
```

Confirm that the hostname resolves to the correct IP address.

---

### Step 7 – Review Event Logs

Navigate to:

* **Event Viewer**

  * **Directory Service Logs**

Review the logs for replication, DNS, authentication, or connectivity-related errors.

---

### Step 8 – Rebuild the Knowledge Consistency Checker (KCC)

If a **KCC** error is detected, run:

```cmd
repadmin /kcc DC1
```

Allow the Knowledge Consistency Checker to regenerate the replication topology.

---

### Step 9 – Force Immediate Replication

Run:

```cmd
repadmin /replicate
```

Verify that replication completes successfully.

---

### Step 10 – Synchronize All Replication Partners

Run:

```cmd
repadmin /syncall
```

Monitor the output for successful synchronization or remaining errors.

---

### Step 11 – Verify FSMO Role Ownership

Run:

```cmd
netdom query fsmo
```

Confirm that all **Flexible Single Master Operations (FSMO)** roles are assigned correctly.

---

### Step 12 – Create a Replication Monitoring Script

Develop a monitoring script that regularly tracks Active Directory replication health and reports failures for proactive administration.

> [!TIP]
> Automating replication monitoring helps identify issues before they affect authentication, directory consistency, or domain services.

---

## Validation Checklist

Verify the following before completing the lab:

* ✅ Replication status report generated successfully.
* ✅ Replication failures identified and analyzed.
* ✅ Network connectivity verified between domain controllers.
* ✅ DNS name resolution validated.
* ✅ Directory Service event logs reviewed.
* ✅ KCC topology regenerated (if required).
* ✅ Replication completed successfully after remediation.
* ✅ All replication partners synchronized.
* ✅ FSMO role ownership verified.
* ✅ Replication monitoring script created.

---

## Critical Information

> [!IMPORTANT]
> Replication failures can cause authentication issues, inconsistent directory data, and service disruptions across the Active Directory environment.

> [!WARNING]
> Prioritize the resolution of replication failures as soon as they are detected to minimize operational impact.

> [!TIP]
> Maintain a documented recovery procedure for Active Directory replication issues, including replication diagnostics, DNS validation, network verification, FSMO role checks, and recovery steps to support rapid incident response.
