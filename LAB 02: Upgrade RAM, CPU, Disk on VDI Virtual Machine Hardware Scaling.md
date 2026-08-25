# LAB 02: Upgrade RAM, CPU, Disk on VDI Virtual Machine Hardware Scaling

## 📘 Overview

Upgrading virtual hardware on a VDI machine is performed through the VMware vSphere Client rather than VMware Horizon.

This lab covers:

- RAM upgrades
- CPU upgrades
- Virtual Disk expansion
- Windows partition extension
- Linux partition extension
- Hot-add and cold-add upgrade methods

## 📋 Prerequisites

Before starting, ensure the following requirements are met:

- vSphere Client access

```text
https://<vCenter-IP>/ui
```

- VM must be powered off for cold upgrades
- Sufficient ESXi host resources available

---

## 🧠 Understanding Upgrade Types

| Upgrade Type | Description |
|-------------|-------------|
| Hot-Add | Hardware resources are added while the VM is powered on. |
| Cold-Add | Hardware resources are added while the VM is powered off. |

> **Note**
>
> Hot-add functionality requires VMware Tools to be installed and properly configured.

---

## ⚙️ Part A: Upgrade RAM

### Step 1: Open vSphere Client and Locate the VM

Open the vSphere Client:

```text
https://<vCenter-IP>/ui
```

Navigate to:

```text
Inventory → VMs
```

Search for the target virtual machine.

**Example:**

```text
NOMVDI-001
```

### Step 2: Edit VM Settings for Memory

1. Right-click the VM.
2. Select **Edit Settings**.
3. Navigate to **Memory**.
4. Change the memory value.

**Example:**

```text
4 GB → 8 GB
```

5. If the VM is running, verify that **Memory Hot Add** is enabled:

```text
VM Options → Advanced → Memory Hot Add
```

6. Click **OK**.

> **Note**
>
> RAM upgrades apply immediately when Hot-Add is enabled. Otherwise, the change takes effect after the next power cycle.

---

## ⚙️ Part B: Upgrade CPU

### Step 3: Edit VM Settings for CPU

1. Open **Edit Settings**.
2. Navigate to **CPU**.
3. Modify the number of virtual CPUs (vCPUs).

**Example:**

```text
2 vCPU → 4 vCPU
```

4. Enable CPU Hot Plug:

```text
VM Options → Advanced → CPU Hot Add
```

5. Verify NUMA topology when the number of vCPUs exceeds the physical cores available on the host.

> **⚠️ Warning**
>
> Improper CPU sizing may negatively impact VM performance and host resource utilization.

---

## 💾 Part C: Expand Disk Size

### Step 4: Extend the Virtual Disk in vSphere

1. Open **Edit Settings**.
2. Select **Hard Disk 1**.
3. Increase the virtual disk size.

**Example:**

```text
60 GB → 100 GB
```

4. Power off the VM if snapshots exist.

> **Important**
>
> Disk resizing requires the VM to be powered off when snapshots are present.

5. Click **OK**.

vSphere extends the VMDK file.

---

## 🪟 Part D: Extend Disk Partition Inside Windows VDI

### Step 5: Extend the Windows Partition

1. Log in to the VDI.
2. Open Disk Management.

```text
diskmgmt.msc
```

3. Right-click the **C:** drive.
4. Select **Extend Volume**.
5. Click **Next**.
6. Click **Finish**.

Verify that the C: drive displays the new size.

### Verify Using PowerShell

```powershell
Get-PSDrive C
```

---

## 🐧 Part E: Extend Disk Partition Inside Linux VDI

### Step 6: Extend the Linux Partition

Confirm the new disk size:

```bash
sudo fdisk -l
```

Extend the partition:

```bash
sudo growpart /dev/sda 1
```

Resize the filesystem:

```bash
sudo resize2fs /dev/sda1
```

> **Note**
>
> Commands may vary depending on the Linux distribution and filesystem type.

---

## 💡 Best Practice Tips

- Always create a snapshot before making any hardware changes. This enables quick rollback if issues occur.
- Schedule production VDI upgrades during off-hours such as nights or weekends.
- Document the before-and-after configuration changes (RAM, CPU, and Disk) in your CMDB or change management ticket.
- Ensure VMware Tools is installed and up to date to support Hot-Add functionality.
- Plan storage requirements carefully
