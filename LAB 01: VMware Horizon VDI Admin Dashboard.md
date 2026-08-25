# LAB 01: VMware Horizon VDI Admin Dashboard

## 📘 Overview

VMware Horizon is a VDI platform that allows IT administrators to provision, manage, and monitor virtual desktops from a centralized dashboard.

This lab covers:

- Adding a new machine
- Assigning a machine to a user
- Deleting unused desktops
- Rebuilding a corrupt VDI

## 📋 Prerequisites

- VMware Horizon Connection Server installed and reachable
- Active Directory domain-joined environment
- vSphere/ESXi host with available resources
- Horizon administrator credentials

---

## 🔐 Part A: Logging into Horizon Admin Console

### Step 1: Open Horizon Admin Console

Open a web browser and navigate to:

```text
https://<ConnectionServer-IP>/admin
```

Log in using:

```text
DOMAIN\username
```

### Step 2: Navigate to Desktop Pools

Navigate to:

```text
Inventory → Desktops → Select your Desktop Pool
```

**Example:**

```text
NomuraVDI-Pool
```

---

## ⚙️ Part B: Adding a New Machine to Pool

### Step 3: Add Machine to Desktop Pool

1. Right-click the Desktop Pool.
2. Select **Edit**.
3. Open **Provisioning Settings**.
4. Click **Add Machines**.
5. Select an available vSphere VM.
6. Configure the naming pattern:

```text
NOMVDI-{n:fixed=3}
```

7. Click **OK**.

> **Note**
>
> Horizon automatically clones and registers the selected VM.

### Step 4: Assign Machine to User

1. Select the newly added machine.
2. Right-click and select **Assign User**.
3. Search for the required Active Directory user.

**Example:**

```text
vinod.muleva@nomura.com
```

4. Click **OK**.

---

## 🗑️ Part C: Deleting a Machine

### Step 5: Remove Machine from Pool

1. Select the machine.
2. Right-click **Remove from Inventory**.
3. Choose:

- **Delete from Disk**
- **Remove from Pool Only**

4. Confirm deletion.

> **⚠️ Warning**
>
> Selecting **Delete from Disk** permanently removes the virtual machine.

---

## 🔄 Part D: Rebuilding a Machine

### Step 6: Rebuild a Corrupt VDI

1. Select the affected machine.
2. Right-click **Recover**.
3. If the machine is corrupt:
   - Delete the machine.
   - Re-provision from the Master Snapshot.
4. Reassign the user after the rebuild is complete.

---

## 💡 Best Practice Tips

- Take a snapshot of the Master Image before provisioning new machines.
- Use consistent naming conventions.

**Example:**

```text
NOM-VDI-{dept}-{n}
```

- Schedule rebuild activities during maintenance windows.
- Enable Horizon Event Database for auditing.
- Use Smart Policies to automate user settings.
