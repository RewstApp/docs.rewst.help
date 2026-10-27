# NinjaOne integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the NinjaOne integration do?

Our NinjaOne integration provides users with a powerful combination of documentation, remote monitoring, and management capabilities. Seamlessly access and manage NinjaOne within Rewst, monitor and troubleshoot devices, deploy software, and perform remote tasks more effectively. Use this integration to centralize your IT documentation and RMM workflows, ensuring a comprehensive and streamlined approach to IT management within the Rewst platform.

## Set up the NinjaOne integration

### Set up steps in NinjaOne

1. Navigate to **Administration > Library > Automation**.
2. Click **Add**, then **New Script**.
3. Add the following script:
   1. Name: Rewst (Windows)
   2. Language: Powershell
   3. OS: Windows
   4. Architecture: All
   5. Paste the code below into the script box

{% hint style="info" %}
Your Rewst Base URL will vary depending on which Rewst instance you are on. You must update the $rewst\_base\_url property in the script below to match your Rewst Instance. You can identify which instance you are on by the URL you use to access Rewst. Please use the following table as a guide to identify your Rewst Base URL.\
Example of correct base URL: `https://engine.rewst.io/webhooks/custom/action`
{% endhint %}

| Rewst URL       | Base URL           |
| --------------- | ------------------ |
| app.rewst.io    | engine.rewst.io    |
| app.eu.rewst.io | engine.eu.rewst.io |
| app.rewst.eu    | engine.rewst.eu    |
| app.rewst.asia  | engine.rewst.asia  |

```powershell
Param(
    [Parameter(Mandatory=$true)]
    [string]$script_content_path,
    [Parameter(Mandatory=$true)]
    [string]$results_postdata_path
)

$rewst_base_url = "https://INSERTBASEURLHERE/webhooks/custom/action"
$script_content_url = "$rewst_base_url/$script_content_path"
$post_url = "$rewst_base_url/$results_postdata_path"



# Download Script Content from Rewst

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$wc = New-Object System.Net.WebClient
$wc.Encoding = [System.Text.Encoding]::UTF8
$commands = ($wc.DownloadString($script_content_url))

# Execute Script Content

iex $commands
```

<figure><img src="../../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. In the Integrations page, search for the NinjaOne integration.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-01-16 at 2.14.22 PM.png>)
3. Click on the integration tile to launch setup.
4.  Choose your Region from the **Region Instance** drop-down selector.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>
5. Click **Save Configuration**. This saving is necessary to ensure that there is no error in the next step.
6. Authorize OAuth into NinjaOne, via Microsoft. You should see your customer show up at the bottom. You may need to click **Refresh Options** for customers to populate.
   1. Rewst connects to NinjaOne with the permissions of the NinjaOne user who completes the authorization.&#x20;
   2. If your own internal or infrastructure organization is managed in NinjaOne, we recommend creating a dedicated NinjaOne user with access only to the client organizations Rewst should manage, and signing in as that user when you authorize. This keeps automations such as onboarding from being run against your internal organization. Consider also removing that user’s permission to create technicians.
7. Click **Save Configuration** again.
8. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.

{% hint style="info" %}
For APAC customers:

* When you click **Authorize** during the set up process, you end up at the URL [https://app.ninjarmm.com/auth/](https://app.ninjarmm.com/auth/).
* If you change the **Region Instance** to APAC and click **Authorize**, you may still be redirected to the US site.
* Click **Save Configuration** first. Then, reload Ninja's website and ensure that it's showing the correct APAC region.
* Click **Authorize** again. The URL should now show the correct APAC address.
{% endhint %}

## Test the integration

Once you’ve [mapped your customers](https://docs.rewst.help/documentation/integrations/general/organization-mapping#what-is-organization-mapping), test the integration by following the steps below.

1. Navigate to **Automations > Workflows**.
2. Click **Create**.
3. Name your workflow, and click **Submit**.
4. Drag a Ninja action onto your workflow builder canvas. In this example, we use **List Contacts**.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-01-16 at 2.18.21 PM.png>)<br>
5. Click <img src="../../../.gitbook/assets/Screenshot 2025-02-21 at 11.13.39 AM.png" alt="" data-size="line"> to add a trigger. In the relevant fields, choose or enter the following settings:
   1. **Name** your trigger
   2. **Trigger Type**: **Core - Always Pass**
   3. **Integration Overrides**: **NinjaOne**
   4. **Enable** the trigger for all or some of your managed organizations, depending on your setup and preference
6.  Click **Submit**.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>
7. Click **Test**, and select a company to run the action for. Test a handful of companies to ensure the integration is working.

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Use custom PowerShell scripts with your RMM integration

This brand of RMM allows PowerShell scripts to be passed via API. To report the script back to Rewst, you'lll need to add a manual webhook action. We recommend using the run PowerShell script subworkflow to handle this for you and if using custom scripts you will need to add this to bottom to ensure the call back to Rewst is made.

```
$postData = $PS_Results | ConvertTo-Json
Invoke-RestMethod -Method 'Post' -Uri $post_url -Body $postData -ContentType 'application/json; 
charset=utf-8'
```

## Crates related to the NinjaOne integration

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Just-in-Time Admin Access</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.01.35 PM.png">Screenshot 2025-11-13 at 3.01.35 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/just-in-time-admin-access-crate.md">just-in-time-admin-access-crate.md</a></td></tr><tr><td><strong>Agent Smith: Device Provisioning, and Agent Smith Service Provisioning</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.00.37 PM.png">Screenshot 2025-11-13 at 3.00.37 PM.png</a></td><td><a href="../../agent-smith/agent-smith-configuration-overview.md">agent-smith-configuration-overview.md</a></td></tr><tr><td><strong>Windows 11 Compatibility Checker</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.02.29 PM.png">Screenshot 2025-11-13 at 3.02.29 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/windows-11-compatibility-checker-crate.md">windows-11-compatibility-checker-crate.md</a></td></tr><tr><td><strong>Bulk Move Users to Specified OU</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.02.05 PM.png">Screenshot 2025-11-13 at 3.02.05 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/bulk-move-users-to-specified-ou-crate.md">bulk-move-users-to-specified-ou-crate.md</a></td></tr></tbody></table>

## Troubleshoot the NinjaOne integration

### All List component actions fail

If any list action is failing, ensure that you have added the script in previous instructions, into NinjaOne.

{% hint style="info" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## NinjaOne actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).
{% endhint %}

NinjaOne's own API documentation can be found [here](https://app.ninjarmm.com/apidocs-beta/core-resources).

| Category                    | Action                                                       | Description                                                                                                                                      |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Backups**                 | Create Integrity Check Job                                   | Description coming soon...                                                                                                                       |
| **Backups**                 | List Backup Jobs                                             | Returns list of backup jobs                                                                                                                      |
| **Backups**                 | List Integrity Check Jobs                                    | Returns list of integrity check jobs                                                                                                             |
| **Checklist Templates**     | Archive A Checklist Template                                 | Archive a checklist template by id                                                                                                               |
| **Checklist Templates**     | List Checklist Templates                                     | List checklists templates with given criteria                                                                                                    |
| **Checklist Templates**     | Create Checklist Templates                                   | Creates multiple checklist templates                                                                                                             |
| **Checklist Templates**     | Update Checklist Templates                                   | Updates multiple checklist templates                                                                                                             |
| **Checklist Templates**     | Delete A Checklist Template                                  | Delete a checklist template by id                                                                                                                |
| **Checklist Templates**     | Delete Checklist Templates                                   | Deletes checklist templates by id                                                                                                                |
| **Checklist Templates**     | Restore A Checklist Template                                 | Restore a checklist template by id                                                                                                               |
| **Devices**                 | List Custom Fields for Device                                | Returns list of applicable management options                                                                                                    |
| **Devices**                 | Update Field Values                                          | Update device's custom field values                                                                                                              |
| **Devices**                 | Get Last Logged On User For Device                           | Returns username that was last to login to device                                                                                                |
| **Devices**                 | List OS Patches by Device                                    | Returns list of pending/rejected/approved OS patches for device                                                                                  |
| **Devices**                 | Get OS Update Installation Report By Device                  | Returns patch installation history records (successful and failed) for device                                                                    |
| **Devices**                 | Get Software Update History by Device                        | Returns 3rd party software patch installation history records for device (successful and failed)                                                 |
| **Devices**                 | List Disk Drives by Device                                   | Returns device disks' details                                                                                                                    |
| **Devices**                 | List Storage Volumes by Device                               | Returns device volumes' details                                                                                                                  |
| **Devices**                 | List Processors by Device                                    | Returns list of device Processor details                                                                                                         |
| **Devices**                 | List Installed Software by Device                            | Returns list of software installed on device                                                                                                     |
| **Devices**                 | Device Alerts (Triggered Conditions) by Device               | Returns list of active alerts (triggered conditions) for device                                                                                  |
| **Devices**                 | Device Currently Running (Active) Jobs by Device             | Returns currently running jobs for device                                                                                                        |
| **Devices**                 | List Windows Services by Device                              | Returns list of Windows Services and their statuses                                                                                              |
| **Devices**                 | Get Device Details                                           | Returns device details                                                                                                                           |
| **Devices**                 | Get Device Activities                                        | Returns activity log for device                                                                                                                  |
| **Devices**                 | Pending, Failed And Rejected Software Patches For Device     | Returns list of 3rd party Software patches for a device (for which there were no installation attempts)                                          |
| **Document Templates**      | Archive A Document Template                                  | Archives a document template by id                                                                                                               |
| **Document Templates**      | List Document Templates With Fields                          | List document templates with fields                                                                                                              |
| **Document Templates**      | Create Document Template                                     | Create document template                                                                                                                         |
| **Document Templates**      | Get Document Template                                        | Get document template                                                                                                                            |
| **Document Templates**      | Update Document Template                                     | Updates a document template by id                                                                                                                |
| **Document Templates**      | Delete A Document Template                                   | Deletes a document template by id                                                                                                                |
| **Document Templates**      | Restore A Document Template                                  | Restores a document template by id                                                                                                               |
| **Generic Action**          | Generic API Request                                          | Generic action for making authenticated requests against the NinjaOne API                                                                        |
| **Groups**                  | List Group Members' Devices                                  | Returns list of device identifiers that match group criteria                                                                                     |
| **Knowledge Base Articles** | Upload Temporary Attachments                                 | Upload temporary attachment                                                                                                                      |
| **Knowledge Base Articles** | Archive Knowledge Base Articles                              | Archive knowledge base articles                                                                                                                  |
| **Knowledge Base Articles** | Archive Knowledge Base Folders                               | Archive knowledge base folders                                                                                                                   |
| **Knowledge Base Articles** | Create Knowledge Base Articles                               | Create knowledge base articles                                                                                                                   |
| **Knowledge Base Articles** | Update Knowledge Base Articles                               | Update knowledge base articles                                                                                                                   |
| **Knowledge Base Articles** | Delete Knowledge Base Articles                               | Delete knowledge base articles                                                                                                                   |
| **Knowledge Base Articles** | Delete Knowledge Base Folders                                | Delete knowledge base folders                                                                                                                    |
| **Knowledge Base Articles** | Download Knowledge Base Article                              | Download knowledge base article                                                                                                                  |
| **Knowledge Base Articles** | List Organization Knowledge Base Articles                    | Lists organization knowledge base articles                                                                                                       |
| **Knowledge Base Articles** | List Global Knowledge Base Articles                          | Lists global knowledge base articles                                                                                                             |
| **Knowledge Base Articles** | Get Knowledge Base Article Signed URLs                       | Get knowledge base article signed urls                                                                                                           |
| **Knowledge Base Articles** | Get Knowledge Base Folder                                    | Returns knowledge base folder and its content                                                                                                    |
| **Knowledge Base Articles** | Restore Archive Knowledge Base Articles                      | Restore archived knowledge base articles                                                                                                         |
| **Knowledge Base Articles** | Restore Archived Knowledge Base Folders                      | Restore archived knowledge base folders                                                                                                          |
| **Knowledge Base Articles** | Upload Knowledge Base Articles                               | Upload knowledge base articles                                                                                                                   |
| **Knowledge Base Articles** | Download Related Item Attachment                             | Download related item attachment                                                                                                                 |
| **Knowledge Base Articles** | Get Related Item Attachments Signed URLs                     | Get related item attachments signed urls for an entity                                                                                           |
| **Management**              | Reset Alert/Condition And Provide Custom Data For Activity   | Resets alert/condition by UID                                                                                                                    |
| **Management**              | Update API Webhook Configuration                             | Creates or updates Webhook configuration for current application/client                                                                          |
| **Management**              | Remove Webhook API Channel                                   | Creates or updates PSA configuration based on client                                                                                             |
| **Management**              | Approve/Reject Devices                                       | Approve or reject devices that are waiting for approval                                                                                          |
| **Management**              | Reset Alert/Condition                                        | Resets alert/condition by UID                                                                                                                    |
| **Management**              | Modify Windows Service Configuration                         | Configures Windows Service startup settings                                                                                                      |
| **Management**              | Reboot Device                                                | Sends a command to restart the computer                                                                                                          |
| **Management**              | List Scripting Options by Device                             | Returns scripting options (built-in actions, custom scripts) available for device                                                                |
| **Management**              | Update Device Information                                    | Change device friendly name, user data, etc.                                                                                                     |
| **Management**              | Get Device Link                                              | Returns link to device                                                                                                                           |
| **Management**              | Control Windows Service                                      | Start/Stop/Restart Windows Service on a device                                                                                                   |
| **Management**              | Schedule Maintenance                                         | Schedule maintenance window for device                                                                                                           |
| **Management**              | Cancel Maintenance                                           | Cancel pending or active maintenance for device                                                                                                  |
| **Management**              | Run Script Or Built In Action                                | Run script or built-in action on a device                                                                                                        |
| **Management**              | Create Location For Organization                             | Creates new location for organization                                                                                                            |
| **Management**              | Update Organization                                          | Change organization name, description and policy mappings                                                                                        |
| **Management**              | Generate Installer                                           | Generates and returns URL for installer for specified organization/location                                                                      |
| **Management**              | Update Location                                              | Change location name, address, description, custom data                                                                                          |
| **Management**              | Change Organization Policy Mappings                          | Update policy assignment for node role(s). Returns list of affected device IDs                                                                   |
| **Organization**            | Create New Organization                                      | Creates new organization with optional list of locations and policy mappings. Template organization ID can be specified to copy various settings |
| **Organization**            | List Organization Locations                                  | Returns list of locations for organization                                                                                                       |
| **Organization**            | Get Organization Information                                 | Returns organization details (policy mappings, locations)                                                                                        |
| **Organization**            | List Users for Organization                                  | Returns list of end-users for organization                                                                                                       |
| **Organization**            | List Organization Documents                                  | Returns organization documents                                                                                                                   |
| **Organization**            | List Organization Devices                                    | Returns list of devices for organization                                                                                                         |
| **Organization Checklists** | Archive Organization Checklists                              | Archive multiple organization checklists                                                                                                         |
| **Organization Checklists** | List Client Checklists                                       | List client checklists with given criteria                                                                                                       |
| **Organization Checklists** | Create Organization Checklists                               | Creates multiple organization checklists                                                                                                         |
| **Organization Checklists** | Update Organization Checklists                               | Updates multiple organization checklists                                                                                                         |
| **Organization Checklists** | Create Organization Checklists From Templates                | Creates multiple organization checklists from templates                                                                                          |
| **Organization Checklists** | Get Client Checklist                                         | Get a client checklist by id                                                                                                                     |
| **Organization Checklists** | Delete An Organization Checklist                             | Deletes an organization checklist by id                                                                                                          |
| **Organization Checklists** | Delete Organization Checklists                               | Deletes organization checklists by id                                                                                                            |
| **Organization Checklists** | Get Organization Checklist Signed URLs                       | Get organization checklist signed urls                                                                                                           |
| **Organization Checklists** | Promote Organization Checklists                              | Promote organization checklists by id                                                                                                            |
| **Organization Checklists** | Restore Organization Checklists                              | Restore multiple organization checklists                                                                                                         |
| **Organization Documents**  | Archive An Organization Document                             | Archives an organization document by id                                                                                                          |
| **Organization Documents**  | Archives Organization Documents                              | Archives multiple organization documents by id                                                                                                   |
| **Organization Documents**  | Create Organization Document                                 | Creates an organization document and returns the document created                                                                                |
| **Organization Documents**  | List All Organization Documents With Field Values            | List all organization documents with field values                                                                                                |
| **Organization Documents**  | Create Organization Documents                                | Creates organization documents and returns the documents created                                                                                 |
| **Organization Documents**  | Update Organization Documents                                | Updates organization documents and returns the documents updated                                                                                 |
| **Organization Documents**  | Delete An Archived Organization Document                     | Deletes an archived organization document by id                                                                                                  |
| **Organization Documents**  | Get Organization Document Signed URLs                        | Get organization document signed urls                                                                                                            |
| **Organization Documents**  | List Organization Documents With Field Values                | List organization documents with field values                                                                                                    |
| **Organization Documents**  | Restore An Organization Document                             | Restores an organization document by id                                                                                                          |
| **Organization Documents**  | Restore Multiple Multi Page Organization Documents           | Restores multiple organization documents by id                                                                                                   |
| **Organization Documents**  | Update Organization Document                                 | Updates an organization document and returns the updated version                                                                                 |
| **Queries**                 | List Uninstalled OS Patches                                  | Returns list of OS patches for which there were no installation attempts                                                                         |
| **Queries**                 | List Pending, Failed And Rejected 3rd Party Software Patches | Returns list of 3rd party Software patches for which there were no installation attempts                                                         |
| **Queries**                 | List Software Update History                                 | Returns 3rd party software patch installation history records (successful and failed)                                                            |
| **Queries**                 | Last Logged On User Report                                   | Returns usernames and logon times                                                                                                                |
| **Queries**                 | List Custom Fields with Details                              | Returns Custom Fields report with additional information about each field                                                                        |
| **Queries**                 | List Health Status by Device                                 | Returns list of device health summary records                                                                                                    |
| **Queries**                 | List Software Inventory                                      | Returns list software installed on devices                                                                                                       |
| **Queries**                 | List OS Update Installations                                 | Returns patch installation history records (successful and failed)                                                                               |
| **Queries**                 | List Antivirus Status by Device                              | Returns list of statues of antivirus software installed on devices                                                                               |
| **Queries**                 | List Raid Controllers                                        | Returns list of RAID controllers                                                                                                                 |
| **Queries**                 | List Raid Drives                                             | Returns list of drives connected to RAID controllers                                                                                             |
| **Queries**                 | List Windows Services                                        | Returns list of Windows Services and their statuses                                                                                              |
| **Queries**                 | List Custom Fields                                           | Returns Custom Fields report                                                                                                                     |
| **Queries**                 | List Computer Systems                                        | Returns computer systems information for devices                                                                                                 |
| **Queries**                 | List Disk Drives                                             | Returns list of physical disks                                                                                                                   |
| **Queries**                 | List Antivirus Threats                                       | Returns list of antivirus threats                                                                                                                |
| **Queries**                 | List Operating Systems by Device                             | Returns operating systems' for devices                                                                                                           |
| **Queries**                 | List Processors                                              | Returns list of processors                                                                                                                       |
| **Queries**                 | List Disk Volumes                                            | Returns list of disk volumes                                                                                                                     |
| **System**                  | List Organizations                                           | Returns list of organizations (Brief mode)                                                                                                       |
| **System**                  | Get Attachment by ID                                         | Returns attachment (image, document)                                                                                                             |
| **System**                  | List All Device Custom Fields                                | Returns list of all custom fields                                                                                                                |
| **System**                  | List Active Alerts (Triggered Conditions)                    | Returns list of active alerts/triggered conditions                                                                                               |
| **System**                  | List Organizations with Locations and Policies               | Returns list of organizations with locations and policy mappings                                                                                 |
| **System**                  | List Device Roles                                            | Returns list of device roles                                                                                                                     |
| **System**                  | List Supported 3rd Party Software                            | Returns available software products (3rd party patching)                                                                                         |
| **System**                  | List Devices (Detailed)                                      | Returns list of devices with additional information                                                                                              |
| **System**                  | List Active Jobs                                             | Returns list of running jobs                                                                                                                     |
| **System**                  | List Locations                                               | Returns flat list of all locations for all organizations                                                                                         |
| **System**                  | List Scheduled Tasks                                         | Returns list of registered scheduled tasks                                                                                                       |
| **System**                  | List Groups (Saved Searches)                                 | Returns list of groups                                                                                                                           |
| **System**                  | List Activities                                              | Returns activity log in reverse chronological order                                                                                              |
| **System**                  | List Devices                                                 | Returns list of devices (basic node information)                                                                                                 |
| **System**                  | List Policies                                                | Returns list of policies                                                                                                                         |
| **System**                  | List Users                                                   | Returns list of users                                                                                                                            |
| **System**                  | Search for Devices                                           | Returns list of entities matching search term                                                                                                    |
| **Ticketing**               | List Ticket Log Entries                                      | Get list of ticket log entries                                                                                                                   |
| **Ticketing**               | List Tickets For Board                                       | Get list of tickets by Board identifier                                                                                                          |
| **Ticketing**               | List Boards                                                  | Get list of boards                                                                                                                               |
| **Ticketing**               | List Contacts                                                | Get list of contacts                                                                                                                             |
| **Ticketing**               | List Ticket Forms                                            | Get list of ticket forms                                                                                                                         |
| **Ticketing**               | Modify Ticket                                                | Modify a ticket on a board.                                                                                                                      |
| **Ticketing**               | Create Ticket                                                | Description coming soon...                                                                                                                       |
| **Ticketing**               | List Users By Type                                           | Returns list of users (contacts, end-user, technician)                                                                                           |
| **Ticketing**               | List Ticket Statuses                                         | Get list of ticket status                                                                                                                        |
| **Ticketing**               | Get Ticket                                                   | Get a single ticket by ID                                                                                                                        |
| **Ticketing**               | Add Comment To Ticket                                        | Add a new comment to a ticket                                                                                                                    |
| **Ticketing**               | List Ticket Attributes                                       | Returns list of the ticket attributes                                                                                                            |
| **Ticketing**               | Ticket Form                                                  | Returns a ticket form with fields                                                                                                                |
