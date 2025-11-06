# Active Directory Lab 1: Deploying a Domain Controller

### Goal
Set up a Windows Server 2022 machine as a Domain Controller and create a new Active Directory environment for centralized authentication and identity management.

---

### What I Did
- Installed **Active Directory Domain Services (AD DS)** and **DNS Server** roles.
- Promoted the server to a Domain Controller.
- Created a new Active Directory forest and domain: **lab.local**
- Verified the configuration using:
  - **Active Directory Users and Computers (ADUC)**
  - **DNS Manager**

---

### Lab Environment Setup
This lab was completed in a local virtualized environment:

- **Host OS:** Windows 11  
- **Virtualization:** VirtualBox  
- **Networking:** Internal Virtual Switch for isolated communication  

**Virtual Machines Involved:**
- **Windows Server 2022** (Domain Controller)

A Windows 11 client will be joined to this domain in the next lab.

---

### Why This Matters
Active Directory Domain Services is still the identity foundation in most organizations, even those that also use Microsoft 365 or Entra ID.  
On-prem AD manages devices, authentication, Group Policy, and internal resources, while Entra ID handles cloud identity and access.  
Understanding how to deploy and configure a Domain Controller is essential for roles in:

- Help Desk / Service Desk
- IT Support / Desktop Support
- Systems Administration
- Network Support

This lab establishes the *identity layer* that future labs will build on. It supports users, groups, Group Policy, client systems, permission structures, and shared resources. Everything starts from this point.

---

### Key Concepts Learned
| Concept | Explanation |
|--------|-------------|
| Domain Controller | The server responsible for authentication and identity services. |
| AD DS | Stores and organizes users, groups, and computers in a structured directory. |
| DNS Integration | AD relies on DNS to locate and communicate with domain services. |
| Forest / Domain Structure | The logical identity boundary for the environment. |

---

### Screenshots

> Screenshots are stored in the `screenshots/` folder.

![01 - Pre-AD-DS Server State](https://github.com/user-attachments/assets/c0202e9a-d2cf-4ce0-a6e0-37dc603f57f1)
_Starting state before configuring Active Directory roles._

![02 - Add Roles and Features - AD DS + DNS Selected](https://github.com/user-attachments/assets/abeff14d-f089-40c3-a2d7-f3d4da9dba68)
_AD DS and DNS selected for installation._

![03 - Post-Deployment - Promote Server to Domain Controller](https://github.com/user-attachments/assets/324692dd-d4dd-4f7d-adc0-f59b8807f23f)
_Beginning Domain Controller promotion._

![04 - Create New Domain - lab.local](https://github.com/user-attachments/assets/0adeeb5c-631f-4f80-8c0a-e39d69fa1d3e)
_Creating the new AD forest and domain._

![05 - Domain Controller Login Screen - lab\Administrator](https://github.com/user-attachments/assets/c3d21303-2f2a-4f56-85f7-39b984275d29)
_Confirmation that the server is now operating as a Domain Controller._


---

### Troubleshooting Notes / Lessons Learned
- Active Directory requires using the Domain Controller as the DNS source.  
  Using external DNS (like 8.8.8.8) will prevent a domain join.
- After changing DNS settings on the client, running `ipconfig /flushdns` helps clear old cached resolution.
- Verified AD DS health using Server Manager notifications and the ADUC console to ensure the domain was created properly.

---

### Next Lab
**Lab 2: Domain Controller + DNS**

We will:
- Promote the server to a Domain Controller
- Configure DNS forward and reverse lookup zones
- Ensure the domain is ready for clients to join
