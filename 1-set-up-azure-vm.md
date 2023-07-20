# Set up Azure VM

## Create a virutal machine
1. Go to Azure portal. Search for Virtual Machines. Create a new virtual machine.
2. Basics
- Resource group: winser-rg
- Virtual machine name: winserVM
- Region: East Asia
- Availability options: No infrastructure redundancy required
- Image: Windows Server 2022 Datacenter: Azure Edition – x64 Gen2
- Security type: Trusted launch virtual machines
- Size: Standard D2s v3
- Username: winseradmin # example only
- Password: yourpassword # example only
- Inbound port rules: Allow selected ports (RDP:3389)
3. Disks
- OS disk type: Premium SSD
- leave everything else as default
4. Networking
- Azure automatically assigns names to VNet, Subnet, and Public IP
- leave everything else as default
5. Review + Create

## Set up static IP
1. Go to the resource page of the VM. Click Networking.
2. Click the network interface.
3. Click IP configurations.
4. Click the IP configuration.
5. Click Static.
6. Click Save.

## Connect to the virtual machine
1. Go to the resource page of the VM. Click Connect.
2. Download the RDP file. Open the file.
3. Enter the username and password you set up earlier.


