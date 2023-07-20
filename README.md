# DNS, DHCP, AD DS, and Cloud Security on Azure Windows Server 2022 Simple Lab

## Introduction
This is a lab project built from referencing online tutorials to go through the setup of DNS, DHCP, AD DS and cloud security tools Microsoft Sentinel and Microsoft Defender for Cloud on Azure Windows Server 2022.

This project is aided by GitHub Copilot in its construction and documentation.

## Main features
1. Setting up a Windows Server 2022 virtual machine on Azure.
2. Setting up AD DS on Windows Server 2022:
   a. Creating a domain controller.
   b. Creating user accounts.
3. Configuring DNS on Windows Server 2022:
   a. Creating forward and reverse lookup zones.
4. Setting up DHCP on Windows Server 2022:
   a. Creating a DHCP scope.
   b. Creating DHCP reservations.
   c. Configuring DHCP options.
5. Integrating Microsoft Defender for Cloud:
   a. Enabling Microsoft Defender for Cloud on the Azure virtual machine.
   b. Configuring security policies and recommendations.
   c. Monitoring and responding to security alerts.
6. Integrating Microsoft Sentinel:
   a. Connecting Azure resources to Microsoft Sentinel.
   b. Setting up data connectors and log analytics.
   c. Creating and customizing Azure Sentinel workbooks and dashboards.
7. Securing the DNS, DHCP, and AD DS services using best practices:
   a. Configuring firewalls and network security groups.
   b. Applying access control lists.
   c. Enabling auditing and logging.
8. Testing the DNS, DHCP, and AD DS services to ensure they are working correctly.
9. Documenting the project, including:
   a. Steps taken to set up and configure the services.
   b. Configuration settings used.
   c. Troubleshooting steps taken.
10. Monitoring and maintaining the environment using Microsoft Defender for Cloud and Microsoft Sentinel:
    a. Reviewing security alerts and recommendations.
    b. Investigating incidents using Microsoft Sentinel.
    c. Continuously improving security posture based on insights from Microsoft Defender for Cloud and Microsoft Sentinel.

## Reflections
### Major hiccups and mitigation
- Section 1: Since this VM will be cleaned up after the labs, so I will use a faster VM size, Standard D2s v3, instead of the B1s, which would make Server Manager crash.

### Future improvement
- Azure DNS as an alternative to Windows DNS
- Automation