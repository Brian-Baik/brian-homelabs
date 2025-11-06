# Lab 2 – Domain Controller + DNS Configuration

**Goal:**  
Promote the Windows Server to a Domain Controller and configure DNS so the domain can perform name resolution for authentication and network services.

---

## What I Did

1. Installed the **Active Directory Domain Services (AD DS)** role.
2. Installed the **DNS Server** role (required for AD to function).
3. Promoted the server to a Domain Controller and created the new domain: lab.local
4. Rebooted and logged in using the domain administrator account: LAB\Administrator

---

## Why This Matters

Active Directory relies on **DNS** to locate domain resources.  
If DNS is misconfigured, clients will fail to:

- Join the domain
- Authenticate with the domain controller
- Apply Group Policy

To ensure proper identity resolution, two DNS zones were configured:

| Zone Type | Purpose | Example |
|----------|---------|---------|
| **Forward Lookup Zone** | Resolves hostname → IP address | `dc01.lab.local → 192.168.56.10` |
| **Reverse Lookup Zone** | Resolves IP address → hostname | `192.168.56.10 → dc01.lab.local` |

**Forward = “Who is this hostname?”**  
**Reverse = “Who owns this IP?”**

The reverse lookup zone also supports:
- Kerberos authentication
- Remote management tools
- Accurate event logging and monitoring

---

## Verification

- `lab.local` appears in **Active Directory Users and Computers**
- Forward Lookup Zone contains A records for the domain controller and the client
- Reverse Lookup Zone contains PTR records confirming IP → hostname resolution

---

## Screenshots

| File | Description |
|------|-------------|
| `01-Server-Manager-Domain-Confirmed.png` | Confirms AD DS + DNS roles installed and server joined to `lab.local`. |
| `02-DNS-Forward-Lookup-Zone-lab-local.png` | Shows name → IP resolution. |
| `03-DNS-Reverse-Lookup-Zone-PTR-Records.png` | Shows IP → name resolution. |
