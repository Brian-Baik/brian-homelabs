# Windows / Hybrid Identity Homelab

This repository documents my Windows Server, Active Directory, DNS/DHCP, and Microsoft Entra ID homelab.

The goal of this lab is to build and document the kinds of support workflows used in real IT environments: identity, access, endpoint organization, network services, permissions, troubleshooting, and repeatable documentation.

I built this lab to strengthen my foundation beyond day-to-day desktop support and better understand the systems behind user accounts, device access, group policy, shared resources, and hybrid identity.

---

## Lab Goals

This homelab is designed to practice:

- Windows Server administration fundamentals
- Active Directory user, computer, group, and OU management
- DNS and DHCP configuration
- Group Policy-based endpoint configuration
- File share permissions using NTFS and share permissions
- Role-based access control using security groups
- Hybrid identity concepts with Microsoft Entra ID
- Entra Connect Sync setup and validation
- Troubleshooting and documentation habits used in real support environments

The focus is not just to “make it work,” but to verify each result and document the process clearly enough that someone else could follow it.

---

## Current Lab Environment

### Core Infrastructure

- Windows Server 2022 domain controller
- Active Directory Domain Services
- DNS
- DHCP
- Windows 11 client device
- VirtualBox virtualization

### Directory Structure

The lab includes a structured Active Directory environment with:

- Users
- Computers
- Groups
- Service accounts
- Standard user accounts
- Helpdesk/admin account separation
- Organized OUs for cleaner management

### Access and Permissions

Configured examples include:

- Shared network folders
- NTFS permissions
- Share permissions
- Security group-based access
- Group Policy drive mappings
- Item-level targeting for mapped drives

The goal is to avoid one-off permission creep and practice cleaner role-based access.

---

## Completed Lab Work

### Active Directory and Windows Server

- Built a Windows Server 2022 domain environment
- Promoted a domain controller
- Configured AD DS, DNS, and DHCP
- Created a clean OU structure for users, computers, groups, and service accounts
- Created standard and helpdesk-style accounts
- Configured security groups for access control
- Created shared folders using NTFS and share permissions
- Configured Group Policy drive mappings with item-level targeting

### DNS and DHCP

- Configured DNS for domain name resolution
- Configured DHCP scopes
- Enabled dynamic DNS update behavior
- Validated name resolution and address assignment
- Practiced troubleshooting network service behavior from the client side

### Microsoft Entra ID and Hybrid Identity

- Created and configured a Microsoft Entra ID tenant
- Created cloud users, roles, and groups
- Configured Entra Connect Sync
- Validated hybrid identity sync behavior
- Worked through Hybrid Azure AD Join concepts and validation

### Troubleshooting

One of the most useful labs involved troubleshooting an Entra sign-in issue caused by domain controller time drift.

The troubleshooting process included:

- Testing multiple browsers
- Checking DNS behavior
- Validating outbound HTTPS access
- Reviewing service dependencies
- Checking time synchronization
- Identifying domain controller clock drift as the root cause

This lab was especially useful because it connected a simple infrastructure issue to a real authentication failure.

---

## Documentation Approach

Each lab is documented with:

- A clear goal
- Required environment/context
- Step-by-step configuration
- Screenshots
- Verification steps
- Notes on what went wrong or what needed troubleshooting
- A short explanation of why the lab matters in real IT support

I try to write documentation that is useful to someone else, not just notes for myself.

---

## What This Lab Demonstrates

This repository is meant to show practical understanding of:

- Windows Server fundamentals
- Active Directory structure and account management
- DNS/DHCP support concepts
- Group Policy basics
- Shared folder access and permission troubleshooting
- Hybrid identity foundations
- Entra Connect Sync concepts
- Troubleshooting methodology
- Technical documentation

It is not meant to claim production-level systems administration experience. It is a structured learning environment built to reinforce the systems I want to support professionally.

---

## What I’m Working On Now

Current focus areas:

- Improving documentation quality and consistency
- Strengthening Network+ fundamentals
- Continuing Microsoft Entra ID and hybrid identity study
- Building stronger endpoint support and troubleshooting workflows
- Connecting homelab concepts back to real desktop support scenarios

---

## Planned Roadmap

These are planned areas of study and are not listed as completed experience yet:

- Microsoft 365 administration fundamentals
- Endpoint management concepts
- Ticketing and change-control workflows
- pfSense firewall and VLAN segmentation
- PowerShell scripting for repeatable admin tasks
- More structured troubleshooting scenarios

I include this roadmap to show the direction of the lab, not to claim these areas as finished work.

---

## Background

I currently work as a Desktop Support Technician contracted to Chicago Public Schools, supporting multiple school sites across high school and K-8 environments.

My day-to-day work includes endpoint support, imaging, break/fix repairs, asset inventory, printer connectivity, classroom technology support, and staff requests. That field experience gives me practical exposure to the front end of IT support.

This homelab is where I study the back end: identity, Windows infrastructure, access control, network services, and the systems that support users and devices at scale.

Before my current role, I worked in MSP support focused on VoIP, UCaaS, and Microsoft Teams Voice. That experience helped build my foundation in ticket triage, documentation, escalation, and user communication.

---

## How to Use This Repository

Start with the numbered lab folders.

Each lab is intended to be readable on its own, but the general progression is:

1. Build the Windows Server environment
2. Configure Active Directory, DNS, and DHCP
3. Add users, groups, computers, and OUs
4. Configure permissions and Group Policy
5. Validate access from a Windows client
6. Expand into Microsoft Entra ID and hybrid identity concepts
7. Document troubleshooting scenarios and lessons learned

---

Thanks for taking the time to look.

**Brian**
