# LAB 11: Microsoft Outlook Configuration Exchange · Microsoft 365 · Profiles · PST Management

## 📘 Overview

Microsoft Outlook is the primary email client used in enterprise environments for email communication, calendar management, contacts, and collaboration.

This lab covers:

- Creating a new Outlook profile
- Configuring Exchange and Microsoft 365 accounts
- Adding shared mailboxes
- Managing OST and PST files
- Troubleshooting common Outlook issues
- Using Microsoft Support and Recovery Assistant (SaRA)

---

## 👤 Part A: Create a New Outlook Profile

### Step 1: Open Mail Settings

Open the Mail configuration utility:

```text
Control Panel → Mail (Microsoft Outlook) → Show Profiles → Add
```

Enter a profile name.

**Example:**

```text
NomuraEmail
```

Click **OK**.

### Step 2: Configure the Mail Profile

1. Enter:
   - Name
   - Email Address
   - Password

2. Click **Next**.

If the device is domain-joined and Autodiscover is configured correctly, Outlook automatically discovers the Exchange settings.

3. Click **Finish**.
4. Set the profile as the default profile.

> **💡 Tip**
>
> Creating a new Outlook profile is often the quickest solution for mailbox synchronization, login, and profile corruption issues.

---

## ☁️ Part B: Configure Microsoft 365 Account

### Step 3: Add a Microsoft 365 Account

Open Outlook and navigate to:

```text
File → Add Account
```

Enter the user's email address.

**Example:**

```text
vinod.muleva@nomura.com
```

Click:

```text
Connect
```

Outlook automatically detects:

- Microsoft 365
- Exchange Online
- Hybrid Exchange environments

Enter the password and complete Multi-Factor Authentication (MFA) if prompted.

Common MFA methods:

- Microsoft Authenticator
- OTP
- Hardware Token

Click:

```text
Done
```

Outlook will begin synchronizing the mailbox.

✅ Mail, Calendar, Contacts, and other folders should automatically appear.

---

## 📬 Part C: Configure Shared Mailbox

### Step 4: Add a Shared Mailbox

Navigate to:

```text
File → Account Settings → Account Settings
```

Select the mailbox and click:

```text
Change → More Settings
```

Open the:

```text
Advanced
```

tab and click:

```text
Add
```

Enter the shared mailbox address.

**Examples:**

```text
helpdesk@nomura.com
```

```text
hr@nomura.com
```

```text
finance@nomura.com
```

Alternatively:

1. Right-click the mailbox pane.
2. Select:

```text
Add Shared Folder
```

3. Enter the mailbox name.

> **Note**
>
> The user must have Full Access or appropriate mailbox permissions assigned before the shared mailbox can be opened.

---

## 💾 Part D: OST Management

### Step 5: Locate the OST File

Default OST file location:

```text
C:\Users\%USERNAME%\AppData\Local\Microsoft\Outlook\
```

To locate the active OST file:

```text
File → Account Settings → Data Files → Open File Location
```

### Step 6: Rebuild a Corrupt OST File

If Outlook experiences:

- Synchronization issues
- Search failures
- Slow performance
- OST corruption

Perform the following steps:

1. Close Outlook.
2. Browse to the OST location.
3. Delete the OST file.
4. Reopen Outlook.

The OST file will automatically be recreated and synchronized from Exchange or Microsoft 365.

> **Important**
>
> OST files are offline cache files. Messages stored on the mail server will automatically re-sync after the OST is recreated.

---

## 📁 Part E: PST Export and Import

### Step 7: Export Mailbox to PST

Navigate to:

```text
File → Open & Export → Import/Export
```

Select:

```text
Export to a File
```

Next select:

```text
Outlook Data File (.pst)
```

Choose the mailbox and destination path.

Example:

```text
D:\MailBackup\Vinod_Muleva.pst
```

Complete the export wizard.

---

### Step 8: Import a PST File

Navigate to:

```text
File → Open & Export → Import/Export
```

Select:

```text
Import from another program or file
```

Choose:

```text
Outlook Data File (.pst)
```

Browse to the PST file and complete the import wizard.

> **Example**
>
> PST imports are commonly used during:
>
> - User migrations
> - Mailbox restorations
> - Historical email recovery
> - Archive imports

---

## 🔧 Part F: Common Outlook Troubleshooting

### Step 9: Outlook Not Sending or Receiving Emails

Perform the following checks.

#### Send/Receive All Folders

Navigate to:

```text
Send/Receive → Send/Receive All Folders
```

Shortcut:

```text
F9
```

#### Test Account Configuration

Navigate to:

```text
Tools → Account Settings → Test Account Settings
```

Verify:

- Network connectivity
- Mailbox connectivity
- Authentication

---

### Step 10: Start Outlook in Safe Mode

Launch Outlook in Safe Mode:

```cmd
outlook.exe /safe
```

Safe Mode disables all Outlook add-ins.

If Outlook works in Safe Mode but fails during normal startup, investigate installed add-ins.

Common problematic add-ins:

- PDF Add-ins
- CRM Plug-ins
- Third-party email tools

---

### Step 11: Reset Outlook Navigation Pane

Corrupted navigation settings often prevent Outlook from opening.

Run:

```cmd
outlook.exe /resetnavpane
```

This resets:

- Folder pane settings
- Favorites
- Navigation configuration

---

## 🛠️ Part G: Run Microsoft Support and Recovery Assistant (SaRA)

### Step 12: Repair Outlook Using SaRA

Download and install:

```text
Microsoft Support and Recovery Assistant (SaRA)
```

Launch the tool and select:

```text
I have problems with Outlook
```

Follow the troubleshooting wizard.

SaRA can automatically diagnose and repair:

- Outlook startup issues
- Profile corruption
- Office activation problems
- Exchange connectivity issues
- Microsoft 365 sign-in problems
- Autodiscover failures

> **💡 Tip**
>
> SaRA should be one of the first troubleshooting tools used for persistent Outlook issues.

---

## ⚡ Common Outlook Commands

### Start Outlook in Safe Mode

```cmd
outlook.exe /safe
```

### Reset Navigation Pane

```cmd
outlook.exe /resetnavpane
```

### Open Outlook Profile Configuration

```cmd
control mlcfg32.cpl
```

### Open Mail Settings

```cmd
control.exe mlcfg32.cpl
```

---

## 💡 Best Practice Tips

- Always create a fresh Outlook profile for a new user instead of copying an existing profile.
- Keep mailbox sizes under control to maintain Outlook performance.
- OST files larger than **50 GB** can lead to synchronization and performance issues.
- Archive old emails to PST files when appropriate.
- Enable Cached Exchange Mode for:
  - VPN users
  - Remote users
  - VDI users
  - Users with unstable networks

- Ensure Autodiscover is functioning correctly for seamless mailbox setup.
- Verify Exchange and Microsoft 365 DNS records during mailbox troubleshooting.
- Check Microsoft 365 Service Health before performing extensive troubleshooting.

Portal:

```text
admin.microsoft.com
```

> **⚠️ Warning**
>
> Deleting a PST file without a backup may result in permanent data loss.

> **⚠️ Warning**
>
> Never store PST files on network drives unless specifically approved by organizational policy, as this may lead to corruption and performance issues.

---

 
