# Lab 4: Domain Users and Helpdesk Role Account

Goal:  
Create standard user accounts and a dedicated Helpdesk administrative account using consistent naming conventions and proper OU placement. This reflects real-world identity lifecycle and privilege separation practices.

---

## Why This Matters

Organizations do not use the built-in Administrator account for daily work.  
Instead, they separate identities into two categories.

| Account Type | Purpose | Example |
|-------------|---------|---------|
| Standard User Account | Daily login, workstation access, regular work | `bbaik` |
| Helpdesk or Administrative Account | Elevated permissions for support and administrative tasks | `helpdesk.bbaik` |

Separating regular identity and administrative identity reduces the risk of accidental privileged actions and limits impact in case of credential compromise. This is a widely used security standard in enterprise environments.

---

## Naming Convention

All users follow the first initial plus last name pattern.

| Display Name | Username (sAMAccountName) | UPN | OU Placement |
|--------------|---------------------------|------|--------------|
| Alex Rivera | `arivera` | `arivera@lab.local` | `CORP/Users` |
| Dana Perez | `dperez` | `dperez@lab.local` | `CORP/Users` |
| Jamie Chen | `jchen` | `jchen@lab.local` | `CORP/Users` |
| Jordan Lee | `jlee` | `jlee@lab.local` | `CORP/Users` |
| Michael Scott | `mscott` | `mscott@lab.local` | `CORP/Users` |
| Brian (Standard Account) | `bbaik` | `bbaik@lab.local` | `CORP/Users` |
| Brian (Helpdesk Account) | `helpdesk.bbaik` | `helpdesk.bbaik@lab.local` | `CORP/Service Accounts` |

The Helpdesk account is the only account with elevated rights.  
It was added to the Helpdesk security group located in: CORP/Groups/Helpdesk

---

## Directory Structure (Updated)

lab.local
CORP
Users
Computers
Groups
Helpdesk
Service Accounts
helpdesk.bbaik


---

## Skills Demonstrated

- Identity lifecycle management and account provisioning
- Separation of standard and administrative identity
- Consistent username and UPN formatting
- Accurate placement of objects in Organizational Units
- Group-based role assignment and security modeling

---

## Screenshots (to add)

`01-users-in-ou.png`  
Shows standard user accounts in CORP/Users

`02-helpdesk-account.png`  
Shows helpdesk.bbaik in CORP/Service Accounts

`03-helpdesk-group.png`  
Shows helpdesk.bbaik as a member of the Helpdesk group

Screenshots will be stored in the `screenshots` directory.
