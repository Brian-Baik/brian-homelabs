# Lab 3 – Active Directory Organizational Unit Structure

**Goal:**  
Establish a clean and maintainable Active Directory structure by organizing objects into appropriate Organizational Units (OUs). This mirrors how real organizations manage users, devices, and permissions at scale.

---

## Why This Matters

Active Directory becomes difficult to manage if everything is stored in the default **Users** and **Computers** containers.  
A clear OU structure:

| Benefit | Description |
|--------|-------------|
| **Maintainability** | Easier tracking of users, systems, and permissions. |
| **Security** | Enables precise scoping of Group Policy and access control. |
| **Professional Standard** | Reflects how real enterprise AD is organized. |
| **Foundation for Future Labs** | Required for Group Policy, file share permissions, and workstation management. |

This lab prepares the environment for **user lifecycle management, least privilege access, and GPO configuration** in later labs.

---

## What I Did

1. Opened **Active Directory Users and Computers** (`dsa.msc`).
2. Enabled **View → Advanced Features** to expose full object settings.
3. Created a top-level OU named: CORP
4. Under **CORP**, created the following structured sub-OUs:

- lab.local (Domain)
  - CORP (Root Organizational Unit)
    - Users
    - Computers
    - Groups
    - Service Accounts

5. Moved previously created user accounts and a Helpdesk security group into their appropriate OUs.
6. Enabled **“Protect object from accidental deletion”** on CORP and its sub-OUs to prevent accidental removal during administrative operations.

---

## OU Structure (Final)

- lab.local (Domain)
  - CORP (Root Organizational Unit)
    - Users
    - Computers
    - Groups
    - Service Accounts

---

## Screenshots

| File | Description |
|------|-------------|
| `01-OU-Tree.png` | CORP OU structure expanded in ADUC. |
| `02-OU-Properties.png` | Protection against accidental deletion enabled. |

Screenshots are located in the `screenshots/` folder.

---

## Skills Demonstrated

- Active Directory structure planning
- Navigating and administering ADUC
- Understanding directory object hierarchy
- Preparing AD for Group Policy and access control workflows
- Following enterprise identity and endpoint management standards

---

## Next Lab

**Lab 4 – Domain Users & Naming Conventions**

I will:

- Create user accounts using a consistent naming standard
- Place accounts in the correct OU
- Prepare for domain workstation joins and Group Policy management

