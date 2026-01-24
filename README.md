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
- DHCP configuration per VLAN  

---

## Network Topology
High-level traffic flow for the network:


