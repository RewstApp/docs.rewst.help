# BYOD for options generators

{% hint style="warning" %}
For the BYOD integration to function correctly with your RMM, it is essential that the **`Database Config Name`** is set exactly as **`Rewst Cache - Database`**. Failure to do so will result in caching issues, affecting data retrieval performance.

This process requires you to have at least a basic understanding of PowerShell and how to use it with Microsoft.
{% endhint %}

## What does BYOD do?

RMM customers occasionally face challenges with the speed at which data is returned from RMM's APIs. One efficient workaround is to leverage the Bring Your Own Database (BYOD) functionality of Rewst's SQL Database integration. Integrating BYOD with RMM streamlines data retrieval and bypasses potential lags or slow responses. With BYOD in place, RMM's options generation workflows are optimized, leading to improved performance and reduced wait times.&#x20;

{% hint style="info" %}
Before attempting BYOD setup, first set up the [SQL Database integration](../../../configuration/integrations/integration-guides/database-integration-setup/).
{% endhint %}

## Set up BYOD for options generators&#x20;

### Set up the database

You'll need to do the following before attempting setup in Rewst:

1. **Database setup via PowerShell:** Set up an Azure Database instance utilizing the script below. It is assumed that you have an understanding of how to use PowerShell to run PowerShell scripts. Ensure that you're running this script with PowerShell 7. For more information regarding PowerShell please refer to [Microsoft's documentation](https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/01-getting-started?view=powershell-5.1).
2. **Password and script output:** During the Azure setup, you'll be prompted to create a password for the DB account designated for the integration. Make sure to safely store this password and all information resulting from the run of the script. Retaining all of the script's output will be crucial for the next steps in Rewst.&#x20;

Click to expand and copy the below script.

<details>

<summary>Bring Your Own Database setup PowerShell script</summary>

{% code overflow="wrap" %}
```powershell
### Script created by Adam Willford of the Rewst ROC ###
### Updated Sep-2023 to add DTU license option by Lucretia Richmond and James Rood of the Rewst ROC ###

### For any assistance, please contact the ROC team on roc@rewst.io, or via the-kewp in Slack or Discord ###

### Require PS7 - mostly because otherwise the logo doesn't look good...

#Requires -Version 7.0

### Check if the module required is installed and if not, install it ###

if (!(Get-Module -ListAvailable Az.SQL)) {
    Install-Module Az.SQL -Confirm:$false -Force
}

if (!(Get-Module -ListAvailable Az.Resources)) {
    Install-Module Az.Resources -Confirm:$false -Force
}

Import-Module Az.Sql
Import-Module Az.Resources

### Create a cool logo, of course ###

$Logo = @'
██████  ███████ ██        ██ ███████ ████████ 
██  ██  ██    ██       ██ ██        ██    
██████  █████   ██   █  ██  ███████    ██    
██  ██ ██     ██ ███ ██     ██    ██    
██   ██ ███████  ███  ███  ███████     ██    
                                           
'@

Write-Output $Logo
Write-Host 'Rewst ROC - Connecting to Azure' -ForegroundColor Cyan
Write-Host 'Requesting Information from end user' -ForegroundColor Cyan

### All the variables required for the script.  Note these are all prompt based, so no need to amend the script ###

$userEnteredSubscriptionId = $(Write-Host "Please enter your subscription ID:" -ForegroundColor Green -NoNewLine; Read-Host)
$userEnteredCompanyName = $(Write-Host "Please enter your Company Name:" -ForegroundColor Green -NoNewLine; Read-Host)
$userEnteredResourceGroupName = $(Write-Host "Enter a unique new Resource Group name:" -ForegroundColor Green -NoNewLine; Read-Host)
$userEnteredResourceGroupName = $userEnteredResourceGroupName -replace '[^a-zA-Z0-9-]',''
$userEnteredLocation = $(Write-Host "Enter the datacenter location to store the database.  Note for 'US East' you would enter 'eastus'. Locations can be seen here: https://learn.microsoft.com/en-us/azure/availability-zones/az-overview:" -ForegroundColor Green -NoNewLine; Read-Host)
$userLicenseChoice = $(Write-Host "Which licensing option would you like? Enter 1 for vCore or 2 for DTU (default is vCore):" -ForegroundColor Green -NoNewLine; Read-Host)
# $userEnteredServerName = $(Write-Host "Please enter the SQL Server Name required (a-z, 0-9 and '-' only):" -ForegroundColor Green -NoNewLine; Read-Host)
$userEnteredAdminUsername = $(Write-Host "Please enter the SQL Administrator Username:" -ForegroundColor Green -NoNewLine; Read-Host)
$userEnteredAdminPassword = $(Write-Host "Please enter the SQL Administrator password. (This is the last one, promise):" -ForegroundColor Green -NoNewLine; Read-Host -AsSecureString)
[pscredential]$credObject = New-Object System.Management.Automation.PSCredential ($userEnteredAdminUsername, $userEnteredAdminPassword)

### Connect to the Azure instance based on the provided information ###

Connect-AzAccount -Subscription $userEnteredSubscriptionId | Out-Null

### Create the Resource Group ###

try {
    Write-Host "Creating resource group..." -ForegroundColor Cyan
    New-AzResourceGroup -Name $userEnteredResourceGroupName -Location $userEnteredLocation -Tag @{Owner = "Rewst-ROC" } | Out-Null
    Start-Sleep 15
    Write-Host "Successfully created resource group $userEnteredResourceGroupName" -ForegroundColor Blue
} catch {
    Write-Error "There was an error creating the resource group.  The error, if supplied, was:  $($_.Exception.Message)"
    exit
}

### If the resource group exists, crack on ###
if (Get-AzResourceGroup -Name $userEnteredResourceGroupName) {
    ### Create the SQL Server ###
    try {
        $SQLServerCreationInformation = @{
            ResourceGroupName           = $userEnteredResourceGroupName
            ServerName                  = "$($userEnteredCompanyName.ToLower().trim())-database" -replace '[^a-zA-Z0-9-]',''
            Location                    = $userEnteredLocation
            SqlAdministratorCredentials = $credObject
        }
        Write-Host "Creating primary server...(Note this may take several minutes, because Microsoft)" -ForegroundColor Cyan
        New-AzSqlServer @SQLServerCreationInformation | Out-Null
        Write-Host "Successfully created SQL Server - $($SQLServerCreationInformation.ServerName)" -ForegroundColor Blue
    } catch {
        Write-Error "There was an error creating the SQL Server $(($SQLServerCreationInformation.ServerName))  The error, if supplied, was:  $($_.Exception.Message)"
        exit
    }

    ### Create a firewall rule to only allow connections in from Rewst ###

    try {
        $SQLServerFirewallRule = @{
            ResourceGroupName = $userEnteredResourceGroupName
            ServerName        = $SQLServerCreationInformation.ServerName
            FirewallRuleName  = 'Rewst - Allowed IPs'
            StartIpAddress    = '3.139.170.31'
            EndIpAddress      = '3.139.170.31'
        }
        Write-host "Configuring server firewall rule..." -ForegroundColor Cyan
        New-AzSqlServerFirewallRule @SQLServerFirewallRule | Out-Null
        Write-Host "Successfully created Firewall Rule - $($SQLServerFirewallRule.ServerName)" -ForegroundColor Blue
    } catch {
        Write-Error "There was an error creating the firewall rule $(($SQLServerFirewallRule.FirewallRuleName)).  The error, if supplied, was:  $($_.Exception.Message)"
        exit
    }

    ### Create the actual database on the newly created server ###
    
    try {
        switch ($userLicenseChoice) {
            2 {
                $SQLServerDatabaseInformation = @{
                    ResourceGroupName  = $userEnteredResourceGroupName
                    ServerName         = $SQLServerCreationInformation.ServerName
                    DatabaseName       = 'Rewst-Database'
                    Edition            = 'Standard'
                    RequestedServiceObjectiveName = 'S3'
                }
            }
            Default {
                $SQLServerDatabaseInformation = @{
                    ResourceGroupName  = $userEnteredResourceGroupName
                    ServerName         = $SQLServerCreationInformation.ServerName
                    DatabaseName       = 'Rewst-Database'
                    Edition            = 'GeneralPurpose'
                    ComputeModel      = 'Serverless'
                    ComputeGeneration = 'Gen5'
                    vCore              = 2
                    MinimumCapacity    = 2
                    AutoPauseDelayInMinutes = 60
                }
            }
        }
        Write-host "Creating a Standard DTU database..." -ForegroundColor Cyan
        New-AzSqlDatabase @SQLServerDatabaseInformation | Out-Null
        Write-Host "Successfully created Database - $($SQLServerDatabaseInformation.ServerName)" -ForegroundColor Blue
    } catch {
        Write-Error "There was an error creating the database $($SQLServerDatabaseInformation.DatabaseName) on $($SQLServerDatabaseInformation.ServerName).  The error, if supplied, was:  $($_.Exception.Message)"
        exit

    }
} else {
    Write-Error "The Resource Group - $($userEnteredResourceGroupName) was not found and therefore we cannot continue."
    exit
}

### Output User Information ###

Write-Host "Congratulations, you can now go and configure the database in the Rewst integration itself.  The following details will be required:" -ForegroundColor Cyan
Write-Host '--------------------------------------------------------' -ForegroundColor White
Write-Host "Database Config Name: Rewst Cache - Database" -ForegroundColor Green
Write-Host "Database Type: MSSQL" -ForegroundColor Green
Write-Host "Hostname: $($SQLServerDatabaseInformation.ServerName).database.windows.net" -ForegroundColor Green
Write-Host "Port: 1433" -ForegroundColor Green
Write-Host "Username: $userEnteredAdminUsername" -ForegroundColor Green
Write-Host "Password: [Entered During Prompt Phase, we don't want to show it here for obvious reasons]" -ForegroundColor Green
Write-Host "Database Name: $($SQLServerDatabaseInformation.DatabaseName)" -ForegroundColor Green
Write-Host '--------------------------------------------------------' -ForegroundColor White
```
{% endcode %}

</details>

### Set up steps in Rewst

1. Navigate to **Configuration > Integrations** in the left side menu of your Rewst platform.
2. Search for `SQL Database`.
3. Click on the integration tile.
4. Note that as with traditional use of the SQL Database integration, multiple databases are entered into Rewst using the drop-down menu at the top left of your configuration page.&#x20;
5.

    <figure><img src="../../../../.gitbook/assets/Screenshot 2026-03-05 at 10.40.36 AM.png" alt=""><figcaption></figcaption></figure>
6. Enter the information received from running the PowerShell script into the relevant fields:
   1. **Database Config Name** - Unique identifier to pick database for action
   2. **Database Type** - Supported SQL databases
   3. **Hostname** - Hostname for database connection
   4. **Port** - Port for database connection
   5. **Username** - Database user username
   6. **Password** - Database user password
   7. **Database Name** - Database name for database connection
   8. **SSL Required** - SSL encryption provides end-to-end security of data sent during the session
   9. **SSL Hostname Verification** - Verify that the SSL certificate hostname matches the connection hostname. Disable for cloud databases (GCP, AWS, Azure) that use dynamic hostnames or load balancers. SSL certificates are still validated when disabled. SSL Required must be enabled.
   10. **Custom Connection Timeout (seconds)** - Default database connection timeout is 5 seconds
   11. **Custom SSL Certificate** - Leave this blank if using AWS RDS or Azure SQL, which are supported by default. If your database needs a custom SSL, copy and paste the raw CA certificate here.
7. Click **Save Configuration**.

#### Post-integration steps specific to Rewst workflows

Following the database setup, you must attach the \[Rewst- TASK] BYOD: Upsert Cache DB Data Listener\_ workflow as a [completion handler](../../../automations/workflows/completion-handlers-and-workflow-wrappers.md#completion-handlers) to the on-prem workflows. If you are missing this workflow, please [reach out to Rewst support](../../../../support-and-community/roc-support/).&#x20;

1. Navigate to **Automations > Workflows.**
2. Search for `[Rewst- TASK] BYOD: Upsert Cache DB Data Listener`.
3. Click **⋮** .
4. Select **On Completion**.
5. Click **Run this workflow when...**
6. Click <img src="../../../../.gitbook/assets/Screenshot 2025-05-12 at 9.35.44 AM.png" alt="" data-size="line">.
7. Select the following settings:
   * **Workflow:** \[REWST - TASK] BYOD: Upsert Cache DB Data Listener
   * **Trigger On Statuses:** succeeded
   * **Integration Override:** SQL Database
   * **Enabled:** On
8. Click **Submit**.
9. Repeat steps 6-8 with the following workflows
   * \[REWST - OPT GEN] On-Prem: List All Groups
   * \[REWST - OPT GEN] Graph: List Mail Enabled Graph Users with ID and UPN
   * \[REWST - OPT GEN] On-Prem: List Users By Filter With SID And UPN/sam
   * \[REWST - OPT GEN] List On-Prem Exchange Email Domains
   * \[REWST - OPT GEN] Get All AD OUs Containing Users
   * \[REWST - OPT GEN] List On-Prem Exchange Databases - (optional)
   * \[REWST - TASK] List On Prem Exchange Shared Mailboxes - (optional)
   * \[REWST - OPT GEN] List On-Prem Exchange Servers - (optional)
