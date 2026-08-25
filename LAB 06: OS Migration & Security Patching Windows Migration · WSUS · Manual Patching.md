# LAB 06: OS Migration & Security Patching Windows Migration · WSUS · Manual Patching

## 📘 Overview

Operating System (OS) Migration involves moving users from an older operating system, such as Windows 7 or Windows 8.1, to Windows 10 or Windows 11 while preserving user data and application settings.

Security patching ensures systems remain protected against vulnerabilities by installing the latest operating system and software updates.

This lab covers:

- User data backup and migration
- In-place Windows upgrades
- User data restoration
- Post-migration validation
- Manual Windows patching
- WSUS patch deployment
- Patch status verification

---

## 🔄 Part A: OS Migration (Windows 7 → Windows 10)

### Step 1: Back Up User Data

Before starting the migration, back up all required user data to a network location.

Source Location:

```text
C:\Users\username
```

Destination Example:

```text
\\NAS\Backup\username
```

Common folders to back up:

- Documents
- Desktop
- Downloads
- AppData (if required)

Verify that the backup size matches the original source data.

Use the following command to perform the backup:

```cmd
robocopy C:\Users\vinod \\NAS01\Backup\vinod /E /LOG:backup.log
```

> **💡 Tip**
>
> Always review the generated log file after the backup to identify skipped files or permission-related issues.

---

### Step 2: Run the Windows 10 Upgrade (In-Place Upgrade)

Download and launch the Windows 10 Media Creation Tool.

Select:

```text
Upgrade this PC now
```

Choose:

```text
Keep personal files and apps
```

Proceed through the installation wizard and allow the upgrade to complete.

> **Enterprise Option**
>
> Organizations commonly use SCCM Task Sequences to perform in-place upgrades across multiple devices.

---

### Step 3: Restore User Data

After the operating system upgrade is complete, restore the user's data from the backup location.

```cmd
robocopy \\NAS01\Backup\vinod C:\Users\vinod /E
```

> **Note**
>
> Verify folder permissions after restoring data to ensure the user retains access to all required files.

---

### Step 4: Perform Post-Migration Verification

Verify the following after migration:

- Domain membership remains intact
- User profile loads successfully
- Applications function correctly
- Network connectivity is operational
- Corporate resources are accessible

Test commonly used applications, such as:

- Microsoft Outlook
- Web Browsers
- Line-of-Business (LOB) Applications

Verify that network drives are mapped correctly through:

- Group Policy Objects (GPO)
- Logon Scripts

✅ User migration is considered successful only after all validation checks pass.

---

## 🔒 Part B: Security Patch Management

### Step 5: Perform Manual Windows Updates

Navigate to:

```text
Settings → Update & Security → Windows Update → Check for Updates
```

Alternatively, install updates using PowerShell.

#### Install PSWindowsUpdate Module

```powershell
Install-Module PSWindowsUpdate -Force
```

#### Scan and Install Updates

```powershell
Get-WindowsUpdate | Install-WindowsUpdate -AcceptAll -AutoReboot
```

> **⚠️ Warning**
>
> Some updates may automatically restart the system. Ensure users save their work before deployment.

---

### Step 6: WSUS - Approve and Deploy Patches (Administrator)

Open the WSUS Console.

Example:

```text
wsus.nomura.com
```

or launch the Windows Server WSUS Role Management Console.

Navigate to:

```text
Updates → All Updates
```

Apply the following filter:

```text
Unapproved
```

Perform the following actions:

1. Select required Critical and Security Updates.
2. Right-click the selected updates.
3. Choose **Approve**.
4. Approve the updates for the target computer group.

To force Windows clients to check in:

```cmd
wuauclt /detectnow
```

#### Force Update Detection and Installation

```cmd
wuauclt /detectnow
wuauclt /updatenow
```

> **Note**
>
> Depending on the WSUS configuration, clients may take several minutes to report their compliance status.

---

### Step 7: Verify Patch Status on the Machine

#### Check Recently Installed Updates

```powershell
Get-HotFix | Sort-Object InstalledOn -Descending | Select -First 10
```

#### Check Recent Update History

```powershell
Get-WmiObject Win32_QuickFixEngineering | Sort HotFixID | Select -Last 5
```

Review the output to confirm:

- Successful update installation
- Latest security patches applied
- No missing critical updates

> **Example**
>
> A healthy system should display recently installed Windows security updates with current installation dates.

---

## 💡 Best Practice Tips

- Always test patches on a pilot group of 5–10 machines before deploying them organization-wide.
- Schedule patch deployments during approved maintenance windows rather than during business hours.
- Deploy Critical and Zero-Day security patches within 24–48 hours of release whenever possible.
- Maintain patch compliance reporting to identify systems that have not been patched for more than 30 days.
- Create a rollback plan before patch deployment.

Common rollback options include:

- System Restore Point
- VMware Snapshot
- Hyper-V Checkpoint
- Full System Backup

> **⚠️ Warning**
>
> Deploying untested patches directly to production systems may result in application failures, user disruption, or downtime.

---

## ✅ Verification Checklist

After completing this lab, verify the following:

### OS Migration

- [ ] User data is successfully backed up.
- [ ] Windows upgrade completed successfully.
- [ ] User profile loads correctly after migration.
- [ ] Corporate applications launch without issues.
- [ ] Network drives are available.
- [ ] Device remains joined to the domain.

### Security Patching

- [ ] Windows Update completes successfully.
- [ ] Required security patches are installed.
- [ ] WSUS deployment status is successful.
- [ ] No failed updates are reported.
- [ ] Patch compliance reports are updated.

### Documentation

- [ ] Migration details are recorded.
- [ ] Patch deployment activity is documented.
- [ ] Change ticket or CMDB has been updated.

---
