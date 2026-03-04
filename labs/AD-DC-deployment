# Active Directory Domain Controller Deployment Lab
Windows Server 2022 • Hyper-V • AD DS • DNS

---

# Overview

This lab documents the deployment of a **Windows Server 2022 Active Directory Domain Controller** in a Hyper-V virtualized environment.

The objective was to build a foundational Active Directory environment and practice core system administration tasks commonly performed by Help Desk and IT Support professionals.

Key technologies implemented:

- Hyper-V virtualization
- Windows Server 2022
- Active Directory Domain Services (AD DS)
- DNS Server
- IPv4 network configuration
- Domain Controller promotion

---

# Lab Environment

| Component | Details |
|---|---|
| Hypervisor | Microsoft Hyper-V |
| Host OS | Windows 11 |
| Server OS | Windows Server 2022 |
| Network | 192.168.50.0 /24 |
| Domain | lab.local |
| Domain Controller | DC01 |
| Server IP | 192.168.50.10 |

---

# VM Deployment

A new virtual machine was created using Hyper-V Manager.

Configuration:

| Setting | Value |
|---|---|
| Generation | Generation 2 |
| Memory | 8192 MB |
| Network | External Virtual Switch |
| Virtual Disk | 60 GB |
| Installation Media | Windows Server 2022 ISO |

The server OS was installed using the **Desktop Experience** option to allow graphical administration tools.

---

# Network Configuration

After installation, the server initially received an **APIPA address (169.254.x.x)** indicating DHCP failure.

Troubleshooting steps included:

- Verifying Hyper-V virtual switch configuration
- Confirming physical adapter binding (Intel Wi-Fi 6 AX200)
- Testing DHCP renewal with `ipconfig /renew`
- Recreating the Hyper-V external switch
- Assigning a manual static IPv4 configuration

Final network configuration:
[Hyper-V Network Connectivity Troublshooting Case Document](https://github.com/git-pak/home-it-troubleshooting/blob/main/cases/Hyper-V-VM-Network-Connectivity-Failure.md)  
