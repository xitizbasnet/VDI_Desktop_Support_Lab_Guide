# LAB 10: Hardware Troubleshooting & Replacement RAM · HDD · GPU · PSU · Keyboard · Battery

## 📘 Overview

Hardware troubleshooting is a fundamental desktop support skill that involves identifying, diagnosing, and replacing faulty hardware components while minimizing downtime and preventing data loss.

This lab covers:

- Windows diagnostic tools
- Hardware error identification
- RAM troubleshooting and replacement
- HDD/SSD diagnostics and replacement
- GPU troubleshooting
- Keyboard, mouse, and USB troubleshooting

---

## 🔍 Part A: Diagnostic Tools

### Step 1: Run Built-in Windows Diagnostics

Use the following built-in Windows tools to diagnose hardware-related issues.

#### Memory Diagnostic

```cmd
mdsched.exe
```

#### Disk Check

```cmd
chkdsk C: /f /r /x
```

#### System File Checker

```cmd
sfc /scannow
```

#### System Hardware Information

```cmd
msinfo32
```

> **💡 Tip**
>
> Always run software-based diagnostics before replacing physical hardware components.

---

### Step 2: Check Event Viewer for Hardware Errors

Open Event Viewer:

```text
eventvwr
```

Navigate to:

```text
Windows Logs → System
```

Review for common hardware-related events:

| Event Type | Description |
|------------|-------------|
| Disk Errors | Event ID 7, 11 |
| Memory Errors | Event ID 1 |
| WHEA Errors | Hardware-related failures and warnings |

> **Note**
>
> Repeated disk or WHEA errors often indicate failing hardware and should be investigated immediately.

---

## 🧠 Part B: RAM Replacement

### Step 3: Identify Faulty RAM

Run Windows Memory Diagnostic:

```cmd
mdsched.exe
```

Select:

```text
Restart now and check for problems
```

Alternatively, use:

```text
MemTest86
```

Boot using a MemTest86 USB drive and perform 1–2 complete passes.

Common indicators of faulty RAM:

- Frequent Blue Screen of Death (BSOD)
- Random system crashes
- Application instability
- System freezes

Example BSOD:

```text
MEMORY_MANAGEMENT
```

> **💡 Tip**
>
> Intermittent crashes are often more difficult to diagnose than complete failures. Use extended memory testing whenever possible.

---

### Step 4: Replace RAM Module

1. Power off the computer.
2. Disconnect the power cable.
3. Hold the power button for approximately 5 seconds to discharge residual electricity.
4. Ground yourself using an anti-static wrist strap (recommended).
5. Open the system chassis.
6. Press the RAM retention clips outward.
7. Remove the existing RAM module.
8. Insert the replacement RAM module.
9. Press firmly until the retention clips lock into place.
10. Power on the machine.

Verify memory detection:

```text
Task Manager → Performance → Memory
```

> **⚠️ Warning**
>
> Mixing RAM modules with different speeds or specifications can cause performance and stability issues.

---

## 💾 Part C: HDD / SSD Replacement

### Step 5: Diagnose a Failing HDD

Check the SMART status of the disk.

```cmd
wmic diskdrive get status
```

Alternatively, use:

```text
CrystalDiskInfo
```

SMART Status Results:

| Status | Action |
|----------|----------|
| Good | No action required |
| Caution | Monitor closely |
| Bad | Replace immediately |

> **⚠️ Warning**
>
> A SMART status of "Bad" indicates a high risk of disk failure and potential data loss.

---

### Step 6: Replace HDD or SSD

Before replacing the drive:

✅ Backup all critical data.

Replacement Procedure:

1. Power off the computer.
2. Remove the existing drive.

Examples:

- SATA HDD
- SATA SSD
- M.2 SSD

3. Install the replacement drive.
4. Connect required cables.

For SATA drives:

- Power Cable
- Data Cable

For M.2 drives:

- Insert into M.2 slot
- Secure with retaining screw

5. Reinstall the operating system.

Refer to:

```text
LAB 05 – Operating System Installation
```

Alternatively:

- Restore from backup image
- Restore from enterprise deployment solution

> **Example**
>
> Organizations commonly restore systems using SCCM, MDT, or backup imaging solutions rather than performing manual installations.

---

## 🖥️ Part D: Other Component Checks

### Step 7: Troubleshoot GPU or Display Issues

When no display is available:

1. Test using a known-good monitor.
2. Test with a known-good display cable.
3. Verify display input selection.
4. Confirm monitor power status.

Check graphics drivers:

```text
Device Manager → Display Adapters
```

Available actions:

- Update Driver
- Roll Back Driver
- Reinstall Driver

Common indicators of GPU problems:

- Screen artifacts
- Screen flickering
- Driver crashes
- Black screens

If overheating is suspected:

- Power off the system.
- Remove and reseat the GPU in the PCIe slot.
- Verify cooling fans are operational.

> **💡 Tip**
>
> Always eliminate monitor and cable issues before replacing a graphics card.

---

### Step 8: Keyboard, Mouse, or USB Device Not Detected

Perform the following troubleshooting steps:

#### Check Hardware Connectivity

- Test a different USB port.
- Test the device on another computer.
- Verify cable integrity.

#### Reinstall USB Controllers

Navigate to:

```text
Device Manager → Universal Serial Bus Controllers
```

1. Uninstall the USB controllers.
2. Restart the computer.

Windows will automatically reinstall the drivers.

#### Wireless Device Troubleshooting

Verify:

- Battery status
- USB receiver connection
- Bluetooth pairing
- Device re-pairing process

> **Example**
>
> Many wireless keyboard and mouse issues are resolved simply by replacing batteries and re-pairing the device.

---

## 🔋 Additional Hardware Checks

### Power Supply Unit (PSU)

Common symptoms of PSU failure:

- Random shutdowns
- No power
- Reboot loops
- Burning smell
- No LED indicators

Checks:

- Verify power cable connection.
- Test power outlet.
- Test with a known-good PSU.

### Laptop Battery

Common battery-related issues:

- Not charging
- Rapid discharge
- Unexpected shutdowns

Verification Steps:

```text
Settings → Power & Battery
```

or

```cmd
powercfg /batteryreport
```

Generate a battery health report:

```cmd
powercfg /batteryreport
```

---

## 💡 Best Practice Tips

- Always raise a change request before replacing hardware on production systems.
- Photograph the internal hardware layout before disassembly to assist during reassembly.
- Record all replaced components in the asset management system.

Track:

- Serial Number
- Asset Tag
- Replacement Date
- Replacement Reason
- Technician Name

- Maintain spare inventory for commonly replaced items such as:
  - RAM
  - SSDs
  - Keyboards
  - Mice
  - Docking Stations

- Follow proper ESD (Electrostatic Discharge) procedures whenever handling internal components.

> **⚠️ Warning**
>
> Electrostatic discharge can permanently damage hardware components even when no visible damage is present.

---

## ✅ Verification Checklist

### Diagnostics

- [ ] Windows diagnostics completed successfully.
- [ ] Event Viewer logs reviewed.
- [ ] Hardware fault identified.

### RAM

- [ ] Memory test completed.
- [ ] RAM successfully replaced.
- [ ] New memory detected by Windows.

### HDD / SSD

- [ ] SMART status reviewed.
- [ ] Data successfully backed up.
- [ ] Storage device replaced successfully.
- [ ] Operating system restored or reinstalled.

### GPU

- [ ] Display functionality verified.
- [ ] Driver status confirmed.
- [ ] GPU operating normally.

### Peripheral Devices

- [ ] Keyboard functioning correctly.
- [ ] Mouse functioning correctly.
- [ ] USB devices detected.

### Documentation

- [ ] Asset records updated.
- [ ] Replacement information documented.
- [ ] Change request completed.

---
