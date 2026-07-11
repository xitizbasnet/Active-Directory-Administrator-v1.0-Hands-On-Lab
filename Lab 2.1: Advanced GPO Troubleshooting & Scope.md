# Lab 2.1: Advanced GPO Troubleshooting & Scope

## Overview

**Objective:** Diagnose GPO application failures and implement Security Group Filtering.

**Estimated Time:** 45 minutes

---

## Scenario

A **Group Policy Object (GPO)** for **Windows Firewall** is not applying to certain computers. Investigate the root cause of the issue and implement a solution using **Security Group Filtering**.

> [!NOTE]
> This lab focuses on troubleshooting Group Policy processing, validating policy scope, and using security group filtering to target specific computers.

---

## Lab Procedure

### Step 1 – Collect Affected Computer Information

1. Collect the names of the affected computers.
2. Verify that each computer is joined to the correct Active Directory domain.

---

### Step 2 – Generate a Group Policy Results Report

On each affected computer, open **Command Prompt** and run:

```cmd
gpresult /h report.html
```

Review the generated report for policy processing details.

---

### Step 3 – Analyze Applied Group Policy Objects

Open the generated **report.html** file and verify whether the target GPO appears under:

* **Applied Group Policy Objects**

If the GPO is missing, continue to the next step.

---

### Step 4 – Refresh Group Policy

On the affected computer, run:

```cmd
gpupdate /force
```

Allow the policy refresh to complete successfully.

---

### Step 5 – Use Resultant Set of Policy (RSoP)

Launch the **Resultant Set of Policy (RSoP)** tool:

```text
rsop.msc
```

Use the results to visualize which policies have been applied and identify any processing issues.

---

### Step 6 – Verify the Organizational Unit (OU)

Review the Active Directory structure and confirm that:

* The affected computers are located in the correct **Organizational Unit (OU)**.
* The GPO is linked to the appropriate OU.

---

### Step 7 – Review the GPO Scope

Within **Group Policy Management Console (GPMC)**:

1. Open the target GPO.
2. Select the **Scope** tab.
3. Review the **Security Group Filtering** configuration.

---

### Step 8 – Create a Security Group

Create a security group for the targeted computers.

Example:

```text
Firewall-Policy-Users
```

Add the appropriate computer accounts to this group.

---

### Step 9 – Configure GPO Permissions

Edit the GPO permissions and:

* Add the newly created security group.
* Grant the **Apply Group Policy** permission.

---

### Step 10 – Modify Default Apply Permissions (If Required)

If appropriate for your environment:

* Remove **Authenticated Users** from the **Apply Group Policy** permissions.

> [!CAUTION]
> Before removing **Authenticated Users**, ensure the replacement security group contains all intended target computers. Incorrect filtering can prevent the GPO from applying.

---

### Step 11 – Verify GPO Application

Run the following command again on an affected computer:

```cmd
gpresult /h report.html
```

Confirm that the target GPO now appears under **Applied Group Policy Objects**.

---

### Step 12 – Validate Windows Firewall Policy

Use **Group Policy Results** to verify that the Windows Firewall rules are now being enforced through the applied Group Policy.

---

## Validation Checklist

Verify the following before completing the lab:

* ✅ Computers are members of the correct Active Directory domain.
* ✅ Computers reside in the correct Organizational Unit (OU).
* ✅ The GPO is linked to the target OU.
* ✅ Security Group Filtering is configured correctly.
* ✅ The target security group has the **Apply Group Policy** permission.
* ✅ The GPO appears under **Applied Group Policy Objects**.
* ✅ Windows Firewall settings are enforced successfully.

---

## Troubleshooting Tip

> [!TIP]
> Use **Event Viewer** on the domain controller to monitor **Group Policy processing** events.

> [!TIP]
> Enable **verbose Group Policy logging** to obtain detailed diagnostic information when troubleshooting complex policy application issues.
