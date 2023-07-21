# DNS, DHCP, AD DS, and Cloud Security on Azure Windows Server 2022 Simple Lab

## Introduction
This is a lab project built from referencing online tutorials to go through the setup of DNS, DHCP, AD DS and cloud security tools Microsoft Sentinel and Microsoft Defender for Cloud on Azure Windows Server 2022.

This project is aided by GitHub Copilot in its construction and documentation.

## Main features
### Section 1
1. Setting up a Windows Server 2022 virtual machine on Azure.
### Section 2
2. Setting up AD DS on Windows Server 2022:
- Creating a domain controller.
- Creating user accounts.
3. Configuring DNS on Windows Server 2022:
- Creating forward and reverse lookup zones.
4. Setting up DHCP on Windows Server 2022: (configurations won't take in effect as DHCP servers are not supported on Azure, so this is for lab purposes only)
- Creating a DHCP scope.
5. Creating a group policy to map a network drive.
### Section 3
6. Integrating Microsoft Defender for Cloud:
   a. Enabling Microsoft Defender for Cloud on the Azure virtual machine.
   b. Looking at Inventory and Recommendations.
7. Integrating Microsoft Sentinel:
   a. Connecting Azure resources to Microsoft Sentinel.
   b. Setting up data connectors and log analytics.
   c. Creating and customizing Azure Sentinel workbooks and dashboards.
8. Securing the DNS, DHCP, and AD DS services using best practices:
   a. Configuring firewalls and network security groups.
   b. Applying access control lists.
   c. Enabling auditing and logging.
9. Testing the DNS, DHCP, and AD DS services to ensure they are working correctly.
10. Documenting the project, including:
   a. Steps taken to set up and configure the services.
   b. Configuration settings used.
   c. Troubleshooting steps taken.
11. Monitoring and maintaining the environment using Microsoft Defender for Cloud and Microsoft Sentinel:
    a. Reviewing security alerts and recommendations.
    b. Investigating incidents using Microsoft Sentinel.
    c. Continuously improving security posture based on insights from Microsoft Defender for Cloud and Microsoft Sentinel.

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
- On-prem DHCP
- Microsoft Defender for Cloud Security Alerts/Azure Defender