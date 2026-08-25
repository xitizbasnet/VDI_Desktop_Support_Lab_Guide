# LAB 07: SCCM Remote Software Deployment Microsoft Endpoint Configuration Manager

## 📘 Overview

SCCM (Microsoft Endpoint Configuration Manager - MECM) enables IT administrators to remotely deploy, update, and manage software across thousands of devices without requiring hands-on access to individual machines.

This lab covers:

- Creating an application in SCCM
- Deploying software to device collections
- Monitoring deployment status
- Uninstalling applications remotely
- Running PowerShell scripts on remote machines

---

## 🖥️ Part A: Create Application in SCCM

### Step 1: Open SCCM Console

Launch the Configuration Manager Console:

```text
Start → Microsoft Endpoint Manager → Configuration Manager Console
```

Alternatively, install or launch the admin console from:

```text
\\SCCM-Server\SMSSetup\AdminConsole.msi
```

> **Note**
>
> Ensure your account has the appropriate SCCM administrative permissions before creating applications or deployments.

---

### Step 2: Create Application Package

Navigate to:

```text
Software Library → Application Management → Applications
```

1. Right-click **Applications**.
2. Select **Create Application**.
3. Choose one of the following application types:
   - Windows Installer (*.msi)
   - Script Installer

4. Browse to the installation source.

Example:

```text
\\SCCM-Source\Software\7zip\7z2301-x64.msi
```

5. Enter the application details:
   - Name
   - Version
   - Publisher

6. Click:

```text
Next → Summary → Close
```

✅ The application is now available for deployment.

> **Example**
>
> Common software deployed through SCCM includes:
>
> - 7-Zip
> - Google Chrome
> - Microsoft Office
> - Adobe Acrobat Reader
> - Citrix Workspace App

---

## 🚀 Part B: Deploy Application

### Step 3: Deploy to Device Collection

1. Right-click the application.
2. Select **Deploy**.

Choose the target collection.

Example:

```text
All Mumbai Desktops
```

or a specific OU-based collection.

Configure the deployment purpose:

| Deployment Type | Description |
|-----------------|-------------|
| Required | Mandatory installation |
| Available | Optional installation through Software Center |

Configure the deployment schedule:

- Deploy Immediately (ASAP)
- Specify a Maintenance Window

Click:

```text
Next → Summary → Close
```

> **💡 Tip**
>
> Use **Available** deployments for optional software to reduce unnecessary help desk tickets and give users flexibility.

---

### Step 4: Monitor Deployment Status

Navigate to:

```text
Monitoring → Deployments
```

Select the deployment to review status information.

Available deployment states include:

- Success
- In Progress
- Error
- Requirements Not Met

To troubleshoot failed installations:

1. Open the **Error** tab.
2. Right-click the affected device.
3. Select **View Status Messages**.

> **Example**
>
> Common deployment failures may occur due to:
>
> - Insufficient disk space
> - SCCM client issues
> - Software dependencies
> - Missing installation source files

---

## 🗑️ Part C: Remote Software Removal

### Step 5: Uninstall Application via SCCM

1. Navigate to **Applications**.
2. Select the application.
3. Right-click and select **Deploy**.
4. Change the deployment action from:

```text
Install
```

to

```text
Uninstall
```

5. Deploy the uninstall action to the target collection.

The application will be removed during the next SCCM policy cycle.

> **Note**
>
> Verify that the application includes a valid uninstall command before deploying removal actions.

---

## ⚡ Part D: Remote Execution via SCCM

### Step 6: Run Script Remotely

Navigate to:

```text
SCCM → Scripts → Create Script
```

Example Script:

**Script Name**

```text
Fix_Outlook_Profile
```

**Language**

```text
PowerShell
```

**Script Content**

```powershell
Remove-Item 'HKCU:\Software\Microsoft\Office\16.0\Outlook\Profiles' -Recurse
Write-Output 'Outlook profile cleared'
```

Deploy the script:

1. Right-click the target device.
2. Select **Run Script**.
3. Choose the desired script.
4. Click **Run**.

Review execution results under:

```text
Scripts Status
```

> **⚠️ Warning**
>
> Test all scripts in a non-production environment before deploying broadly. Improper scripts can impact user profiles, applications, or system functionality.

---

## 💡 Best Practice Tips

- Always test software deployments on a pilot collection containing 1–2 devices before large-scale deployment.
- Use **Available** deployments for optional software to provide self-service installation through Software Center.
- Regularly monitor SCCM client health using:

```text
Monitoring → Client Status
```

- Utilize SCCM Maintenance Windows to prevent installations and reboots during business hours.
- Maintain a consistent naming convention for collections.

Examples:

```text
LOC_Mumbai_Desktops
```

```text
DEPT_Finance_Laptops
```

- Distribute content to Distribution Points before deploying software to avoid installation failures.
- Monitor deployment success rates and remediate recurring issues promptly.

> **💡 Tip**
>
> Maintaining healthy SCCM clients significantly improves software deployment success rates and reporting accuracy.

---

## ✅ Verification Checklist

After completing this lab, verify the following:

### Application Creation

- [ ] Application has been created successfully.
- [ ] Application metadata (name, version, publisher) is accurate.
- [ ] Source files are accessible from SCCM.

### Deployment

- [ ] Application is deployed to the correct collection.
- [ ] Deployment schedule is configured correctly.
- [ ] Devices receive the deployment policy.

### Monitoring

- [ ] Deployment status shows successful installation.
- [ ] Failed installations are reviewed and investigated.
- [ ] Status messages are available for troubleshooting.

### Software Removal

- [ ] Uninstall deployment is configured correctly.
- [ ] Target machines successfully remove the application.

### Script Execution

- [ ] PowerShell script executes successfully.
- [ ] Script output is visible in SCCM.
- [ ] No unexpected errors are reported.

---
