#  Network Home Lab Project

This repository documents the design, setup, and configuration of a **Home Network Lab** built to simulate a small enterprise IT infrastructure using virtualization, VLAN segmentation, and real-world services.

---

## Lab Overview & Physical equipment

- **ISP Routed** → for internal acsses
- **firewall-end router (Cisco ASA 5515-X)**  → 
- **Switches (Cisco WS-C2948G)**  → For handling VLAN segmentation 
- **physical servers (R710 & R730)** → for virtualization and domain services
- **NAS storage** → for backups, media, and VM hosting (https://pve.proxmox.com/wiki/Passthrough_Physical_Disk_to_Virtual_Machine_(VM))
- **Proxmox VE on (server Dell power edge R710)** → for VM/container management.
---

##  Network Topology Overview
   
<img src="https://i.postimg.cc/LsKZMxrz/Lucas-Home-Lab-Feature-768x576.webp" height="50%" width="50%" alt="Disk Sanitization Steps"/>

---

##  VLAN Configuration

### VLAN 10 –  **Main Lab**
- For sysadmin tools, monitoring systems, and testing VMs
- Only trusted devices allowed
- Access to all VLANs permitted via router rules

### VLAN 20 – 👨‍👩‍👧 **Home Users**
- Daily devices: phones, PCs, tablets
- Moderate access rights
- Internet access allowed
- No access to lab VLAN

### VLAN 30 – 🎫 **Guest Network**
- For guests and visitors
- Strict internet-only access
- Isolated from other VLANs

### VLAN 40 – 📷 **IoT & Surveillance**
- Smart devices: lights, thermostats, sensors, IP cameras
- Heavily restricted internet access
- No local network access except for NVR/NAS

---

##  Physical Infrastructure

### 🔐 Router + Firewall
- Custom firmware (pfSense or OPNSense recommended)
- VLAN-aware, NAT rules, DHCP relay, logging
- Firewall rules to isolate/route traffic based on VLAN

### 🖧 Switches
- Layer 2 managed switches
- VLAN tagging and trunking enabled
- Ports grouped per VLAN with uplink trunks to router and servers

---

##  Server 1: Virtualization Node (Proxmox)

- **Platform**: Proxmox VE
- **VMs**:
  - Ubuntu Server for web services
  - windows 11
  <br>i followed this workflow to
  (https://guides.hakedev.com/wiki/proxmox/windows-11-vm/)
  - CentOS server for DNS/NTP
  - Kali Linux for security testing
- **Containers**:
  - Pi-hole (DNS filtering)
  - Grafana + Prometheus (monitoring)
- **Connected Storage**: NAS over NFS/iSCSI

---

## 🎮 Server 2: Gaming + Active Directory

- **Platform**: Windows Server + Gaming OS dual-boot or Hyper-V
- **Roles**:
  - Active Directory (Domain Controller)
  - DHCP, DNS, Group Policy Management
  - 5 domain user accounts configured
  - Shared folders and roaming profiles
- **Gaming/Media**: Steam server, Plex, etc.

---

