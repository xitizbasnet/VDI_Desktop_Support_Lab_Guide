# LAB 08: Remote L1 Application Support 2000-User PAN India Remote Support

## 📘 Overview

L1 (Level 1) Support serves as the first point of contact for end users experiencing application, account, or connectivity issues.

This lab covers:

- Remote support tools
- Application troubleshooting
- VPN and network issue resolution
- Password and account lockout assistance
- Escalation procedures
- Support best practices for a large PAN India user base

---

## 🖥️ Part A: Remote Support Tools

### Step 1: Connect via Quick Assist (Built-in Windows)

Quick Assist is a built-in Microsoft tool that enables secure remote support without requiring additional software installation.

1. Press:

```text
Win + S
```

2. Search for:

```text
Quick Assist
```

3. Open the application.
4. Click **Give Assistance**.
5. Share the generated 6-digit code with the user.
6. Ask the user to:
   - Open Quick Assist
   - Enter the code
   - Approve the connection request

After approval, screen sharing or full control can begin.

> **💡 Tip**
>
> Quick Assist is ideal for occasional support sessions because it is built into Windows and requires minimal setup.

---

### Step 2: Connect via SCCM Remote Control

Navigate to:

```text
SCCM Console → Assets and Compliance → Devices
```

1. Locate the target device.
2. Right-click the device.
3. Select:

```text
Start → Remote Control
```

A remote desktop session will begin.

Features:

- Full desktop visibility
- User can observe all actions performed
- Suitable for troubleshooting corporate-managed devices

> **Note**
>
> SCCM Remote Control provides better integration with managed corporate devices than third-party remote tools.

---

### Step 3: Connect via TeamViewer or AnyDesk (If Approved)

If approved by organizational policy:

1. Ask the user to provide:
   - TeamViewer ID / AnyDesk Address
   - Session Password

2. Enter the provided ID.
3. Request remote control access.
4. Wait for user approval.
5. Begin the support session.

> **⚠️ Warning**
>
> Always use the company-approved and licensed version of TeamViewer or AnyDesk. Personal versions should not be used for enterprise support.

---

## 🔧 Part B: Common L1 Application Issues

### Step 4: Application Won't Open or Crashes

When an application fails to launch or closes unexpectedly:

#### Check Event Viewer

Press:

```text
Win + R
```

Run:

```text
eventvwr
```

Navigate to:

```text
Windows Logs → Application
```

Review:

- Error Events
- Application Name
- Faulting Module

Example:

```text
OUTLOOK.EXE
```

#### Repair the Application

Navigate to:

```text
Control Panel → Programs → Programs and Features
```

Select the application and choose:

```text
Repair
```

#### Reinstall .NET Framework (If Applicable)

If application logs indicate a .NET Framework issue:

- Download the appropriate version from Microsoft.
- Reinstall or repair the framework.
- Reboot the machine if required.

> **Example**
>
> Outlook, custom internal applications, and many third-party business applications commonly depend on .NET Framework components.

---

### Step 5: VPN or Network Connectivity Issues

Perform basic network troubleshooting.

#### Verify Network Connectivity

Ping the gateway:

```cmd
ping 10.0.0.1
```

#### Review IP Configuration

```cmd
ipconfig /all
```

#### Flush DNS Cache and Renew IP Address

```cmd
ipconfig /flushdns
ipconfig /renew
```

#### Reconnect VPN

Reconnect the corporate VPN client.

Examples:

- Cisco AnyConnect
- GlobalProtect

#### Test Connectivity to Internal Services

```powershell
Test-NetConnection -ComputerName dc01.nomura.com -Port 443
```

> **✅ Expected Result**
>
> The test should show a successful TCP connection on port 443.

---

### Step 6: Password or Account Lock Issues

Verify the user's account status using Active Directory Users and Computers (ADUC).

Launch:

```text
dsa.msc
```

#### Check Account Status

1. Locate the user account.
2. Open **Properties**.
3. Review account status.

#### Unlock User Account

Navigate to:

```text
Properties → Account
```

Select:

```text
Unlock Account
```

#### Reset User Password

1. Right-click the user account.
2. Select:

```text
Reset Password
```

3. Assign a temporary password.

> **💡 Tip**
>
> Advise users to update saved passwords on:
>
> - Outlook
> - VPN Clients
> - Mobile Devices
> - Browser Password Managers
> - Remote Desktop Connections

This helps prevent repeated account lockouts.

---

### Step 7: Escalate to L2 if Unresolved

If the issue cannot be resolved at Level 1:

1. Document all troubleshooting steps performed.
2. Collect supporting evidence:
   - Screenshots
   - Error messages
   - Event logs
   - Application logs

3. Update the support ticket.
4. Assign the ticket to the appropriate L2 queue.
5. Inform the user about:
   - Escalation status
   - Current findings
   - Expected SLA

> **Important**
>
> Incomplete ticket documentation can significantly increase resolution time for L2 and L3 teams.

---

## 📝 Standard L1 Troubleshooting Flow

When receiving a support request, follow this structured approach:

1. Identify the issue.
2. Verify user identity.
3. Gather symptoms and error messages.
4. Attempt basic troubleshooting.
5. Review logs and system information.
6. Apply known fixes or workarounds.
7. Verify resolution with the user.
8. Document actions taken.
9. Escalate if necessary.

> **💡 Tip**
>
> Following a consistent troubleshooting methodology improves First Call Resolution (FCR) rates and reduces escalation volume.

---

## 💡 Best Practice Tips

- Always verify the user's identity before starting a remote support session.

Examples:

```text
Employee ID
Manager Verification
Service Desk Ticket Reference
```

- Obtain verbal or written consent before connecting to systems that may display sensitive information.
- Create a ticket for every user interaction, even for quick fixes lasting only a few minutes.
- Maintain a Known Error Database (KEDB) containing:
  - Common issues
  - Root causes
  - Workarounds
  - Permanent fixes

- For PAN India support operations, consider regional working hours and support coverage requirements.
- Capture screenshots whenever unusual errors occur.
- Use standard troubleshooting templates to improve ticket quality and consistency.

> **⚠️ Warning**
>
> Never access or modify user data without authorization and proper business justification.

---

## ✅ Verification Checklist

After completing this lab, verify the following:

### Remote Support

- [ ] Successfully connected using Quick Assist, SCCM, or approved remote tools.
- [ ] User approved the remote session.
- [ ] Support activity was performed successfully.

### Application Troubleshooting

- [ ] Event Viewer logs reviewed.
- [ ] Application repaired or reinstalled if required.
- [ ] User confirmed issue resolution.

### Network Troubleshooting

- [ ] Network connectivity verified.
- [ ] DNS cache cleared.
- [ ] VPN connectivity tested successfully.
- [ ] Internal services accessible.

### Account Support

- [ ] User account status verified.
- [ ] Password reset completed if required.
- [ ] Account unlocked successfully.

