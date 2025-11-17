# Lab 10 – Security Defaults, MFA, and Admin Account Hardening

## Overview
In this lab, I configured identity security for my Microsoft Entra tenant by:
- Disabling Security Defaults to support advanced Conditional Access policies.
- Registering MFA for my primary administrator accounts.
- Creating a proper *internal* global admin account (best practice: no external personal accounts as admins).
- Configuring a password-only Break Glass (BG Admin) account with no MFA methods.

This lab establishes the foundation for later Conditional Access and Zero Trust identity labs.

---

## Objectives
- Disable Microsoft Security Defaults.
- Register MFA for my main admin account(s).
- Resolve MFA registration issues by creating a correct internal admin account.
- Configure and validate a Break Glass administrator with **no MFA**.
- Confirm all authentication methods are applied correctly.

---

## Screenshots

### **01 – MFA prompt enforced due to Security Defaults**

<img width="1916" height="919" alt="01-entra-mfa-enforced-security-defaults" src="https://github.com/user-attachments/assets/f4e66ce4-e56c-4244-8b33-5455601053e2" />

**Screenshot:** `01-entra-mfa-enforced-security-defaults.png`

---

### **02 – Security Defaults configuration screen**

<img width="1919" height="917" alt="02-entra-security-defaults-screen" src="https://github.com/user-attachments/assets/25ffc685-8bd7-47ea-a852-2be9049d2e0c" />

**Screenshot:** `02-entra-security-defaults-screen.png`

---

### **03 – Security Defaults disabled**

<img width="1907" height="912" alt="03-entra-security-defaults-disabled" src="https://github.com/user-attachments/assets/4fd22e5c-2c01-4d28-90e5-91610be9944e" />

**Screenshot:** `03-entra-security-defaults-disabled.png`

---

### **04 – Authentication methods for the correct internal admin**

This is the correct internal administrator (`brian.admin@brianbaikgaoutlook.onmicrosoft.com`) showing successful MFA registration.

<img width="1918" height="916" alt="04-entra-user-auth-methods-brian-baik" src="https://github.com/user-attachments/assets/91f84ef0-56e5-4dde-9a47-c8b4270616e7" />

**Screenshot:** `04-entra-user-auth-methods-brian-baik.png`

---

### **05 – MFA registration success for original admin**

<img width="1919" height="915" alt="05-mfa-registration-success-brian-baik" src="https://github.com/user-attachments/assets/3e9225c5-3231-433b-a32a-0df4404ece12" />

**Screenshot:** `05-mfa-registration-success-brian-baik.png`

---

### **06 – MFA registration success for the new internal admin**

<img width="1918" height="921" alt="06-mfa-registration-success-brian-admin" src="https://github.com/user-attachments/assets/0e970b78-abf0-40a5-ba8b-3d5d336bc1cd" />

**Screenshot:** `06-mfa-registration-success-brian-admin.png`

---

### **07 – Break Glass Admin configured (no MFA methods)**

<img width="1919" height="918" alt="07-entra-bg-admin-no-mfa" src="https://github.com/user-attachments/assets/644d9b36-f4ba-45ba-8e6f-653f7542cbb3" />

**Screenshot:** `07-entra-bg-admin-no-mfa.png`

---

## Notes & Lessons Learned

### **1. External (#EXT#) accounts cannot be primary global admins**
My initial admin account was created as an external identity because it originated from a personal Outlook account.  
This caused MFA registration errors and blocked some authentication methods.

**Fix:**  
I created a proper internal cloud admin (`brian.admin@…`) and assigned Global Administrator.

This mirrors real enterprise environments where:
- Personal accounts are never admins  
- Admin identities are internal-only  
- MFA must be enforced consistently across cloud admins

---

### **2. Break Glass accounts must never have MFA**
This lab demonstrates the proper configuration:
- Strong password  
- No MFA  
- No authentication methods  
- This account will later be excluded from Conditional Access policies as part of a future lab

This is industry best practice for disaster recovery.

---

### **3. Security Defaults block advanced identity configurations**
Disabling them is required for:
- Conditional Access  
- MFA policies  
- Modern Zero Trust identity governance  
- Custom SSPR and authentication methods

---

## Outcome
At the end of this lab, my tenant has a fully aligned identity security baseline:
- MFA enforced for cloud admins  
- Correct internal admin accounts established  
- Break Glass admin validated  
- Security Defaults disabled  
- Tenant ready for advanced Conditional Access and Hybrid Identity labs

This completes the foundational identity hardening for my Microsoft Entra environment.

---

## Next Lab

**Lab 11 – Entra Connect Installation & Hybrid Identity Preparation**

In the next lab, I’ll install Microsoft Entra Connect on my domain controller, synchronize my on-prem Active Directory users to Entra ID, and begin building a practical hybrid identity environment. This sets the stage for:
- Hybrid Azure AD Join  
- Conditional Access targeting synced users  
- Intune device enrollment  
- Autopilot deployment  
- Cloud-based identity lifecycle testing  

Lab 11 is where my on-prem identity and cloud identity start working together.
