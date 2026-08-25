# LAB 12: Printer Configuration Local Printers · LAN, Network Printers · Print Server

## 📘 Overview

Printer installation and troubleshooting are among the most common desktop support tasks in enterprise environments.

This lab covers:

- Installing local USB printers
- Installing network printers
- Connecting to shared printers via a Print Server
- Managing print queues
- Deploying printers using Group Policy (GPO)

---

## 🖨️ Part A: Add Local USB Printer

### Step 1: Connect and Install a Local Printer

1. Connect the printer to the computer using a USB cable.
2. Windows will automatically detect most modern printers and install the required drivers.

Navigate to:

```text
Settings → Devices → Printers & Scanners
```

3. Click:

```text
Add a printer or scanner
```

4. Wait while Windows searches for available printers.

If the printer is not detected:

1. Click:

```text
The printer that I want isn't listed
```

2. Proceed with manual installation.

> **💡 Tip**
>
> Always verify that the printer is powered on and connected before beginning troubleshooting.

---

### Step 2: Install Printer Driver Manually

If Windows cannot automatically install the printer:

1. Download the latest driver from the printer manufacturer's website.

Common vendors:

- HP
- Canon
- Epson
- Kyocera

2. Run the installation package.
3. Follow the Add Printer Wizard.
4. Select the printer port.

Example:

```text
USB001
```

5. Complete the installation.

### Print a Test Page

Navigate to:

```text
Printer Properties
```

Right-click the installed printer and select:

```text
Print Test Page
```

✅ Successful printing confirms that the installation is working correctly.

---

## 🌐 Part B: Add Network/LAN Printer

### Step 3: Add Printer Using IP Address

Navigate to:

```text
Settings → Printers & Scanners
```

1. Click:

```text
Add a printer or scanner
```

2. Select:

```text
The printer that I want isn't listed
```

3. Choose:

```text
Add a printer using TCP/IP address or hostname
```

Enter the hostname or IP address.

**Example:**

```text
10.0.1.210
```

> **Note**
>
> This IP address may be assigned through a DHCP Reservation configured in DHCP (refer to LAB 04).

Windows will:

- Detect the printer model
- Install the required driver
- Complete the setup automatically

### PowerShell Alternative

```powershell
Add-Printer -Name 'NomPrinter01' -DriverName 'HP Universal Printing PCL 6' -PortName '10.0.1.210'
```

---

### Step 4: Connect to a Shared Printer via Print Server

Open Run:

```text
Win + R
```

Enter the printer share path.

**Example:**

```text
\\NOMPS01\FinancePrinter
```

1. Right-click the printer.
2. Select:

```text
Connect
```

The printer and required drivers are automatically installed from the Print Server.

### PowerShell Alternative

```powershell
Add-Printer -ConnectionName '\\NOMPS01\FinancePrinter'
```

> **Example**
>
> Shared printers are commonly deployed for:
>
> - Finance Department
> - HR Department
> - Admin Department
> - Branch Offices

---

## 🖥️ Part C: Print Server Management

### Step 5: Open Print Management Console

Launch:

```text
printmanagement.msc
```

Navigate to:

```text
Print Servers → NOMPS01 → Printers
```

From this console, administrators can view:

- Installed printers
- Shared printers
- Print queues
- Driver status

Common Printer Statuses:

| Status | Meaning |
|----------|----------|
| Ready | Printer available |
| Printing | Active print job |
| Offline | Device unreachable |
| Error | Printer issue detected |

> **💡 Tip**
>
> Print Management provides a centralized interface for managing enterprise printer infrastructure.

---

### Step 6: Clear a Stuck Print Queue

If print jobs remain stuck:

#### Stop the Print Spooler Service

```cmd
net stop spooler
```

#### Delete Print Queue Files

```cmd
del /Q /F /S C:\Windows\System32\spool\PRINTERS\*.*
```

#### Start the Print Spooler Service

```cmd
net start spooler
```

✅ Existing stuck print jobs should be cleared.

> **⚠️ Warning**
>
> Clearing the print queue removes all pending print jobs for all users on that device or server.

---

### Step 7: Deploy Printers via Group Policy (GPO)

Open:

```text
Group Policy Management
```

Create or edit an existing GPO.

Navigate to:

```text
User Configuration → Windows Settings → Deployed Printers
```

Select:

```text
Add Printer
```

Enter the printer UNC path.

**Example:**

```text
\\NOMPS01\FinancePrinter
```

Click **OK** and link the GPO to the target Organizational Unit (OU).

When users log in, the printer is automatically installed.

> **Example**
>
> Users in the Finance OU automatically receive:
>
> ```text
> \\NOMPS01\FinancePrinter
> ```
>
> without requiring manual installation.

---

## 🔧 Common Printer Troubleshooting

### Printer Appears Offline

Verify:

- Printer is powered on
- Network cable is connected
- Printer IP address is reachable

Test connectivity:

```cmd
ping 10.0.1.210
```

---

### Print Jobs Stuck in Queue

Verify:

- Print Spooler service is running
- Queue is not paused
- Printer is online

Restart the spooler service if required.

---

### Driver Issues

Symptoms:

- Garbled output
- Missing print options
- Installation failures

Resolution:

- Remove the printer
- Download the latest driver
- Reinstall using manufacturer-supported drivers

---

### Unable to Connect to Shared Printer

Verify:

- Print Server availability
- Share permissions
- DNS resolution

Test access:

```cmd
ping NOMPS01
```

Open:

```text
\\NOMPS01
```

Ensure the printer share is accessible.

---

## 💡 Best Practice Tips

- Use a centralized Print Server whenever possible to simplify administration and driver management.
- Assign printers either:
  - Static IP Address
  - DHCP Reservation

This prevents printer connectivity issues caused by IP address changes.

- Before escalating printer incidents, check:
  - Toner or ink levels
  - Paper trays
  - USB/network cables
  - Printer status panel

These checks resolve a significant percentage of printer-related issues.

- Use Universal Print Drivers whenever supported.

Examples:

```text
HP Universal Printing PCL 6
```

```text
Kyocera Universal Driver
```

- Deploy departmental printers using Group Policy to ensure automatic installation and reconnection.

> **💡 Tip**
>
> GPO-deployed printers automatically reconnect after user logon and system restarts, making them the preferred deployment method in enterprise environments.

---

 
