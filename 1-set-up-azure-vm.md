# Create a virutal machine
1. Go to Azure portal. Search for Virtual Machines. Create a new virtual machine.
2. Basics
- Resource group: winser-rg
- Virtual machine name: winserVM
- Region: East Asia
- Availability options: No infrastructure redundancy required
- Image: Windows Server 2022 Datacenter: Azure Edition – x64 Gen2
- Security type: Standard
- Username: winseradmin # example only
- Password: yourpassword # example only
- Inbound port rules: Allow selected ports (RDP:3389)
3. Disks
- OS disk type: Standard SSD
- leave everything else as default
4. Networking
- Azure automatically assigns names to VNet, Subnet, and Public IP
- leave everything else as default