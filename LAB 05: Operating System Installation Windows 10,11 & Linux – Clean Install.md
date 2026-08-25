# LAB 05: Operating System Installation Windows 10,11 & Linux – Clean Install

## 📘 Overview

This lab covers clean Operating System (OS) installation on both Windows and Linux platforms. These procedures are commonly performed during device provisioning, desktop support activities, hardware replacement, and new employee onboarding.

This lab includes:

- Windows 10/11 clean installation
- Ubuntu Linux installation
- BIOS/UEFI configuration
- Post-installation system setup
- Basic Linux system configuration

---

## 💻 Part A: Windows 10/11 Clean Install

### Step 1: Create a Bootable USB

1. Download the Windows 10 or Windows 11 ISO from Microsoft.
2. Open Rufus.

```text
https://rufus.ie
```

3. Configure the following settings:

| Setting | Value |
|----------|---------|
| Boot Selection | Windows ISO |
| Partition Scheme | GPT |
| File System | FAT32 |

4. Click **Start**.

✅ Result: A bootable Windows installation USB drive is created.

> **💡 Tip**
>
> Always verify the ISO checksum when downloading operating system images from the internet.

---

### Step 2: Configure BIOS/UEFI Settings

1. Restart the computer.
2. Enter BIOS/UEFI using the manufacturer-specific key.

Common keys:

```text
F2
Delete
F12
```

3. Configure the following settings:

- Disable Secure Boot temporarily if required.
- Set the USB drive as the first boot device.
- Save the configuration and exit.

> **Note**
>
> BIOS menus vary between manufacturers such as Dell, HP, Lenovo, and Acer.

---

### Step 3: Run the Windows Installation Wizard

1. Boot the device from the USB drive.
2. Wait for Windows Setup to load.
3. Select:

- Language
- Time and Region
- Keyboard Layout

4. Click **Next**.
5. Select **Install Now**.
6. Enter the product key or choose **I don't have a product key** to activate later.
7. Select:

```text
Custom Install (Advanced)
```

8. Choose the target drive.
9. Format the disk if performing a clean installation.
10. Click **Next**.

Windows copies installation files and installs the operating system.

> **⏱ Expected Duration**
>
> Installation typically takes between 15 and 25 minutes depending on hardware specifications.

The system will automatically reboot during the installation process.

---

### Step 4: Perform Post-Installation Setup

After Windows installation completes:

1. Configure:
   - Region
   - Keyboard Layout
   - Local or Organizational Account

2. For corporate devices, join the domain:

```text
Settings → System → About → Domain
```

Domain:

```text
nomura.com
```

3. Verify hardware drivers.

Navigate to:

```text
Device Manager
```

Check for:

- Missing drivers
- Yellow warning icons
- Unknown devices

4. Run Windows Updates.

Navigate to:

```text
Settings → Update & Security → Check for Updates
```

> **💡 Tip**
>
> Installing Windows Updates immediately helps ensure security patches and device drivers are current before software deployment.

---

## 🐧 Part B: Ubuntu Linux Installation

### Step 5: Create an Ubuntu Bootable USB

1. Download Ubuntu 22.04 LTS ISO.

```text
https://ubuntu.com
```

2. Create the bootable USB using:

- Rufus
- BalenaEtcher

3. Flash the ISO image to the USB drive.

✅ Result: Ubuntu installation media is ready.

---

### Step 6: Install Ubuntu

1. Boot the system from the Ubuntu USB drive.
2. Select:

```text
Try or Install Ubuntu
```

3. Choose:

```text
Install Ubuntu
```

4. Select:

```text
Normal Installation
```

5. Enable:

```text
Download updates while installing Ubuntu
```

6. Select one of the following options:

```text
Erase disk and install Ubuntu
```

or

```text
Custom Partition Layout
```

7. Configure:

- Hostname
- Username
- Password

8. Click **Install Now**.

Ubuntu will install and automatically configure the system.

> **⚠️ Warning**
>
> Selecting **Erase disk and install Ubuntu** permanently removes all existing data on the disk.

---

### Step 7: Perform Post-Installation Configuration

Update the operating system:

```bash
sudo apt update && sudo apt upgrade -y
```

Install common administrative tools:

```bash
sudo apt install openssh-server net-tools curl -y
```

Configure the hostname:

```bash
hostnamectl set-hostname nomura-ws01
```

Verify the hostname:

```bash
hostnamectl
```

> **Example**
>
> A standardized hostname convention helps uniquely identify systems within the corporate environment.
>
> ```text
> nomura-ws01
> nomura-ws02
> nomura-ws03
> ```

---

## 💡 Best Practice Tips

- Always perform a full disk format during a clean installation to avoid operating system conflicts and leftover configurations.
- Join the corporate domain immediately after installation before deploying business applications and policies.
- For deployments involving more than 10 devices, use image-based deployment solutions instead of manual installations.

Common solutions include:

```text
Microsoft Deployment Toolkit (MDT)
Windows Deployment Services (WDS)
```

- Enable BitLocker on all corporate laptops immediately after installation.
- Record asset information in the CMDB, including:
  - Device Serial Number
  - Hostname
  - Assigned User
  - Department
  - Installation Date

> **⚠️ Warning**
>
> Failure to document newly deployed devices can create inventory, audit, and support challenges later.

---

 
