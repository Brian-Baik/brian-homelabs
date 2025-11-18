# Lab 12 – Hybrid Identity with Microsoft Entra Connect Sync
This lab demonstrates how to connect an on-premises Active Directory domain to Microsoft Entra ID using Entra Connect Sync. The goal is to enable hybrid identity and synchronize on-prem user accounts to the cloud.

---

## Environment
- Windows Server 2022 Domain Controller  
- Active Directory Domain Services and DNS  
- Domain: lab.local  
- Microsoft Entra tenant: brian.admin@brianbaikgaoutlook.onmicrosoft.com  
- Entra Connect Sync (latest installer from the Entra Admin Center)

---

## Screenshots
(Replace filenames with your actual screenshot names.)

1. Entra Connect Sync installation completed  
   `01-entra-connect-install-complete.png`
<img width="1918" height="1032" alt="01-entra-sync-install-complete" src="https://github.com/user-attachments/assets/95144c94-f165-4e82-922b-5353bd4af5b3" />

2. Synchronization Service Manager showing connectors  
   `02-entra-sync-service-connectors.png`
<img width="1919" height="1030" alt="02-sync-manager-connectors" src="https://github.com/user-attachments/assets/6cac7f0d-8c28-4e66-a2d4-1831d038cbec" />

3. Synchronization Service Manager showing successful sync operations  
   `03-entra-sync-service-operations.png`
<img width="1919" height="1029" alt="03-sync-manager-operations" src="https://github.com/user-attachments/assets/f19428eb-5663-4d7e-9622-1a9fd2cbf754" />

4. On-premises AD user in Active Directory Users & Computers  
   `04-onprem-ad-user.png`
<img width="1919" height="1031" alt="04-aduc-user" src="https://github.com/user-attachments/assets/2a00f2b1-7a70-49ef-a6cd-f20cfb309da4" />

5. Matching synced user in Microsoft Entra ID  
   `05-entra-synced-user.png`
<img width="1919" height="1031" alt="05-entra-synced-user" src="https://github.com/user-attachments/assets/2ad51f31-b818-4550-87ac-b87ef8f0b9ee" />

---

## Configuration Steps

### 1. Install Entra Connect Sync
Downloaded from the Entra Admin Center and ran using Express Settings. This installs the sync engine and required components.

### 2. Connect to Microsoft Entra ID
Signed in using: brian.admin@brianbaikgaoutlook.onmicrosoft.com

This authorizes the sync engine to communicate with the tenant.

### 3. Connect to AD DS
Entered the domain administrator account: LAB\Administrator

This allows the connector to read from on-prem AD during sync.

### 4. UPN Suffix Review
The wizard detected the following:

- Active Directory UPN suffix: lab.local  
- Microsoft Entra ID domain: Not Added  

Since this is a lab environment and the domain is not routable, continued without matching the UPN suffix.

### 5. Configuration Summary
Before installation, the wizard displayed the components it would configure, which included:

- Sync engine installation  
- Microsoft Entra ID connector  
- On-prem AD connector  
- Password hash synchronization  
- Auto upgrade  
- Sync services  

Selected Install to begin the process.

---

## Sync Results
After installation, the initial synchronization ran automatically.  
Verified in Synchronization Service Manager:

- Connectors were created  
- Import, sync, and export steps completed  
- Users from lab.local appeared in Microsoft Entra ID  

This confirmed that hybrid identity was configured correctly and synchronization was functioning.

---

## What I Learned
- How Entra Connect Sync links on-prem AD with Entra ID  
- How password hash sync works  
- How to review connectors and sync operations  
- How UPN suffix mismatches affect sign-in behavior  
- How to validate sync using Synchronization Service Manager  

---

## Lab Summary
This lab established hybrid identity by installing and configuring Microsoft Entra Connect Sync, connecting the on-prem AD domain to Entra ID, and verifying successful user synchronization.

## Next Lab
Now that Entra Connect Sync is running, the next step is to configure hybrid Azure AD join for the Windows 11 client. This will confirm that devices can register in both on-prem AD and Entra ID and will prepare the environment for Intune.
