# LAB 13: Mail Monitoring & Ticket Assigning ITSM · ServiceNow · Monitoring Mailbox

## 📘 Overview

A key responsibility of L1 Support is monitoring shared support mailboxes, triaging user requests, creating incidents, and assigning tickets to the appropriate support teams.

This lab covers:

- Monitoring a support mailbox
- Categorizing incoming requests
- Creating incidents in ServiceNow
- Assigning tickets to the correct support teams
- Updating and closing tickets according to ITSM best practices

---

## 📬 Part A: Monitoring the Support Mailbox

### Step 1: Access the Shared Mailbox

#### Outlook Method

Navigate to:

```text
Outlook → File → Account Settings → Advanced → Add Shared Mailbox
```

Add the shared mailbox.

**Example:**

```text
helpdesk@nomura.com
```

#### Outlook Web Access (OWA) Method

Open Outlook Web Access and select:

```text
Open Another Mailbox
```

Enter:

```text
helpdesk@nomura.com
```

### Configure Mail Rules

To improve mailbox organization:

```text
Folder → Manage Rules & Alerts
```

Create rules to automatically sort incoming emails based on:

- Keywords
- Department
- Priority
- Assignment Group

> **💡 Tip**
>
> Well-designed mailbox rules reduce manual effort and help ensure critical issues are identified quickly.

---

### Step 2: Triage Incoming Requests

Review incoming emails and assign an appropriate priority level.

| Priority | Criteria | Example |
|-----------|-----------|-----------|
| P1 – Critical | Service outage affecting more than 100 users | Email server down |
| P2 – High | Business-critical user or service impacted | VPN not working for MD |
| P3 – Medium | Single user issue with available workaround | Printer offline |
| P4 – Low | General query or information request | How to set Out of Office (OOO)? |

> **⚠️ Important**
>
> Incorrect prioritization can lead to SLA breaches and delayed resolution of critical incidents.

---

## 🎫 Part B: Create a Ticket in ServiceNow

### Step 3: Log in to ServiceNow

Open:

```text
https://nomura.service-now.com
```

Log in using your Active Directory credentials.

---

### Step 4: Create an Incident Ticket

Navigate to:

```text
Service Desk → New Incident
```

Complete the required fields.

#### Caller

Search and select the affected user.

#### Category

Choose the appropriate category:

- Hardware
- Software
- Network
- Access

#### Short Description

Provide a clear, concise summary.

**Example:**

```text
Outlook not opening – Win11
```

#### Description

Include:

- Full issue description
- Error messages
- Business impact
- Troubleshooting steps already performed

#### Priority

Assign according to the triage matrix:

```text
P1
P2
P3
P4
```

#### Assignment Group

Examples:

```text
L1-Mumbai
```

```text
L2-Infrastructure
```

```text
Network Operations
```

Click:

```text
Submit
```

> **💡 Tip**
>
> A high-quality incident description reduces reassignment delays and speeds up resolution.

---

## 🔄 Part C: Assign Ticket to the Correct Team

### Step 5: Route the Ticket

Assign incidents based on the issue type.

| Issue Type | Assignment Group |
|------------|------------------|
| Network / VPN | L2-Network Team |
| Server / Active Directory | L2-Infrastructure |
| Application Bug | Application Support |
| Hardware | On-site Tech / Field Support |
| Security / Virus | Security Operations (SOC) |

> **Example**
>
> A user unable to connect to VPN should be assigned to:
>
> ```text
> L2-Network Team
> ```
>
> rather than Hardware or Application Support.

---

## 📝 Part D: Update and Close Ticket

### Step 6: Maintain Ticket Updates

Throughout the lifecycle of the incident:

- Add work notes regularly
- Record troubleshooting steps
- Document user communications
- Record escalation details if applicable

Example work note:

```text
Verified VPN configuration.
Reset user credentials.
Issue persists.
Escalated to L2-Network Team.
```

---

### Step 7: Resolve the Ticket

When the issue has been fixed:

1. Document the exact resolution.
2. Update Category and Subcategory fields.
3. Change the ticket status to:

```text
Resolved
```

4. Contact the user for confirmation.

If the user confirms resolution:

```text
Close
```

> **✅ Example Resolution**
>
> ```text
> Outlook profile recreated successfully.
> User verified email functionality.
> Incident resolved.
> ```

---

## 📋 Incident Lifecycle Workflow

A typical L1 ticket workflow should follow:

```text
Mailbox Monitoring
        ↓
Request Review
        ↓
Priority Assignment
        ↓
Ticket Creation
        ↓
Initial Troubleshooting
        ↓
Resolve or Escalate
        ↓
User Confirmation
        ↓
Ticket Closure
```

---

## 💡 Best Practice Tips

- Never leave a ticket unassigned. Every incident must have a clear owner.
- Update ticket work notes every 30 minutes during active P1 and P2 incidents.
- Use incident templates for recurring issues to improve consistency and efficiency.
- Always follow up with users before closing incidents.
- Ensure Category and Subcategory fields are completed correctly for reporting and trend analysis.
- Escalate early when issues exceed L1 scope rather than delaying resolution.
- Maintain clear and professional communication throughout the ticket lifecycle.

> **⚠️ Warning**
>
> Unassigned or poorly documented tickets are one of the most common causes of SLA breaches.

> **💡 Tip**
>
> Customer Satisfaction (CSAT) surveys are typically sent automatically after incident closure. Accurate updates and timely communication significantly improve user satisfaction scores.

---

