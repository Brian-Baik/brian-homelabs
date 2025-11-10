# Lab 5 – File Shares and NTFS Permissions

**Goal**  
Create network file shares on the domain controller and control access using security groups. Verify that standard users have read-only access and the Helpdesk role has modify permissions.

---

## Environment

- **Domain:** lab.local
- **Domain Controller:** DC-01 (Windows Server 2022)
- **Client:** Windows 11 domain-joined
- **Accounts:**
  - `LAB\bbaik` (standard user)
  - `LAB\helpdesk.bbaik` (Helpdesk service account, member of **Helpdesk** security group)

## OU Structure

```
lab.local
└─ CORP
   ├─ Users
   ├─ Computers
   ├─ Groups
   └─ Service Accounts
```

- `helpdesk.bbaik` is in **Service Accounts**
- The **Helpdesk** security group is in **Groups**


## Share Layout

The central share directory was created at: C:\Shares

```
Subfolders:
C:\Shares\Public
C:\Shares\Helpdesk
C:\Shares\HR
```

---


---

## Permissions Configuration

### Share Permissions (Sharing tab)

| Folder   | Everyone | Helpdesk Group |
|---------|----------|----------------|
| Shared  | Read     | Read           |
| Helpdesk| Read     | Change         |
| HR      | Read     | (No Modify)    |

### NTFS Permissions (Security tab)

| Folder   | Domain Users (Read?) | Helpdesk Group | Resulting Effective Access |
|---------|-----------------------|----------------|----------------------------|
| Shared  | Read & Execute        | Read & Execute | Universal read-only share |
| Helpdesk| Read & Execute        | Modify         | Helpdesk can create/modify files |
| HR      | Read or No Access     | No Modify      | Reserved for later use |

> **Important:** Any direct permissions on the user `helpdesk.bbaik` were removed so that group membership is the **only** method of privilege escalation. This helps prevent privilege creep.

---

## Access Verification (Windows 11 Client)

| Account | Path | Expected | Result |
|--------|------|----------|--------|
| `LAB\bbaik` | `\\DC-01\Shared`   | Can read only | Confirmed ✅ |
| `LAB\bbaik` | `\\DC-01\Helpdesk` | Cannot modify | Confirmed ✅ |
| `LAB\helpdesk.bbaik` | `\\DC-01\Helpdesk` | Modify/create files allowed | Confirmed ✅ |
| `LAB\bbaik` | `\\DC-01\HR` | No edit capability | Confirmed ✅ |

This confirms **least privilege** and **RBAC** are correctly implemented.

---

## Screenshots

Stored in: /05-file-shares-and-ntfs/screenshots/
```
01-folder-structure.png
02-share-permissions.png
03-ntfs-permissions-helpdesk.png
04-access-denied-bbaik.png
05-access-allowed-helpdesk.png
```
---

## Skills Demonstrated

- Configuring Windows SMB shares
- Understanding and aligning **Share Permissions** vs **NTFS Permissions**
- Implementing **Role-Based Access Control**
- Verifying effective permissions using different user roles
- Removing direct-per-user ACL entries to prevent privilege creep

---

## Next Lab
**Lab 6 – Group Policy (GPO)**  
We will create and apply Group Policy Objects to manage workstation behavior and automate drive mapping.
