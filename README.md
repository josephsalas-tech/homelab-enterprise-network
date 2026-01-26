# Homelab Enterprise Network with VLAN Segmentation

## Overview
This project documents the design and implementation of a segmented home network built to replicate **small enterprise and school district IT environments**. The network emphasizes security, manageability, and real-world troubleshooting using VLANs, centralized routing and firewalling, managed switching, virtualization, and network-attached storage.

The environment supports multiple trust zones (administrative devices, guests, IoT, and homelab servers) while maintaining controlled inter-VLAN access.

**Core skills demonstrated:**
- VLAN design and segmentation
- Router and firewall configuration
- Managed switching
- Wireless network separation
- Virtualization and NAS integration
- Technical documentation and troubleshooting methodology

---

## Network Hardware & Core Components
- **ISP Modem:** Xfinity modem (bridge mode)
- **Router / Firewall:** TP-Link Omada ER605
- **Managed Switch:** Tenda 5-Port Managed Switch
- **Wireless Access Point:** TP-Link Archer AX55 (AP mode)
- **Server Host:** Proxmox VE
- **Storage:** TrueNAS SCALE (virtual machine)

---

## VLAN Architecture
The network is segmented into four primary VLANs, each serving a defined operational purpose.

| VLAN ID | Name / Purpose      | Typical Devices |
|--------|---------------------|-----------------|
| 10     | Home / Admin        | Personal PCs, admin devices, network management |
| 20     | Guest Network       | Guest phones and laptops |
| 30     | IoT Network         | Smart TVs, streaming devices, IoT hardware |
| 40     | Homelab / NAS       | Proxmox host, virtual machines, TrueNAS, infrastructure services |

Screenshots of the TP-Link ER605 VLAN configuration and DHCP scopes are included below.

**Screenshots:**
- ER605 VLAN configuration page
<img width="1903" height="906" alt="image" src="https://github.com/user-attachments/assets/6879c0bb-e63f-49bf-b291-1506098eb0e0" />

- DHCP configuration per VLAN  
<img width="967" height="901" alt="image" src="https://github.com/user-attachments/assets/705b3d68-a48e-4b4c-a803-d94c041eba4a" />

## Network Topology
High-level traffic flow for the network:

[ Internet ]
|
[Xfinity Modem - Bridge Mode]
|
[TP-Link Omada ER605]
|
[Tenda Managed Switch]
├── VLAN 10 → Home / Admin Devices
├── VLAN 20 → Guest Network
├── VLAN 30 → IoT Devices
└── VLAN 40 → Homelab / NAS
|
[Proxmox Host]
├── Windows Server VM (Active Directory)
├── Windows 10 Pro Client VM
├── TrueNAS SCALE VM
└── Linux Utility VMs


**Diagrams Included:**
- Physical network topology
- Switch port VLAN assignments

---

## Routing, Firewalling, and Access Control
- The **TP-Link Omada ER605** functions as the central routing and firewall platform.
- Inter-VLAN routing is explicitly controlled to limit lateral movement.
- Guest (VLAN 20) and IoT (VLAN 30) networks are isolated from administrative and server resources.
- The homelab VLAN (VLAN 40) is restricted to infrastructure services only.
- Wireless SSIDs are mapped to their corresponding VLANs through the access point.

This segmentation model reflects best practices commonly used in:
- School district networks
- Small enterprise environments
- MSP-managed infrastructure

---

## Services Hosted on the Network
- **Virtualization:** Proxmox VE
- **Directory Services:** Windows Server Active Directory (lab environment)
- **Storage:** TrueNAS SCALE with SMB shares and dataset permissions
- **DNS Filtering:** Pi-hole (VLAN-aware configuration)
- **Client Systems:** Windows 10 Pro domain-joined virtual machine

All services are intentionally segmented to reinforce security boundaries and provide realistic troubleshooting scenarios.

---

## Validation & Testing
The following functionality was verified during implementation:
- Devices receive correct IP addresses based on VLAN membership
- Unauthorized VLAN access is blocked by routing rules
- NAS SMB shares are accessible only from approved networks
- Wireless clients are isolated based on SSID-to-VLAN mapping
- Virtual machines retain connectivity after reboots and DHCP renewals

**Validation Screenshots:**
- Proxmox VM overview
- TrueNAS SMB datasets and permissions
- Pi-hole dashboard and DNS query statistics

---

## Troubleshooting & Lessons Learned
- DNS behavior across VLANs requires explicit configuration to prevent fallback to public resolvers
- Wireless VLAN tagging must match router and switch configuration exactly
- Bridge-mode ISP modems simplify firewall design but require WAN verification
- Consistent documentation significantly reduces recovery time after configuration changes

---

## Future Improvements
- Centralized logging using Syslog or Wazuh
- Dedicated NTP server for consistent timestamps
- Single Sign-On (SSO) integration across services
- VPN access into VLAN 40 for secure remote administration
- Expanded switching infrastructure and structured cabling

---

## Why This Project Matters
This homelab was built to demonstrate **practical IT support, networking, and troubleshooting skills** rather than purely theoretical knowledge. It reflects real-world constraints, incremental problem-solving, and documentation practices expected in production IT environments.

---

## Resume / LinkedIn Summary
Designed and documented a VLAN-segmented enterprise-style network using TP-Link Omada routing, managed switching, Proxmox virtualization, and NAS services to simulate school district and small-enterprise IT environments.


