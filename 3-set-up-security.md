# Security
[Reference](https://cyberwoxacademy.com/azure-cloud-detection-lab-project/) and [YouTube Tutorials](https://www.youtube.com/playlist?list=PLBNtagSCmDWw27ccfeWeiaMcpNIxpGHy4)

### Notes on costs
- Microsoft Defender for Cloud and Microsoft Sentinel are both very expensive and very recommended to use a free trial for this tutorial. Deleting the resource group will not disable Microsoft Defender for Cloud or Microsoft Sentinel. See Section 4 for cleanup instructions.

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
2. Click Rule template. Search for "Excessive Windows Logon Failures". Select and click Enable.
3. Click Create rule. Add a rule name (e.g. testrule2) to the ``winser-rg`` resource group. 
4. Create rule.

## Incident response (alert)
1. Try to trigger the alert if you have the time. The alert can be viewed in the Incidents section of Microsoft Sentinel.
2. Assign the incident to yourself, give it an active status, and mark it as closed (reason: test).

## View recommendations for individual resource in Microsoft Defender for Cloud
1. In Microsoft Defender for Cloud, click Inventory.
2. You may click View resource on any individual resource to view its recommendations. 
3. You may click on any recommendation to view its details to see mitigation steps.