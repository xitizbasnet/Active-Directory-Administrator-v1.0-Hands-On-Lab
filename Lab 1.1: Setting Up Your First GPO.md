# Lab 1.1: Setting Up Your First GPO

## Overview

**Objective:** Create and link a basic Group Policy Object (GPO)

**Estimated Time:** 30 minutes

---

## Prerequisites

Before you begin, ensure the following requirements are met:

* 3 Active Directory domain with at least 1 domain controller
* 3 Domain admin credentials
* 3 Windows Server with GPMC installed

> [!IMPORTANT]
> Ensure you have sufficient permissions to create, edit, and link Group Policy Objects within the target Active Directory domain.

---

## Lab Procedure

### Step 1 – Open Group Policy Management Console (GPMC)

1. Press **Win + R**.
2. Type:

```text
gpmc.msc
```

3. Click **OK**.

---

### Step 2 – Expand Your Domain

1. In **Group Policy Management Console (GPMC)**, expand your Active Directory domain.
2. Right-click **Group Policy Objects**.
3. View the current domain controller.

---

### Step 3 – Create a New GPO

1. Right-click **Group Policy Objects**.
2. Select **New**.
3. Name the Group Policy Object:

```text
L1-PasswordPolicy
```

---

### Step 4 – Edit the GPO

1. Right-click the newly created GPO.
2. Select **Edit**.

---

### Step 5 – Navigate to the Password Policy

Navigate to the following path:

```text
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Password Policy
```

---

### Step 6 – Configure Password Settings

Configure the following policy settings:

| Policy                                     | Value         |
| ------------------------------------------ | ------------- |
| Minimum password length                    | 12 characters |
| Password must meet complexity requirements | Enabled       |

---

### Step 7 – Link the GPO to an Organizational Unit (OU)

1. Return to **Group Policy Management Console (GPMC)**.
2. Right-click the target **Organizational Unit (OU)**.
3. Select **Link an Existing GPO**.
4. Choose:

```text
L1-PasswordPolicy
```

---

### Step 8 – Verify the Link

Confirm that:

* The GPO appears under the target OU.
* The GPO displays the green link icon, indicating that it is successfully linked.

---

### Step 9 – Force a Group Policy Update

On a domain-joined computer:

1. Open **Command Prompt** as **Administrator**.
2. Run:

```cmd
gpupdate /force
```

---

### Step 10 – Verify Policy Application

Generate and review the Group Policy Results report to confirm that the GPO has been successfully applied.

```text
gpresult.html
```

---

## Best Practice

> [!TIP]
> Always test GPO changes in a non-production OU first.

> [!TIP]
> Use clear and consistent GPO naming conventions to identify their purpose (for example, **L1-PasswordPolicy**).

---

## Common Issues

> [!WARNING]
> If the GPO does not apply as expected, perform the following checks:

* Review **Group Policy Results** to verify policy processing.
* Verify **OU inheritance** settings.
* Confirm **domain controller replication** is healthy and complete.
