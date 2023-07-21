# Security
[Reference](https://cyberwoxacademy.com/azure-cloud-detection-lab-project/) and [YouTube Tutorials](https://www.youtube.com/playlist?list=PLBNtagSCmDWw27ccfeWeiaMcpNIxpGHy4)

## Initial setup
1. In the Azure portal, search for Microsoft Defender for Cloud.
2. Click Getting started. Upgrade the subscription.
3. Click the VM. Click Connect in the option menu. Click Enable just-in-time VM access.
4. Refresh the page and select My IP as the source IP.
5. Search for Log Analytics workspaces. Create a new workspace inside the ``winser-rg`` resouce group. 
6. Search for Microsoft Sentinel. Click Connect workspace. Select the workspace you just created.

## Data connectors
1. In Microsoft Sentinel, click Data connectors.
2. Click Content Hub. Find Windows Security Events. Click Install. After installation is complete, click Manage.
3. Select Windows Secuirty Events via AMA. Click Open Connector Page.
4. Click Create data collection rule. Add a new rule name (e.g. testrule) to the winser-rg resource group. Click Next: Resources.
5. Click Add resources, then select the VMs ``winserVM`` and ``winserVM2``. Click Apply.
6. For Collection, collect all security events.
7. Review + Create 
8. It will take some time for Windows Security Events via AMA to become connected in its status.
9. Now try to log in to the VMs, both successfully and unsuccessfully. Note the time for which did those login actions. You should see the logins in the Logs section of Microsoft Sentinel. For successful login attempts, the query would be:
```
Security Event
| where EventID == 4624
| project TimeGenerated,Computer,Account
```
For unsuccessful login attempts,
```
SecurityEvent
| where EventID == 4625
| project TimeGenerated,Computer,Account
```
## Add a query rule
1. In Microsoft Sentinel, click Analytics.
2. Click Rule template. Search for "Excessive Windows Logon Failures". Click Add.
3. Click Create rule. Add a rule name (e.g. testrule2) to the ``winser-rg`` resource group. Click Next: Tactics.'
4. Select the following tactics:
- Credential Access
5. Click Next: Scheduling and suppression.
6. Click Next: Incident settings.
7. Click Next: Review.
8. Click Create rule.


