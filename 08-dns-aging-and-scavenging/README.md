# **Lab 8: DNS Aging & Scavenging + DHCP Health Check**

## **Overview**
In this lab, I enabled DNS Aging and Scavenging inside my Active Directory environment and validated that DHCP is correctly maintaining DNS records. This helps keep the DNS zone clean as clients join, leave, or refresh their leases.  

For demonstration purposes, I set the refresh and no-refresh intervals to **1 day**, since this is a homelab and I want to see updates quickly. In real enterprise environments, these values are typically longer (for example, 7 days + 7 days).

---

## **Objective**
- Enable DNS Aging on the forward lookup zone  
- Enable DNS server scavenging  
- Configure DHCP to update and clean up DNS records  
- Refresh the client’s DNS registration  
- Manually trigger scavenging  
- Verify the behavior in DNS Manager and Event Viewer  

---

## **Prerequisites**
- Windows Server 2022 Domain Controller (DC01)  
- DNS and DHCP roles installed  
- Active Directory–Integrated DNS zone (e.g., `lab.local`)  
- Windows 11 domain-joined client using DHCP  

---

## **Configuration Steps**

### **1. Verified DNS Zone Configuration**
I confirmed the zone is AD-integrated and using **Secure Only** dynamic updates.  
This allows domain-joined clients and DHCP to safely update DNS records.

`01-dns-aging-zone-general.png`
<img width="1919" height="1028" alt="01-dns-aging-zone-general" src="https://github.com/user-attachments/assets/be3d87a9-157f-4129-bf0b-909d06e95095" />

---

### **2. Enabled DNS Aging**
From the zone’s **Aging** menu, I turned on scavenging of stale records and set both intervals to **1 day** for lab visibility.

(In production, these intervals are usually much longer to avoid unnecessary churn.)

`02-dns-aging-zone-aging-settings.png`
<img width="1919" height="1029" alt="02-dns-aging-zone-aging-settings" src="https://github.com/user-attachments/assets/d3cad2fe-cc98-4f26-bfe1-628e64f60633" />

---

### **3. Enabled Scavenging on the DNS Server**
On the DNS server itself, I enabled automatic scavenging and set the scavenging period to **1 day**.

This allows the server to routinely check for stale records and remove them if needed.

`03-dns-aging-server-advanced-scavenging.png`
<img width="1918" height="1030" alt="03-dns-aging-server-advanced-scavenging" src="https://github.com/user-attachments/assets/16e16a64-e28b-426e-a2d0-482515437135" />

---

### **4. Validated DHCP DNS Integration**
In the DHCP IPv4 DNS tab, I enabled:

- Always update A and PTR records  
- Discard records when leases are deleted  
- Update DNS for clients that don’t explicitly request it  

This ensures DHCP keeps DNS accurate as leases renew or expire.

`04-dhcp-dns-settings.png`
<img width="1919" height="1033" alt="04-dhcp-dns-settings" src="https://github.com/user-attachments/assets/a50d47d5-73b3-4e2e-ac06-dba943c36c19" />

---

### **5. Refreshed Client DNS Registration**
On the Windows 11 client, I renewed the lease and re-registered DNS:

```
ipconfig /release
ipconfig /renew
ipconfig /registerdns
```

After refreshing DNS Manager, the client’s A record recreated with a **fresh timestamp**.  
This confirms dynamic updates and aging are functioning correctly.

`05-dns-aging-client-a-record-timestamp-updated.png`
<img width="1919" height="1031" alt="05-dns-aging-client-a-record-timestamp-updated" src="https://github.com/user-attachments/assets/d7a1d5e8-fec6-471f-9446-4bae2292f2a9" />

---

### **6. Triggered Manual Scavenging**
I manually initiated scavenging from DNS Manager.  
In a new lab environment, there usually aren’t any stale records yet, which is expected.

`06-dns-aging-manual-scavenge.png`
<img width="1918" height="1032" alt="06-dns-aging-manual-scavenge" src="https://github.com/user-attachments/assets/8a9790e2-d22d-4524-ab50-f8a92e828dd9" />

---

### **7. Verified Scavenging Events**
Lastly, I checked the DNS Server Operational log.  
Event **2502** confirmed the scavenging cycle completed successfully.

`07-dns-scavenging-event-log.png`
<img width="1919" height="1030" alt="07-dns-scavenging-event-log" src="https://github.com/user-attachments/assets/1ba578c3-417f-4965-a95f-bd548e6a875e" />


---

## **Verification Checklist**
- Aging enabled on the zone  
- Scavenging enabled on the server  
- DHCP configured to maintain A/PTR records  
- Timestamp on client A record updated  
- Manual scavenging performed  
- Event Viewer confirmed scavenging ran  

---

## **Why This Lab Matters**
DNS health is critical for Active Directory. Stale or inconsistent records can cause:

- Name resolution failures  
- Duplicate hostnames  
- Group Policy issues  
- Join failures (especially in hybrid setups)  
- Intune / Autopilot enrollment issues  

Aging + Scavenging ensures the DNS zone stays clean and prevents issues as more devices get added to the environment.

---

## **Next Lab**
**Lab 9: Entra ID – Cloud Identity Basics**

In the next lab, I start building the cloud side of the environment by configuring Entra ID users, groups, and admin roles. This sets the foundation for Conditional Access, Intune enrollment, Autopilot, and later connecting my on-prem Active Directory to Entra ID for a hybrid identity setup.
