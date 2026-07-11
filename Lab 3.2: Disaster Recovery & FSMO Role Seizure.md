# Lab 3.2: Disaster Recovery & FSMO Role Seizure

## Overview

**Objective:** Develop and execute disaster recovery procedures.

**Estimated Time:** 75 minutes

---

## Scenario

Your **Primary Domain Controller (PDC) Emulator** domain controller has failed catastrophically. You must seize the required **Flexible Single Master Operations (FSMO)** roles to another healthy domain controller and recover the Active Directory domain.

> [!IMPORTANT]
> This lab simulates a disaster recovery scenario involving the permanent loss of a domain controller that owns one or more FSMO roles.

---

## Challenge Tasks

### 1. Diagnose FSMO Role Holder Status

Determine the current FSMO role holders by running:

```cmd
netdom query fsmo
```

Document the current role assignments.

---

### 2. Verify the Failed Domain Controller Is Not Recoverable

Confirm that the failed domain controller cannot be recovered.

Document all troubleshooting and recovery attempts before proceeding with FSMO role seizure.

> [!CAUTION]
> FSMO role seizure should only be considered after confirming that the original role holder cannot be returned to service.

---

### 3. Identify a Healthy Domain Controller

Select a healthy domain controller that will assume the FSMO roles.

Verify that the selected server:

* Is online.
* Has healthy Active Directory replication.
* Is functioning correctly.
* Meets organizational requirements for FSMO role ownership.

---

### 4. Seize the PDC Emulator Role

Using **ntdsutil** on the healthy domain controller, seize the **PDC Emulator** role.

```text
ntdsutil
roles
seize pdc
```

---

### 5. Seize the RID Master Role

Using **ntdsutil**, seize the **RID Master** role.

```text
ntdsutil
roles
seize rid master
```

---

### 6. Seize the Infrastructure Master Role

Using **ntdsutil**, seize the **Infrastructure Master** role.

```text
ntdsutil
roles
seize infrastructure master
```

---

### 7. Seize the Schema Master Role (Rare)

If required, use **ntdsutil** to seize the **Schema Master** role.

```text
ntdsutil
roles
seize schema master
```

> [!NOTE]
> Seizing the **Schema Master** role is uncommon and should only be performed when absolutely necessary.

---

### 8. Verify FSMO Role Seizure

Confirm that all required FSMO roles have been successfully transferred to the new domain controller.

Verify the updated role ownership using:

```cmd
netdom query fsmo
```

---

### 9. Check Domain Functionality

Run domain controller diagnostics on all remaining domain controllers.

```cmd
dcdiag
```

Verify that:

* Active Directory services are functioning correctly.
* Replication is healthy.
* Authentication services operate normally.

---

### 10. Implement the Recovery Plan

Depending on the recovery strategy:

* Restore the failed domain controller.
* Decommission the failed domain controller if recovery is not possible.

Document the chosen recovery approach.

---

### 11. Document the Root Cause Analysis (RCA)

Prepare a **Root Cause Analysis (RCA)** that includes:

* Failure timeline
* Root cause
* Impact assessment
* Recovery actions
* Lessons learned
* Preventive recommendations

---

### 12. Create Proactive Monitoring

Implement monitoring for FSMO role health and availability.

Monitoring should include:

* FSMO role ownership
* Domain controller health
* Replication status
* Critical Active Directory services
* Alerting for role or service failures

---

## Validation Checklist

Verify the following before completing the lab:

* ✅ FSMO role ownership identified.
* ✅ Failed domain controller confirmed unrecoverable.
* ✅ Healthy replacement domain controller selected.
* ✅ PDC Emulator role seized successfully.
* ✅ RID Master role seized successfully.
* ✅ Infrastructure Master role seized successfully.
* ✅ Schema Master role seized (if required).
* ✅ FSMO role ownership verified.
* ✅ Domain functionality validated using **dcdiag**.
* ✅ Recovery plan implemented.
* ✅ Root Cause Analysis documented.
* ✅ FSMO monitoring configured.

---

## Critical Warning

> [!WARNING]
> FSMO role seizure should only be performed when the current role holder is **permanently unavailable**. If the original domain controller is brought back online after a role seizure without proper cleanup, serious Active Directory inconsistencies can occur.

> [!IMPORTANT]
> Document every action performed during disaster recovery, including diagnostics, decisions, FSMO role changes, recovery activities, and post-recovery validation. Comprehensive documentation is essential for auditing, compliance, and future incident response.
