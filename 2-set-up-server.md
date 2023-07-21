# Set up the server
[Reference](https://www.youtube.com/watch?v=F6f5xWLNTiQ) (ignore the static IP part)

## Add the roles of AD DS, DNS, and DHCP
1. Go to Server Manager. Click Manage. Click Add Roles and Features.
2. Click next until the server selection page.
3. Click Active Directory Domain Services, DHCP, and DNS. Click Add Features.
4. Click next until installation.
5. When installation succeeded, click Close.

# Promote the server to a domain controller
1. Go to Server Manager. Click Notifications.
2. Click Promote this server to a domain controller.
3. Click Add a new forest.
4. Enter the root domain name. Click Next.
5. Type the DSRM password and leave everything else as default. Click Install.
6. When installation succeeded, click Close.

# Set up Active Directory Users and Computers
1. Go to Server Manager. Click Tools. Click Active Directory Users and Computers.
2. Right click the domain name. Click New. Click Organizational Unit.
3. Enter the name of the OU (e.g. ``TestOU``). Click OK.
4. Right click the OU. Create two new OUs within TestOU named ``TestOU - Computers`` and ``TestOU - Users``. Click ``TestOU - Users``. Click New. Click User.
5. Enter the user information (e.g. ``domainadmin1``). Click Next.
6. Enter the password. Click Next.
7. Click Finish.
8. Right click the user. Click Properties.
9. Click Member Of. Click Add.
10. Enter the group name as domain admins. Click OK.
11. Sign off the VM.
12. Sign in with the new user. There should be no remote access error.

# Set up DNS server
1. Go to Server Manager. Click Tools. Click DNS.
2. Right click the server name. Click Properties.
3. Click Forwarders. Click Edit.
4. Enter the IP address of the DNS server (8.8.8.8 and 8.8.4.4 as Google DNS). Click OK.
5. Click OK.
6. Right click the server name. Click New Zone.
7. Click Primary zone. Click Next.
8. Click To all DNS servers running on domain controllers in this domain: ``winser.local``. Click Next.
9. Click IPv4. Click Next.
10. Enter the network ID same as the first three numbers of the VM private address. 
11. Click Next. Allow only secure dynamic updates. Click Finish.
12. Click ``winser.local`` in Forward Lookup Zones. Right click the domain controller. Click properties. Tick the box of Update associated pointer (PTR) record. Click Apply and then OK. 
- If there is an error message saying created zone cannot be found, it means the network ID has a typo.

# Set up DHCP server (on-prem)
1. Go to Server Manager. Click Notifications. Click Complete DHCP configuration.
2. Click Next. Then Commit. Then Close.
3. Back to Server Manager. Click Tools. Click DHCP.
4. Right click IPv4. Click New Scope.
5. Click Next.
6. Enter the name of the scope (e.g. ``Default Scope``). Click Next.
7. Enter the start (e.g. 10.1.0.20) and end IP address (e.g. 10.1.0.254). Click Next.
8. Enter the subnet mask (e.g. /24). Click Next until Router (Default Gateway) page.
9. Enter the IP address of the default gateway (e.g. 10.1.0.1). Click Next.
10. Check the IP address of the DNS server (leave it as the same VM private address). Click until finish.

# Test DHCP assignment (on-prem)
1. Create a new Windows Server 2022 VM ``winserVM2`` with the same VNet and subnet. Assign a new username and password. Keep the VM private address as dynamic but everything else as the same as the first VM created. Review + create.
2. Connect to ``winserVM2``.
3. Search for Advanced system settings. Click the Computer Name tab. Click Change.
4. Click Domain. Enter the domain name (e.g. ``winser.local``). Click OK.
- If there is an error message saying the DNS name cannot be found, open network connections. Right click the Ethernet. Click Properties. Click Internet Protocol Version 4 (TCP/IPv4). Click Properties. Click Use the DNS server address (10.1.0.4).

# Notes on DHCP server on Azure
DHCP servers are not supported by Azure. ([Source](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#can-i-deploy-a-dhcp-server-in-a-vnet)

# Log in domain computer using domain admin credentials
1. Now you may add the computer on ``winserVM2`` to the domain on ``winserVM``. In ``winserVM``, go to Server Manager. Click Tools. Click Active Directory Users and Computers.
2. Drag the computer to the ``TestOU - Computers`` OU. This is now a domain computer set up.
3. Now login the domain computer (``winserVM2``) with the domain admin credentials (username should be in the format of ``winseradmin@winser.local``). Remember the AD DS Server VM should stay online.
4. If login is successful, the domain computer (``winserVM2``) is set up correctly.

# Add a group policy to map a drive for domain admin logging in to any VM
1. In ``winserVM``, open File Explorer. Go to ``C:``. Create a new folder named ``Share``.
2. Right click the folder. Click Properties. Click Sharing. Click Advanced sharing.
3. Tick the box of Share this folder. Click Permissions. Click Full Control for Everyone. Click OK.
4. Back to Share Properties window. Click Security. Click Advanced. Click Disable inheritane. Click Remove all inherited permissions from this object. Click Add.
5. Click Select a principal. Enter System. Click Full Control. Click OK.
6. Add another principal. Enter Domain users. Click Full Control. Click OK.
7. Enter the Share folder. Create a new text file. Enter some text. Save and close the file.
8. In File Explorer, go to ``\\winserVM\Share``. You should be able to access the file.
9. Go to Server Manager. Click Tools. Click Group Policy Management.
10. Expand the domain name and right click on ``TestOU - Users``. Click Create a GPO in this domain, and Link it here.
11. Enter the name of the GPO (e.g. Mapped drive). Click OK.
12. Right click the GPO. Click Edit.
13. Go to User Configuration > Preferences > Windows Settings > Drive Maps. Right click. Click New > Mapped Drive.
14. Enter the drive letter (e.g. ``Z:``). Enter the path (e.g. ``\\winserVM\Share``). Click OK.
15. Now login the domain computer (``winserVM2``) with the domain admin (``domainadmin1``) credentials. You should be able to see the mapped drive when opening File Explorer.
16. You can log in ``winserVM`` as ``domainadmin1`` as well and check the syncing of newly created files.