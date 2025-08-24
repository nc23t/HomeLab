

2025-08-22 16:38

Status:

Tags:


# Write Up


# Web Application Security Home Lab

## Overview
This project demonstrates a home lab environment I built to practice web application security concepts, including deploying a vulnerable web application (DVWA), configuring a Web Application Firewall (WAF), and enforcing security rules.  

The lab was designed to simulate a real-world scenario where a web server is protected by a WAF, and attacker/defender dynamics can be tested.

---

## Topology

- **Victim / App Host:** Ubuntu Desktop VM
    
- **Attacker:** Kali Linux Desktop VM
    
- **App:** DVWA (PHP) on Apache + MySQL
    
- **WAF/Proxy:** SafeLine WAF on the Ubuntu host (fronting Apache)
    
- **Name Resolution:** `/etc/hosts` on both VMs (e.g., `dvwa.local`)
![[VMWare-Virtual-MachineList.png]]
![[both-VMscreens.png]]👉 **Insert Network Diagram Screenshot Here** (VMs, IPs, WAF, browser access)  

---

## Setup Process

### 1. Virtual Machines
- Created two VMs:
  - Ubuntu Desktop → hosting the DVWA server and WAF
  - Kali Linux → used as an attacker machine for testing  
  - Configured a bridged Virtual Network
- Configured `/etc/hosts` on both machines to map hostnames to VM IPs.![[both-VMscreens.png]]
![[Ubuntu-etc-hosts.png]]
![[Kali-etc-hosts.png]]👉 **Insert Screenshot of `/etc/hosts` entries**  

---

### 2. LAMP Stack & DVWA Installation
- Installed **Apache2**, **MySQL**, and **PHP** on Ubuntu.  
- Downloaded and deployed **DVWA** into Apache’s web root.  
- Configured database credentials in `config.inc.php`.  
- Confirmed DVWA was accessible through the browser on both VMs.

![[DVWA-Login.png]]👉 **Insert Screenshot of DVWA login page**  

---

### 3. SafeLine WAF Setup
- Installed **SafePoint WAF** on Ubuntu VM.  
- Configured it to proxy traffic to the DVWA application.  
- Verified DVWA was accessible through the WAF.  
![[WAF-DashRequests.png]]
![[WAF-DashRequests2.png]]👉 **Insert Screenshot of WAF web console**  

---

### 4. Firewall Rules
- Created a firewall rule in the WAF to **block all traffic originating from the Kali Linux VM’s IP**.  
- Verified that requests from Kali were denied while other traffic succeeded.  

👉 **Insert Screenshot of blocked request or WAF logs**  
![[WAF-BlockKaliVMRule.png]]
---

### 5. SSL/TLS Configuration
- From the Kali Linux VM, generated a **certificate and private key**.  
- Imported this certificate into the WAF to enable secure HTTPS connections.  
- Confirmed DVWA was accessible securely via `https://dvwa.local`.  
![[WAF-Certificate.png]]
👉 **Insert Screenshot of HTTPS access in browser**  

---

## Key Takeaways
- Practiced setting up a **LAMP stack** and deploying DVWA.  
- Gained hands-on experience configuring a **Web Application Firewall**.  
- Implemented **access control** with firewall rules.  
- Configured **SSL/TLS** certificates manually for secure communication.  
- Built foundational skills for defending web applications in a controlled environment.  

---

## Next Steps / Improvements
- Expand the lab with additional vulnerable apps (e.g., Juice Shop).  
- Integrate a SIEM (e.g., Splunk or ELK stack) to monitor WAF logs.  
- Add intrusion detection/prevention systems for deeper network visibility.  


 




# References 