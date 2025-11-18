# Lab 11 – Fixing Entra ID Login Loop on the Domain Controller (Time Sync Issue)
*No screenshots – issue had to be fixed live.*

## Overview
While trying to sign in to Entra ID from the Domain Controller, the login page kept flickering, refreshing, and eventually showed:

> “We couldn’t sign you in. Please try again.”

Both Edge and Chrome had the same problem.  
DNS worked. Internet worked. Nothing obvious was broken.  
This lab explains how the issue was found and fixed.

---

## Why There Are No Screenshots
This issue was diagnosed live on an active DC.  
Capturing screenshots risked interrupting the authentication loop and breaking the sign-in test flow.

This lab documents the troubleshooting steps and final solution clearly without images.

---

## Environment
- Windows Server 2022 Domain Controller  
- Active Directory Domain Services + DNS  
- VirtualBox networking (NAT + Host-Only)  
- Browsers: Microsoft Edge & Google Chrome  
- Entra tenant admin:  
  `brian.admin@brianbaikgaoutlook.onmicrosoft.com`

---

## Symptoms
- Microsoft login page flickers nonstop  
- Endless redirect loop  
- Generic error eventually displays  
- Happens in Edge *and* Chrome  
- InPrivate mode does nothing  
- DNS resolves correctly  
- Internet connectivity is fine  
- Firewall and SmartScreen not blocking anything  

This suggested the problem was deeper than a browser or DNS issue.

---

## Key Observation
Checking system time sync revealed the Domain Controller was using:

**Local CMOS Clock**

instead of an external NTP time source.

A DC using its CMOS clock will drift over time.  
Even a **1–2 minute drift** breaks Microsoft cloud authentication.

This causes:
- Redirect loops  
- Flicker on login.microsoftonline.com  
- Token timestamp failures  
- Silent authentication errors  

This matched the behavior exactly.

---

## Fixing the Problem

### 1. Enable the Windows Time Service
```powershell
Set-Service w32time -StartupType Automatic
Start-Service w32time
```

### 2. Configure a real external time source
```powershell
w32tm /config /manualpeerlist:"time.windows.com,0x9" /syncfromflags:manual /reliable:yes /update
```

### 3. Force a time sync
```powershell
w32tm /resync /force
```

### 4. Verify it worked
```powershell
w32tm /query /status
```

Expected:
- **Source:** time.windows.com  
- **NOT** Local CMOS Clock

Once the DC clock aligned with a valid external source, Entra login immediately started working.

---

## Result
After proper NTP sync:

- No more flickering  
- Login.microsoftonline.com redirected normally  
- Authentication completed instantly  
- Chrome and Edge both worked  
- Entra ID login succeeded on the first try  

The entire issue was caused by time drift on the Domain Controller.

---

## Root Cause
- Windows Time Service was not configured  
- DC was relying on Local CMOS Clock  
- System time was drifting  
- OAuth tokens were invalid  
- Entra ID authentication looped endlessly  

Fixing time synchronization resolved the issue completely.

---

## Skills Demonstrated
- Troubleshooting cloud authentication failures  
- Understanding the role of time sync in identity  
- Configuring Windows Time Service  
- Practical problem isolation (DNS → browser → OS → identity)  
- Fixing real-world Entra login issues on a domain controller  

---

## Outcome
The Domain Controller now:
- Syncs with time.windows.com  
- Supports Entra login normally  
- Avoids future token timestamp issues  
- Is ready for hybrid identity + Entra Connect

This was a high-value troubleshooting experience demonstrating practical IT problem-solving under real conditions.
