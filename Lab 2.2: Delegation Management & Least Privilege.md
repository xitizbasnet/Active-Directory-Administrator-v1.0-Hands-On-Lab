# Lab 2.2: Delegation Management & Least Privilege

## Overview

**Objective:** Implement proper delegation of administrative tasks.

**Estimated Time:** 50 minutes

---

## Scenario

Implement delegation for the IT support team to reset passwords and manage user accounts within specific **Organizational Units (OUs)** without granting full **Domain Admin** privileges.

> [!NOTE]
> This lab demonstrates how to delegate administrative responsibilities while following the **Principle of Least Privilege (PoLP)**.

---

## Lab Procedure

### Step 1 – Create a Security Group

Create a security group for the IT support team.

Example:

```text
IT-Support-Group
```

Add the appropriate IT support staff members to the group.

---

### Step 2 – Open the Delegate Control Wizard

1. Open **Active Directory Users and Computers (ADUC)**.
2. Right-click the target **Organizational Unit (OU)**.
3. Select **Delegate Control**.
4. Click **Next**.

---

### Step 3 – Add the Security Group

1. Add the following group to the selected users or groups:

```text
IT-Support-Group
```

2. Click **Next**.

---

### Step 4 – Delegate Common Administrative Tasks

1. Select:

* **Delegate the following common tasks**

2. Enable the following option:

* **Reset user passwords**

3. Click **Next**.

---

### Step 5 – Delegate Additional Administrative Tasks

Add the following delegated task:

* **Modify the membership of a group**

---

### Step 6 – Complete the Delegation Wizard

1. Review the selected permissions.
2. Complete the **Delegate Control Wizard**.

---

### Step 7 – Verify Delegated Permissions

1. Right-click the target **Organizational Unit (OU)**.
2. Select **Properties**.
3. Open the **Security** tab.
4. Verify that the delegated permissions have been applied correctly.

---

### Step 8 – Add Additional Permissions (If Required)

If required by your organization's operational procedures, grant additional permissions such as:

* Create user objects
* Delete user objects

> [!IMPORTANT]
> Grant only the minimum permissions required for the delegated role.

---

### Step 9 – Test the Delegation

Sign in using an account that is a member of:

```text
IT-Support-Group
```

Verify that the delegated user can:

* Reset user passwords.
* Perform delegated user account management tasks.

---

### Step 10 – Validate Permission Restrictions

Confirm that the delegated user **cannot** perform administrative tasks outside the delegated scope, including:

* Modifying Group Policy Objects (GPOs)
* Creating Domain Controllers (DCs)

> [!CAUTION]
> Successful delegation includes both allowing authorized actions and preventing unauthorized administrative access.

---

### Step 11 – Document the Delegation Model

Document the delegation model implemented within your Active Directory environment, including:

* Delegated security groups
* Assigned permissions
* Target Organizational Units (OUs)
* Administrative responsibilities
* Operational limitations

---

## Validation Checklist

Verify the following before completing the lab:

* ✅ Security group created successfully.
* ✅ Delegate Control Wizard completed.
* ✅ Password reset permission assigned.
* ✅ Group membership management delegated.
* ✅ Additional permissions configured only when required.
* ✅ Delegated user can perform assigned tasks.
* ✅ Delegated user cannot perform unauthorized administrative actions.
* ✅ Delegation model documented.

---

## Best Practice

> [!TIP]
> Always apply the **Principle of Least Privilege (PoLP)** when delegating administrative access.

> [!TIP]
> Use **time-bound delegation** for temporary administrative requirements whenever possible.

> [!TIP]
> Maintain comprehensive documentation of all delegated permissions, administrative groups, and Organizational Unit (OU) assignments to support auditing, compliance, and troubleshooting.
