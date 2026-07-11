# Lab 1.2: DNS Management Basics

## Overview

**Objective:** Create and manage DNS records for domain services.

**Estimated Time:** 25 minutes

---

## Lab Procedure

### Step 1 – Open DNS Manager

On the domain controller:

1. Open **Server Manager**.
2. Navigate to **Tools**.
3. Select **DNS**.

---

### Step 2 – Expand the Forward Lookup Zones

1. In **DNS Manager**, expand **Forward Lookup Zones**.
2. Navigate to your domain zone.

---

### Step 3 – Create an A Record

1. Right-click inside the zone.
2. Select **New Host (A or AAAA)**.
3. Enter the following:

   * Hostname
   * IP address

---

### Step 4 – Create a CNAME Record

1. Right-click the zone.
2. Select **New Alias (CNAME)**.
3. Create an alias for the required service.

---

### Step 5 – Create an MX Record

1. Right-click the zone.
2. Select **Other New Records**.
3. Choose **Mail Exchanger (MX)**.
4. Add the mail server.

---

### Step 6 – Create an SRV Record

1. Right-click the zone.
2. Select **Other New Records**.
3. Choose **Service Location (SRV)**.
4. Define the required service port.

---

### Step 7 – Test DNS Resolution

Open **Command Prompt** and run:

```cmd
nslookup hostname.yourdomain.com
```

Verify that the hostname resolves to the expected IP address.

---

### Step 8 – Test Reverse Lookup

Run the following command:

```cmd
nslookup -type=PTR 192.168.1.x
```

Verify that the reverse lookup returns the correct hostname.

---

### Step 9 – Check DNS Event Logs

Review the **DNS Event Viewer** for any query or service-related errors.

> [!NOTE]
> Investigate any warnings or errors before placing DNS records into production use.

---

## Best Practice

> [!TIP]
> Follow these DNS management best practices:

* Maintain consistent naming conventions.
* Use lowercase for DNS records.
* Test all DNS records after creation to verify proper name resolution.
