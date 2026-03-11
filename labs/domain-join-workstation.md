# Domain Join Workstation Lab
Windows 11 • Active Directory • Hyper-V

---

# Overview

This lab demonstrates how to deploy a Windows 11 client workstation and join it to an Active Directory domain. The objective was to simulate a real enterprise workflow where a workstation is prepared, connected to the domain, and used by domain users.

Domain joining is a common responsibility for Help Desk and IT Support technicians when provisioning new employee workstations.

---

# Environment

| Component | Details |
|---|---|
| Hypervisor | Hyper-V |
| Domain Controller | DC01 |
| Domain | lab.local |
| Domain Controller IP | 192.168.50.10 |
| Client OS | Windows 11 |
| Client Computer Name | USA-WKS-01 |

---

# Steps

## Step 1 — Deploy Windows 11 Client VM

A new virtual machine was created in Hyper-V to simulate an employee workstation.

VM configuration:

| Setting | Value |
|---|---|
| VM Name | USA-WKS-01 |
| Generation | Generation 2 |
| Memory | 4096 MB |
| Network | External Virtual Switch |
| Disk | 60 GB |
| OS | Windows 11 |

During installation a temporary local setup account was created.

Example local account:

```
labsetup
```

This account is used only to complete the installation and configure the workstation before joining the domain.

---

## Step 2 — Configure DNS for Domain Resolution

For domain join to work, the workstation must use the **domain controller as its DNS server**.

Navigate to:

```
Settings
→ Network & Internet
→ Advanced network settings
→ More network adapter options
```

Open the Ethernet adapter and configure IPv4 settings:

```
Preferred DNS Server: 192.168.50.10
```

This allows the client machine to locate the domain controller.

---

## Step 3 — Verify Connectivity

Before attempting to join the domain, connectivity to the domain controller was verified.

Example commands:

```
ping dc01

```

```
nslookup lab.local
```
![Ping dc01](https://github.com/git-pak/AD-Home-Lab/blob/main/images/AD%20verified%20domain%20connectivity%20using%20ping.png)
Successful responses confirm that DNS and network communication are functioning correctly.

---

## Step 4 — Start the Domain Join Process

Navigate to:

```
Settings
→ System
→ About
→ Rename this PC (Advanced)
```

Click:

```
Change
```

Select:

```
Domain
```

Enter the domain name:

```
lab.local
```

---

## Step 5 — Authenticate with Domain Administrator

Windows prompts for credentials with permission to join the domain.

Example credentials:

```
LAB\Administrator
```

After authentication, Windows confirms the join with the message:

```
Welcome to the lab.local domain
```

---

## Step 6 — Restart the Workstation

The workstation must be restarted to complete the domain join process.

After reboot, the system becomes a member of the **lab.local** domain.

---

## Step 7 — Log in with Domain Users

Users previously created in Active Directory can now log into the workstation.

Example logins:

```
LAB\sampak
```

```
LAB\tombrady
```

On first login, Windows creates a domain user profile.

Example user profile path:

```
C:\Users\sampak
```

---

## Step 8 — Verify Computer Object in Active Directory

On the domain controller open:

```
Active Directory Users and Computers
```

Navigate to:

```
Computers
```

The workstation appears as:

```
USA-WKS-01
```

The computer object was then moved to the appropriate OU:

```
lab.local
└── USA
     └── Computers
          └── USA-WKS-01
```

---

# Verification

Successful domain join was verified by:

- Logging into the workstation using a domain user account
- Confirming the workstation appears in Active Directory
- Confirming domain user profiles are created on the workstation

---

# Skills Demonstrated

- Windows workstation deployment using Hyper-V
- DNS configuration for domain environments
- Joining a computer to an Active Directory domain
- Domain authentication using domain credentials
- Active Directory computer object management
- Organizational Unit (OU) placement for workstations

These tasks reflect common responsibilities for **Tier 1 / Tier 2 Help Desk and IT Support roles**.

---

# Real-World Workflow Simulated

This lab simulates a typical enterprise device deployment process:

```
Deploy workstation
↓
Configure networking
↓
Join workstation to domain
↓
User logs in with domain account
↓
Workstation managed through Active Directory
```

