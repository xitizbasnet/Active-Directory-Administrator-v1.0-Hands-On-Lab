# Lab 1.3: Domain Controller Health Check

## Overview

**Objective:** Monitor and verify domain controller health.

**Estimated Time:** 20 minutes

---

## Lab Procedure

### Step 1 – Open Active Directory Sites and Services

1. Open **Server Manager**.
2. Navigate to **Tools**.
3. Select **Active Directory Sites and Services**.

---

### Step 2 – Check Replication Status

1. Expand your Active Directory domain.
2. Right-click the appropriate **Connection Objects**.
3. Select the option to check replication.

---

### Step 3 – Run a Replication Diagnostic

Open **Command Prompt** as **Administrator**, then run:

```cmd
repadmin /replicate
```

---

### Step 4 – Check SYSVOL Replication

Run the following command:

```cmd
repadmin /showvector DC=yourdomain,DC=com
```

Review the output for replication status and synchronization information.

---

### Step 5 – Monitor Event Viewer

Navigate to:

* **Event Viewer**

  * **Windows Logs**

    * **System**
    * **Directory Service**

Review the logs for warnings, errors, or replication-related events.

---

### Step 6 – Check FSMO Roles

Open **Command Prompt** and run:

```cmd
netdom query fsmo
```

Verify that all **Flexible Single Master Operations (FSMO)** roles are assigned correctly.

---

### Step 7 – Verify DNS SRV Records

1. Open **DNS Manager**.
2. Verify that the required **Active Directory SRV records** are present and correctly registered.

---

### Step 8 – Test Domain Controller Connectivity

Run a comprehensive diagnostic using:

```cmd
dcdiag /v
```

Review the output for any failures or warnings requiring attention.

---

### Step 9 – Review DCPROMO Logs

Check the following log file for installation or promotion-related issues:

```text
C:\Windows\System32\debug\dcpromo.log
```

---

### Step 10 – Document Findings

Create a health check report that includes the current status of:

* Replication health
* SYSVOL replication
* Event log review
* FSMO role assignments
* DNS SRV records
* Domain controller diagnostics
* Overall health assessment

---

## Best Practice

> [!TIP]
> Perform domain controller health checks on a weekly basis.

> [!TIP]
> Establish baseline metrics for the following to help identify performance degradation or operational issues over time:

* Replication latency
* User logon time
* Event log health
* Domain controller diagnostics
* DNS service health

> [!IMPORTANT]
> Consistent health monitoring helps identify replication, DNS, and authentication issues before they impact production services.
