# LAB 04: Active Directory, DNS & DHCP Core Windows Infrastructure Services

## 📘 Overview

Active Directory (AD), DNS, and DHCP form the foundation of Windows enterprise networking and identity management.

This lab covers:

- Active Directory user management
- Password reset and account unlock operations
- Group membership administration
- DNS record management
- DHCP scope administration
- DHCP reservations

---

## 👥 Part A: Active Directory User Management

### Step 1: Open Active Directory Users and Computers (ADUC)

Open the Run dialog and launch ADUC:

```text
dsa.msc
```

---

### Step 2: Create a New User

1. Right-click the target OU.

**Example:**

```text
OU=Mumbai,DC=nomura,DC=com
```

2. Select:

```text
New → User
```

3. Enter the required details:

- First Name
- Last Name
- User Logon Name

**Example:**

```text
vinod.muleva
```

4. Configure the password.
5. Uncheck **User must change password at next logon** for service accounts if required.
6. Click **Finish**.

#### PowerShell Alternative

```powershell
New-ADUser -Name 'Vinod Muleva' -SamAccountName 'vinod.muleva' -UserPrincipalName 'vinod.muleva@nomura.com' -Enabled $true -AccountPassword (ConvertTo-SecureString 'P@ssw0rd!' -AsPlainText -Force)
```

> **💡 Tip**
>
> Follow a consistent naming convention for user accounts to simplify administration and auditing.

---

### Step 3: Reset Password and Unlock Account

1. Right-click the user account.
2. Select **Reset Password**.
3. Enter the new password.
4. Check **Unlock account** if the account is locked.
5. Click **OK**.

> **Example**
>
> This procedure is commonly used when users forget their password or are locked out after multiple failed login attempts.

---

### Step 4: Add User to a Security Group

Add the user to the required security group.

#### PowerShell Alternative

```powershell
Add-ADGroupMember -Identity 'VPN_Users' -Members 'vinod.muleva'
```

> **Note**
>
> Group membership determines user access to applications, network resources, VPN access, and file shares.

---

## 🌐 Part B: DNS Management

### Step 5: Open DNS Manager and Create an A Record

Open DNS Manager:

```text
dnsmgmt.msc
```

Navigate to:

```text
Forward Lookup Zones → nomura.com
```

1. Right-click the zone.
2. Select:

```text
New Host (A or AAAA)
```

3. Enter the following information:

| Field | Value |
|---------|---------|
| Name | webserver01 |
| IP Address | 10.0.1.50 |

4. Click **Add Host**.

This creates the following DNS record:

```text
webserver01.nomura.com → 10.0.1.50
```

> **Example**
>
> Users can now access the server using the hostname instead of memorizing the IP address.

---

### Step 6: Flush DNS Cache and Verify Name Resolution

Clear the local DNS cache:

```cmd
ipconfig /flushdns
```

Verify DNS resolution:

```cmd
nslookup webserver01.nomura.com
```

> **✅ Expected Result**
>
> The hostname should successfully resolve to:
>
> ```text
> 10.0.1.50
> ```

---

## 📡 Part C: DHCP Scope Management

### Step 7: Open DHCP Console and Review Scope Information

Open the DHCP Management Console:

```text
dhcpmgmt.msc
```

Navigate to:

```text
Server → IPv4 → Scope → Address Pool
```

Review the configured address range.

**Example:**

```text
10.0.1.100 – 10.0.1.200
```

Next, review:

```text
Address Leases
```

This displays:

- Active clients
- Assigned IP addresses
- Lease duration
- Device information

> **Note**
>
> Monitoring address leases helps identify IP exhaustion and unauthorized devices.

---

### Step 8: Create a DHCP Reservation

1. Right-click **Reservations**.
2. Select **New Reservation**.
3. Enter the reservation details:

| Field | Value |
|---------|---------|
| Name | NomPrinter01 |
| IP Address | 10.0.1.210 |
| MAC Address | AA:BB:CC:DD:EE:FF |

4. Click **Add**.

The printer will now always receive the same IP address from DHCP.

> **Example**
>
> DHCP Reservations are commonly used for:
>
> - Printers
> - Network appliances
> - CCTV systems
> - Servers requiring predictable IP addressing

---

## 💡 Best Practice Tips

- Use Organizational Units (OUs) logically based on department, location, or business function for simplified administration and GPO management.

**Example:**

```text
OU=Mumbai
OU=Finance
OU=HR
```

- Always disable user accounts instead of immediately deleting them during offboarding. Retain disabled accounts for at least 30 days.

- Configure DNS TTL values according to business requirements:

| Record Type | Recommended TTL |
|------------|------------------|
| Frequently Changing Records | 300 Seconds |
| Stable Records | 86400 Seconds |

- Exclude critical infrastructure devices from DHCP address pools, such as:
  - Default gateways
  - Domain Controllers
  - Application Servers
  - Printers

- Enable DHCP failover using split-scope or hot standby configurations to improve availability and resilience.

---

## ✅ Verification Checklist

After completing this lab, verify the following:

- [ ] New Active Directory user has been created successfully.
- [ ] User password can be reset and account unlocked.
- [ ] User has been added to the required security group.
- [ ] DNS A record has been created successfully.
- [ ] Hostname resolves correctly using `nslookup`.
- [ ] DHCP scope configuration is visible and operational.
- [ ] DHCP reservations are assigning the expected IP address.
- [ ] Clients are receiving IP addresses from the correct DHCP scope.

---
