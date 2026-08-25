# LAB 03: Citrix Gateway – Basics & Access Secure Remote Access | SSL VPN

## 📘 Overview

Citrix Gateway (formerly NetScaler Gateway) is a secure remote access solution that provides SSL VPN and ICA Proxy services for Citrix Virtual Apps & Desktops.

This lab covers:

- User access through Citrix Gateway
- Citrix Workspace App installation
- Reviewing active user sessions
- Reviewing session policies
- Basic troubleshooting procedures

---

## 🌐 Part A: Accessing Citrix Gateway

### Step 1: User Access via Web Browser

Users can access Citrix resources from any supported web browser using the Gateway URL:

```text
https://gateway.nomura.com
```

1. Enter your Active Directory (AD) username and password.
2. Complete Multi-Factor Authentication (MFA) using RSA Token or OTP (if configured).
3. After successful authentication, the Gateway displays published desktops and applications through:
   - Citrix Workspace App (Receiver)
   - HTML5 Browser Access

> **Note**
>
> Depending on organizational policy, users may be required to complete MFA before accessing any published resources.

---

### Step 2: Install Citrix Workspace App

Download the Citrix Workspace App from:

```text
https://www.citrix.com/downloads/workspace-app/
```

Installation Steps:

1. Download the installer.
2. Run the installation package.
3. Accept the End User License Agreement (EULA).
4. Complete the installation.

After installation:

1. Open a web browser.
2. Navigate to the Gateway URL.

```text
https://gateway.nomura.com
```

3. Launch published applications and desktops directly through Citrix Workspace App.

> **💡 Tip**
>
> Using the Citrix Workspace App provides a better user experience and performance than browser-based launches for most users.

---

## 🔐 Part B: Admin - Reviewing Sessions and Policies

### Step 3: Log in to Citrix ADC (NetScaler) GUI

Access the Citrix ADC (NetScaler) management interface:

```text
https://<ADC-NSIP>
```

Log in using:

```text
Username: nsroot
Password: <password>
```

> **⚠️ Warning**
>
> Ensure administrative credentials are secured and accessed only by authorized personnel.

---

### Step 4: Check Active User Sessions

Navigate to:

```text
NetScaler Gateway → Monitoring → ICA Sessions
```

Review the following session information:

- Connected users
- Session duration
- Client IP address

To disconnect an active session:

1. Select the user session.
2. Click **Disconnect**.

> **Example**
>
> If a user's session becomes unresponsive or remains connected after logout, administrators can manually disconnect the session from the ICA Sessions dashboard.

---

### Step 5: Review Session Policies

Navigate to:

```text
NetScaler Gateway → Policies → Session
```

Review the configured session policies, including:

- Policy expressions
- Access restrictions
- Session timeout settings

Example policy expression:

```text
CLIENT.OS(WIN)
```

The above policy can be used to allow access only from Windows operating systems.

Default timeout settings:

| Setting | Value |
|----------|---------|
| Idle Timeout | 30 Minutes |
| Session Limit | 8 Hours |

> **Note**
>
> Session policies help enforce security and compliance requirements for remote access users.

---

## 🔧 Part C: Basic Troubleshooting

### Step 6: User Cannot Connect - Checklist

Perform the following checks when troubleshooting user connection issues:

#### Verify Active Directory Account Status

Confirm the user account is not locked or disabled using:

```text
Active Directory Users and Computers
```

#### Verify SSL Certificate Status

Navigate to:

```text
SSL → Certificates
```

Confirm that:

- The certificate is valid
- The certificate is not expired
- The certificate chain is complete

#### Test Gateway URL

Open the Gateway URL in a browser:

```text
https://gateway.nomura.com
```

Review for:

- SSL certificate warnings
- Browser trust errors
- Accessibility issues

#### Review Citrix ADC Logs

Check authentication-related logs:

```bash
/var/nslog/ns.log
```

Review entries for:

- Authentication failures
- LDAP errors
- MFA failures
- Connection issues

> **💡 Tip**
>
> Authentication failures are commonly caused by locked AD accounts, expired passwords, invalid certificates, or MFA synchronization issues.

---

## 💡 Best Practice Tips

- Always use HTTPS with a valid SSL certificate. Never use HTTP in production environments.
- Enable Multi-Factor Authentication (MFA) using RSA Tokens or OTPs for all remote users.
- Configure idle session timeouts between 15 and 30 minutes to meet compliance requirements.
- Review gateway logs regularly for failed authentication attempts and suspicious activity.
- Keep Citrix Workspace App updated on all end-user devices.
- Regularly review and remove inactive Gateway access policies.
