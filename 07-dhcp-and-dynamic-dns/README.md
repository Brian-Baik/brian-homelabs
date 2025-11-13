# Lab 7: DHCP and Dynamic DNS Integration

## Overview
In this lab I configured DHCP on my domain controller so Windows clients in the `lab.local` domain automatically receive IP settings and register their A and PTR records in DNS. This builds on earlier labs where I set up Active Directory, DNS, and a Windows 11 domain-joined client.

The goal was to replace static IP assignments with a centralized DHCP scope and confirm DNS updates work in both forward and reverse lookup zones.

## Environment
- **Domain:** lab.local
- **Domain Controller:** DC-01  
  - IPv4: 192.168.56.10  
  - DNS Server  
  - DHCP Server  
- **Windows 11 Client:** Win11-CLI01  
  - Receives IP from DHCP
- **Network:** 192.168.56.0 /24 (Host-only network for AD traffic)

## Objectives
- Install the DHCP Server role on DC-01
- Authorize DHCP in Active Directory
- Create a DHCP scope for the 192.168.56.0 network
- Configure DNS settings inside DHCP
- Enable secure dynamic DNS updates
- Test DHCP leasing on the Windows 11 client
- Verify A and PTR records are created automatically

## Step 1: Verify DC-01 Network Settings
Confirmed that DC-01 uses 192.168.56.10 on the internal network where DHCP will run.

**Screenshot:**

`01-dc-ipconfig.png`

<img width="1919" height="1028" alt="01-dc-ipconfig" src="https://github.com/user-attachments/assets/9c070847-7cfc-4b94-b428-f166bca39b5e" />


## Step 2: Install DHCP Server Role
Installed the DHCP Server role from Server Manager and prepared it for AD authorization.

**Screenshot:**  

`02-install-dhcp-role.png`

<img width="1911" height="1025" alt="02-install-dhcp-role" src="https://github.com/user-attachments/assets/dfabc77c-0fa8-4b13-baf8-76f253b27a95" />


## Step 3: Authorize DHCP in Active Directory
Ran the post-install wizard to authorize DC-01 as a DHCP server inside the domain.

**Screenshot:**  

`03-authorize-dhcp-server.png`

<img width="1914" height="1027" alt="03-authorize-dhcp-server" src="https://github.com/user-attachments/assets/8c7170ee-a94c-498c-b47d-0c4261fd4569" />

## Step 4: Create the DHCP Scope
Created a new scope for lab clients:

- IP range: 192.168.56.50 to 192.168.56.200  
- Subnet mask: 255.255.255.0  
- No default gateway (host-only network)  
- DNS server: 192.168.56.10  
- DNS domain name: lab.local

**Screenshot:**  
`04-create-scope.png`

<img width="1916" height="1031" alt="04-create-scope" src="https://github.com/user-attachments/assets/e6ee71a1-65a4-4871-8dcf-3d3e076cea1e" />

Reviewed scope options to confirm DNS values were correct.

**Screenshot:**  
`05-scope-options.png` 

<img width="1919" height="1031" alt="05-scope-options" src="https://github.com/user-attachments/assets/1ff9c294-0e8b-41dd-9888-29bdaa05ac25" />

## Step 5: Enable Dynamic DNS Updates
Configured DHCP to always update A and PTR records and to remove them when leases expire.

**Screenshot:**  
`06-dns-tab-settings.png`

<img width="1917" height="1029" alt="06-dns-tab-settings" src="https://github.com/user-attachments/assets/4b86ef32-db77-4149-9403-e559bce10c61" />

## Step 6: Configure the Windows 11 Client for DHCP
Switched Win11-CLI01 from static IP to automatic assignment, then ran:
ipconfig /release
ipconfig /renew


Client received an address from the new scope and used the DC as its DNS server.

**Screenshot:**  
`07-client-ipconfig.png`

<img width="1919" height="1029" alt="07-client-ipconfig" src="https://github.com/user-attachments/assets/3808605c-7211-4d15-bb94-06ab88d31076" />


## Step 7: Verify DNS Registration

### Forward Lookup Zone
Confirmed an A record for Win11-CLI01 was created inside the `lab.local` zone.

**Screenshot:**  
`08-forward-dns-record.png`

<img width="1917" height="1026" alt="08-forward-dns-record" src="https://github.com/user-attachments/assets/2b7cbb0d-8852-4e0f-a3ef-2eb3e8bc4dbf" />

### Reverse Lookup Zone
Confirmed the PTR record was created in the `56.168.192.in-addr.arpa` zone after fixing DHCP update credentials.

**Screenshot:**  
`09-reverse-zone-final.png`

<img width="1917" height="1029" alt="09-reverse-zone-final" src="https://github.com/user-attachments/assets/b02b6e13-baa6-433e-9c3e-ef8d4a5bc7c5" />

## Step 8: DHCP Dynamic Update Credentials
Added domain credentials to allow DHCP to write secure DNS records, which completed PTR registration.

**Screenshot:**  
`10-dhcp-dynamic-update-credentials.png`

<img width="1918" height="1032" alt="10-dhcp-dynamic-update-credentials" src="https://github.com/user-attachments/assets/aae50530-9bdb-4320-9489-d7d960aceb4e" />

## Validation
- Client receives DHCP addressing successfully
- Forward DNS (A record) created automatically
- Reverse DNS (PTR record) created after credentials were added
- nslookup resolves both name to IP and IP to name
- DHCP scope and dynamic updates are functioning correctly

## Notes
- PTR records require DHCP to have permissions in AD, which was fixed by adding DHCP credentials
- No default gateway is needed on this host-only lab network
- DNS and DHCP integration is now fully working across the domain

## Next Lab

The next lab will cover **DNS aging and scavenging** so outdated DNS records clean up automatically. This helps keep the lab domain healthy as more devices get added. I will test this by adding a temporary client, letting it generate records, and then removing it to see how DNS handles stale entries.

**Planned next steps:**
- Enable DNS aging and scavenging at the server and zone level  
- Review how DNS timestamps work  
- Add a temporary test VM to generate new records  
- Remove the test VM and confirm stale records get cleaned up  
- Update documentation with screenshots and validation steps
