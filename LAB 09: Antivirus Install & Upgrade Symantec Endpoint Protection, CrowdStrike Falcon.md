# LAB 09: Antivirus Install & Upgrade Symantec Endpoint Protection, CrowdStrike Falcon

## 📘 Overview

Antivirus management is a critical security responsibility that helps protect endpoints from malware, ransomware, unauthorized access, and other cyber threats.

This lab covers:

- Symantec Endpoint Protection (SEP) deployment
- SEP upgrades and definition updates
- CrowdStrike Falcon Sensor installation
- Falcon Sensor upgrades
- Endpoint protection validation

---

## 🛡️ Part A: Symantec Endpoint Protection (SEP)

### Step 1: Deploy SEP to a New Machine via SEPM

Open the Symantec Endpoint Protection Manager (SEPM) Console:

```text
https://<SEPM-IP>:8443/console
```

Navigate to:

```text
Clients → Right-click Group
```

Example:

```text
Mumbai-Desktops
```

Select:

```text
Install Client
```

Deployment Options:

- Push Deployment
  - Enter machine name or IP address

- Web Link Deployment
  - Share the installation URL with the user

SEP installs silently and automatically registers with the SEPM server.

> **💡 Tip**
>
> Push deployment is preferred for domain-joined machines that are online and reachable from the network.

---

### Step 2: Perform Manual SEP Client Installation

Run the installer on the endpoint:

```cmd
\\SEPM-Server\Install\setup.exe /qn /norestart
```

After installation, verify SEP is running.

Check the system tray:

```text
SEP Shield Icon
```

Status Indicators:

| Status | Meaning |
|----------|----------|
| 🟢 Green | Protected |
| 🟡 Yellow | Warning |
| 🔴 Red | Protection Issue |

> **✅ Expected Result**
>
> The SEP shield icon should display a green status indicating the endpoint is protected.

---

### Step 3: Update SEP Virus Definitions

#### Update from SEPM

Navigate to:

```text
Admin → LiveUpdate Settings
```

Select:

```text
Run LiveUpdate
```

#### Update from Endpoint

1. Right-click the SEP tray icon.
2. Select:

```text
LiveUpdate
```

3. Click:

```text
Check for Updates
```

Verify the virus definition date.

> **Best Practice**
>
> Virus definitions should be no more than 24–48 hours old.

---

### Step 4: Upgrade SEP Clients via SEPM

Navigate to:

```text
Admin → Install Packages
```

Upload the latest SEP package:

```text
Add Package
```

Upload:

```text
New SEP .zip Package
```

Deploy the upgrade:

```text
Clients → Select Group → Upgrade Clients
```

Schedule the upgrade during a maintenance window.

> **⚠️ Warning**
>
> Large-scale upgrades should first be tested on a pilot group before deployment across production devices.

---

## 🦅 Part B: CrowdStrike Falcon Sensor

### Step 5: Download Falcon Sensor Installer

Log in to the CrowdStrike Falcon Console:

```text
https://falcon.crowdstrike.com
```

Navigate to:

```text
Hosts → Sensor Downloads
```

Select:

```text
Windows x64
```

Download:

```text
WindowsSensor.exe
```

> **Note**
>
> Ensure you download the correct sensor version for the target operating system.

---

### Step 6: Install Falcon Sensor (Windows)

Run the installer using elevated privileges.

```cmd
WindowsSensor.exe /install /quiet /norestart CID=<CustomerID>
```

Verify installation:

```cmd
sc query csagent
```

> **✅ Expected Result**
>
> The CrowdStrike Falcon Sensor service should display a running status.

---

### Step 7: Verify Host in Falcon Console

Navigate to:

```text
Falcon Console → Hosts → Devices
```

Search using the endpoint hostname.

Example:

```text
nomura-ws01
```

Verify the device status.

Expected status:

```text
Normal
```

Status indicator:

```text
Green
```

If the device does not appear:

- Verify the Customer ID (CID)
- Reinstall the sensor
- Check firewall settings
- Verify internet connectivity
- Confirm HTTPS communication is allowed

> **💡 Tip**
>
> Newly deployed sensors may take several minutes to appear in the Falcon Console.

---

### Step 8: Upgrade Falcon Sensor

Navigate to:

```text
Falcon Console → Hosts → Sensor Update Policy
```

Configure:

```text
Auto-Update Policy
```

Assign the policy to the required host group.

Alternatively, manually deploy the latest sensor package through SCCM.

Example:

```text
Deploy new WindowsSensor.exe to target collection
```

> **Note**
>
> Automatic sensor updates help maintain protection without requiring manual intervention.

---

## 🔍 Verification Commands

### Verify SEP Installation

Check the SEP system tray icon and client status from the endpoint.

### Verify CrowdStrike Sensor Service

```cmd
sc query csagent
```

### Verify CrowdStrike Host Registration

```text
Falcon Console → Hosts → Devices
```

Search for the endpoint hostname.

---

## 💡 Best Practice Tips

- Never disable real-time protection unless specifically required for troubleshooting and approved by the security team.
- Review antivirus coverage reports weekly to identify unmanaged or unprotected devices.
- Ensure CrowdStrike Falcon Sensor can communicate outbound over HTTPS.

Required Port:

```text
TCP 443
```

- Configure exclusions carefully for:
  - Large databases
  - Development tools
  - Performance-intensive applications

Document all exclusions for audit and security review purposes.

- Remove any existing antivirus products before installing SEP to prevent software conflicts.
- Test antivirus upgrades on pilot devices before organization-wide deployment.
- Maintain documentation for antivirus versions, deployment dates, and endpoint coverage.

> **⚠️ Warning**
>
> Running multiple antivirus products simultaneously can lead to performance degradation, scanning conflicts, and system instability.

---

## ✅ Verification Checklist

### Symantec Endpoint Protection

- [ ] SEP successfully installed.
- [ ] Client registers with SEPM.
- [ ] Real-time protection is enabled.
- [ ] Virus definitions are current.
- [ ] SEP shield displays a green status.

### CrowdStrike Falcon

- [ ] Falcon Sensor installed successfully.
- [ ] `csagent` service is running.
- [ ] Host appears in Falcon Console.
- [ ] Device status shows Normal.
- [ ] Sensor update policy is assigned.

### Security Validation

- [ ] Endpoint is protected by approved antivirus software.
- [ ] No conflicting antivirus products are installed.
- [ ] Security policies are applied successfully.
- [ ] Endpoint appears in compliance reports.

---
