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
![Hyper-V Create New VM](https://github.com/git-pak/AD-Home-Lab/blob/main/images/create-vm.png)  

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

See troubleshooting steps and documentation below:  
[Hyper-V Network Connectivity Troublshooting Case Document](https://github.com/git-pak/home-it-troubleshooting/blob/main/cases/Hyper-V-VM-Network-Connectivity-Failure.md)  

Connectivity was verified with:


```
ping 192.168.50.1
```
```
ping 8.8.8.8
```

# Server Preparation

Before installing Active Directory, the server was configured with:

- Computer rename → **DC01**
- Static IPv4 address
- Network connectivity verification

These steps follow best practices for domain controller deployment.

---

# Active Directory Installation

Active Directory Domain Services was installed using **Server Manager**:


Server Manager
→ Manage
→ Add Roles and Features
→ Active Directory Domain Services

Required dependencies were installed automatically.

---

# Domain Controller Promotion

After installing AD DS, the server was promoted to a Domain Controller using the AD DS Configuration Wizard.

Deployment configuration:  
Add a new forest  
Root domain name: lab.local  


Additional configuration:

| Setting | Value |
|---|---|
| NetBIOS Name | LAB |
| Forest Functional Level | Windows Server 2016 |
| DNS Server | Enabled |
| Global Catalog | Enabled |

The server rebooted automatically to complete the promotion process.

---

# DNS Verification

After promotion, DNS zones were verified using **DNS Manager**.

Structure:
DNS
└ DC01
└ Forward Lookup Zones
└ lab.local
├ (SOA)
├ (NS)
├ _msdcs
└ DC01  


This confirms:

- Active Directory–integrated DNS was created
- The Domain Controller successfully registered itself in DNS

---

# Domain Login Verification

After promotion, the administrator account is now authenticated by the domain.

Example login format: LAB\Administrator  


This confirms the server is now functioning as a **Domain Controller for the lab.local forest**.

---

# Skills Demonstrated

This lab demonstrates practical experience with:

- Hyper-V virtual machine provisioning
- Windows Server installation
- Network troubleshooting (APIPA addressing)
- IPv4 configuration
- Active Directory Domain Services installation
- Domain Controller promotion
- DNS zone verification

These tasks reflect common responsibilities in **Tier-1 / Tier-2 Help Desk and IT Support roles**.

---

# Next Steps

Planned extensions to this lab include:

- Creating Organizational Units (OUs)
- Creating domain users and security groups
- Deploying a Windows client VM
- Joining a workstation to the domain
- Practicing common help desk tasks (password resets, account unlocks, GPO troubleshooting)
- Implementing NTFS and share-permissions to enforce least-privilege access.

---


