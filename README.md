# DNS, DHCP, AD DS, and Cloud Security on Azure Windows Server 2022 Simple Lab

## Introduction
This is a lab project built from referencing online tutorials to go through the setup of DNS, DHCP, AD DS and cloud security tools Microsoft Sentinel and Microsoft Defender for Cloud on Azure Windows Server 2022.

This project is aided by GitHub Copilot in its construction and documentation.

## Main features
### Section 1: Azure setup
Windows Server 2022 VM on Azure

### Section 2: Server setup
Windows AD DS
- Domain controller
- Organization Units (User, Computer)

Windows DNS
- Forward lookup zone
- Reverse lookup zone

Windows DHCP ([not supported on Azure](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#can-i-deploy-a-dhcp-server-in-a-vnet); lab purposes only)
- DHCP scope

Group policy
- Mapped drive

### Section 3: Security
Microsoft Defender for Cloud:
- Inventory
- Recommendations

Microsoft Sentinel
- Log analytic workspace
- Data connector
- Scheduled query rule

## Reflections
### Major hiccups and mitigation
- Section 1: Since this VM will be cleaned up after the labs, so I will use a faster VM size, Standard D2s v3, instead of the B1s, which would make Server Manager crash.
- Section 2: Took some time to figure out what causes the "DNS name not found" error when trying to apply the domain to the second VM. It turns out that the DNS server address is not set up correctly. I set it to the private IP address of the first VM in network connections > ethernet properties > IPv4 properties.
- Section 2: Took some time to figure out who can see the mapped drive (``domainadmin1`` only)

### Future improvement/lab ideas
- Automation and disaster recovery of Section 2
- Azure AD as an alternative to Windows AD DS (or do hybrid)
- Azure DNS as an alternative to Windows DNS
- Azure DHCP as an alternative to Windows DHCP
- On-premise DHCP server
- Microsoft Defender for Cloud Security Alerts/Azure Defender