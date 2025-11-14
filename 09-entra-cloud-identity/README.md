# Lab 9: Entra ID Cloud Users, Roles, and Groups

## Overview
This lab sets up the basic cloud identity structure for the rest of the hybrid and Intune labs. I created cloud-only accounts, assigned directory roles, and built foundational security groups. These objects will be used for MFA, Intune enrollment, device management, Autopilot, Conditional Access, and the upcoming hybrid identity integration with on-prem Active Directory.

---

## Tasks Completed

### 1. Created cloud-only users
I created the following accounts in Entra ID:

- Brian Baik (Global Admin)
- John Admin (Privileged Role Administrator)
- Helpdesk Tech
- David User
- Sarah User
- Device Enrollment

These accounts reflect a typical small organization: admins, helpdesk, standard employees, and a device enrollment identity for Intune and Autopilot.

---

### 2. Assigned directory roles
Roles were assigned according to least privilege:

| User | Role |
|------|------|
| Brian Baik | Global Administrator |
| John Admin | Privileged Role Administrator |
| Helpdesk Tech | Helpdesk Administrator |
| Device Enrollment | Standard user (will receive enrollment roles later) |
| David and Sarah | Standard users |

This establishes proper separation between full admins, helpdesk operators, and regular users.

---

### 3. Created core security groups
These groups match real identity architecture and will be used later for policy scoping, device management, and Conditional Access.

- **Cloud-Admins**  
  Members: Brian Baik, John Admin  
  Description: Administrative group for Entra ID and cloud services. Used for high privilege accounts only.

- **Helpdesk-Techs**  
  Members: Helpdesk Tech  
  Description: Helpdesk and support staff with delegated permissions for user support and basic administration.

- **Standard-Users**  
  Members: David User, Sarah User  
  Description: Regular user accounts for MFA testing, policy enforcement, and device enrollment scenarios.

- **Device-Enrollment-Admins**  
  Members: Device Enrollment  
  Description: Used for Windows device enrollment, Autopilot testing, and Intune onboarding.

---

## Screenshots
Screenshots for this lab are stored in the `/screenshots` folder.

1. `01-entra-users-list`
2. `02-entra-brian-assigned-roles`
3. `03-entra-john-assigned-roles`
4. `04-entra-groups-list`
5. `05-entra-group-members-cloud-admins`

---

## Lab Summary
This lab created the cloud identity foundation for the rest of the project. With users, roles, and groups in place, the tenant is now ready for the next steps:

- MFA and security defaults
- Intune MDM setup
- Autopilot preparation
- Hybrid Azure AD Join
- Directory synchronization with Entra Connect
- Conditional Access testing

This completes the cloud identity preparation for the hybrid environment.

### Why role assignments matter
Even though I use a Global Administrator account in this homelab, the role assignments in this lab mirror how identity is structured in real organizations. Production environments follow the principle of least privilege. Only dedicated admin accounts receive high-level roles, and day-to-day accounts use lower privilege permissions.

Assigning specific directory roles in this lab demonstrates:

- a realistic separation between full admin and helpdesk access  
- delegated permissions for support tasks  
- a structure that will be used later for Conditional Access testing  
- proper organization of responsibilities across identities  

This makes the lab environment behave like a real cloud tenant even though I am using a global admin account for setup and testing.
