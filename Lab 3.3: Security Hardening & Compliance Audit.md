# Lab 3.3: Security Hardening & Compliance Audit

## Overview

**Objective:** Audit and harden Active Directory (AD) infrastructure against modern threats.

**Estimated Time:** 120 minutes

---

## Scenario

Your organization must comply with security standards. Audit the existing Active Directory environment for vulnerabilities, implement appropriate hardening measures, and produce a comprehensive compliance report.

> [!IMPORTANT]
> This lab focuses on strengthening the security posture of an enterprise Active Directory environment through auditing, remediation, and continuous monitoring.

---

## Challenge Tasks

### 1. Audit User Accounts

Review the Active Directory environment and identify:

* Inactive user accounts
* Orphaned accounts
* Privileged accounts

Document any accounts requiring remediation.

---

### 2. Review Group Memberships

Audit security groups to identify:

* Unnecessary nested groups
* Excessive permissions
* Over-privileged administrative groups

Document recommended changes.

---

### 3. Audit Service Accounts

Review all service accounts by:

* Auditing Service Principal Name (SPN) registrations
* Verifying that service accounts use unique passwords

Document any security concerns.

---

### 4. Implement an Account Lockout Policy

Configure an account lockout policy that appropriately balances:

* Security
* Operational usability

Validate the policy after implementation.

---

### 5. Enforce a Strong Password Policy

Implement a password policy that enforces:

* Password complexity requirements
* Strong password standards

Verify that the policy is applied successfully.

---

### 6. Audit Group Policy Object (GPO) Security

Review all applicable Group Policy Objects for:

* GPO scoping
* Windows Management Instrumentation (WMI) filters
* Delegated permissions

Identify any unnecessary or excessive access.

---

### 7. Enable Advanced Audit Logging

Configure auditing to capture important Active Directory events, including:

* Active Directory object changes
* User logon events

Verify that audit events are recorded successfully.

---

### 8. Implement Local Administrator Password Solution (LAPS)

Deploy **Local Administrator Password Solution (LAPS)** to manage local administrator credentials securely.

Validate successful deployment and password management.

---

### 9. Review Administrative Delegation

Audit delegated administrative permissions by:

* Removing inappropriate delegations
* Documenting required delegations

Verify compliance with the Principle of Least Privilege (PoLP).

---

### 10. Audit for Kerberoasting Risks

Review **Service Principal Name (SPN)** configurations to identify potential **Kerberoasting** risks.

Document findings and recommended mitigations.

---

### 11. Implement Attack Surface Reduction

Enable appropriate **Windows Defender** security features to reduce the attack surface of the Active Directory environment.

Validate the implemented security controls.

---

### 12. Create a Compliance Report

Prepare a comprehensive compliance report that includes:

* Audit findings
* Identified vulnerabilities
* Risk assessment
* Remediation actions
* Security recommendations

---

### 13. Establish Continuous Monitoring

Implement continuous monitoring and alerting for critical Active Directory security events.

Monitoring should include:

* Administrative activity
* Authentication events
* Directory changes
* Privileged account usage
* Security alerts

---

## Validation Checklist

Verify the following before completing the lab:

* ✅ User accounts audited.
* ✅ Group memberships reviewed.
* ✅ Service accounts assessed.
* ✅ Account lockout policy implemented.
* ✅ Strong password policy enforced.
* ✅ GPO security reviewed.
* ✅ Advanced audit logging enabled.
* ✅ Local Administrator Password Solution (LAPS) deployed.
* ✅ Administrative delegation reviewed.
* ✅ Kerberoasting risks assessed.
* ✅ Attack surface reduction measures implemented.
* ✅ Compliance report completed.
* ✅ Continuous monitoring configured.

---

## Security Best Practice

> [!TIP]
> Use Microsoft's **Security Compliance Toolkit (SCT)** as a baseline when evaluating and hardening Active Directory environments.

> [!TIP]
> Perform regular security audits and vulnerability scans to identify configuration drift, privilege escalation risks, and emerging security threats.

> [!IMPORTANT]
> Security hardening is an ongoing process. Establish recurring compliance assessments, continuous monitoring, and periodic reviews to maintain a secure and resilient production Active Directory environment.
