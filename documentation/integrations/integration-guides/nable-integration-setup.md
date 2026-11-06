# N-able N-central integration

{% hint style="warning" %}
**N-central Required Version**

The new REST API endpoints are only available on N-central with a version of 2023.9 or above. Contact your N-able Representative to be upgraded where applicable.

If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the N-able N-central integration do?

Our N-able N-central integration allows MSPs to seamlessly interact with N-central's powerful RMM capabilities through Rewst, facilitating device management, task automation, and efficient operational workflows.

### Integration use cases

* Automatically synchronize device and customer data with your Rewst workflows.
* Execute and manage scheduled tasks directly from Rewst.
* Run automated Powershell scripts remotely to maintain and configure devices.

## Integration prerequisites

* N-able N-central version 2023.9 or above
* A dedicated API user created in N-able N-central
* A JSON web token from N-able N-central
* Powershell scripts configured for API access in N-able N-central
* Defined organization variables in Rewst

## Set up the N-able N-central integration

Set up steps in N-able N-central

1. Navigate to **Administration > User Management > Users**.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.03.55@2x.jpg>)
2. Click **Create User** to create a new user specifically for API access. Name the user something that will easily identify its purpose.
3. Assign appropriate permissions required for your automations On the **Access Groups and Roles** tabs.
   1. **Roles**: Create a role under **user management > roles** for a full API user. Name it administrator and set all the properties to manage. A reference sheet can be found here under [N-able API user permissions](https://documentation.n-able.com/N-central/userguide/Content/User_Management/Role%20Based%20Permissions/role_based_permissions_API_user.htm).
   2. **Access Groups**: Set this to **All**.
4. Click the **User Details** tab. Click **User Information**.
5. Check **MFA Not Required** to on.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-03-31 at 10.54.36 AM.png>)
6. Click into the **API Access** tab.
7. Check **API Only User** to on.
8. Click **Save**.
9. Click **Generate JSON Web Token**.
10. Securely copy the generated API key. You’ll need this information for the next setup steps in Rewst.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-03-31 at 19.06.38@2x.jpg" alt=""><figcaption></figcaption></figure>

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `N-able N-central` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.12.59.jpg>)
3. Click on the integration tile to launch the configuration setup page.
4. Under **Parameters**, enter the information copied from N-able N-central into its relevant field:
   1. **API Key:** The JSON Web Token generated on the API user you created
   2. **Base URL:** The base URL of your N-able N-central environment, e.g `rewst.n-able.com` if different from the resource server hostname
5. Click **Save Configuration**.
6. Rewst will do a quick validation of your input.Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.

### Run Powershell via RMM: Script setup

To run Powershell on devices via the RMM, you must create the script in your N-able repository and enable its access for use over the API, as per N-able security policies.

{% hint style="info" %}
To complete all the needed script setup steps in N-able N-central, you'll need to be assigned their Default Administrator Role.
{% endhint %}

1. Navigate to **Configuration > Scheduled Tasks > Script/Software Repository** in N-able.
2. Click **Add > Scripting**.\
   ![](<../../../.gitbook/assets/Screenshot 2025-07-24 at 12.07.14 PM.png>)
3. Name the script `Rewst (Powershell)`.
4. Enter `Executes Powershell sent via API from Rewst` into the **Description** field.
5. Download the provided PS1 file from the bottom of this instruction section. Update your Powershell script's `$rewst_base_url` variable to match your Rewst Instance URL, using the table provided at the bottom of this section. You can identify which instance you are on by referencing the URL you use to access Rewst. The content of the **Command Line Parameters** field will automatically populate when you upload the file.\
   Example of correct base URL: `https://engine.rewst.io/webhooks/custom/action`
6. Click **Browse** to upload the edited file into N-able N-central.
7. Click **Ok**.
8.  Navigate to **Configuration > Scheduled Tasks > Script/Software Repository.**<br>

    <figure><img src="../../../.gitbook/assets/image (81) (1).png" alt=""><figcaption></figcaption></figure>
9. Enable **API Access** for the script.
10. Note the **Repository ID**.
11. In Rewst, [create an organization variable](../organization-variables.md#manually-add-a-new-organization-variable) named `nable_rewst_powershell_script_id` with the Repository ID as its value. Set this organization variable as default.

| Rewst URL        | Base URL            |
| ---------------- | ------------------- |
| app.rewst.io     | engine.rewst.io     |
| app.pdx.rewst.io | engine.pdx.rewst.io |
| app.eu.rewst.io  | engine.eu.rewst.io  |
| app.rewst.eu     | engine.rewst.eu     |
| app.rewst.asia   | engine.rewst.asia   |

{% hint style="info" %}
The org variable is only currently required as there is no way to search for a script with the existing API endpoints.
{% endhint %}

{% file src="../../../.gitbook/assets/run-nable-powershell.ps1 (1).zip" %}



## Use custom PowerShell scripts with your RMM integration

If you're writing custom PowerShell scripts to use and be run with your RMM integration, you'll need to manually add webhook calls. Any custom script will time out if used without first adding the webhook calls. The use of standard built-in Rewst scripts with your RMM does not require you to add the calls.

* The webhook calls everyone doing this custom scripting should use will always be as follows.

```

### Send all the data back to RewstyRewst ###



$postData = $PS_Results | ConvertTo-Json
Invoke-RestMethod -Method 'Post' -Uri $post_url -Body $postData -ContentType 'application/json; 
charset=utf-8'
```

1. Navigate to **Automation > Workflows** in Rewst.
2. Create a new workflow and name it with something short and descriptive, such as `Test N-able Integration`.
3. Add the action **List Agents** to the workflow builder canvas, by dragging it from the left pane.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.28.49.jpg>)
4. Add a trigger to your test workflow by clicking <img src="../../../.gitbook/assets/Screenshot 2025-02-21 at 11.13.39 AM.png" alt="" data-size="line">. Name your trigger whatever you’d like.
5. Click into the trigger’s settings.
6. Toggle **Enabled** to on.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.29.17.jpg>)
7. Set the Trigger Type to **Core - Always Pass**.
8. Click ![](<../../../.gitbook/assets/Screenshot 2025-03-13 at 6.14.27 PM.png>) next to **Integration Overrides**. Add **N-able N-central** as your integration override.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.29.51.jpg>)
9. In the **Activate Trigger To Run For** section, keep **Selected Organization** toggled on. Toggle **All current and future managed organizations** on, or choose just one or individually selected organizations from the **Organizations** drop-down selector.\
   \
   ![](<../../../.gitbook/assets/CleanShot 2025-03-31 at 19.30.35.jpg>)
10. Click **Submit** to save your trigger.
11. Click **Publish** to save your changes.
12. Click Test to run your workflow. Note that this will bring up a drop-down selector to choosing organizations.
13. Select your MSP level.
14. Click **Test** and confirm that the execution finishes without errors.\
    <br>

    <figure><img src="../../../.gitbook/assets/CleanShot 2025-03-31 at 19.31.20.jpg" alt=""><figcaption></figcaption></figure>
15. If the test for your MSP is successful, do the same test again. At this point in your steps, select a client organization instead, and ensure that it finishes with no errors.

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Crates related to the N-able N-central integration

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="image">Cover image</th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Run Powershell script on Selected Devices</strong></td><td data-object-fit="cover"><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 2.59.54 PM.png">Screenshot 2025-11-13 at 2.59.54 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md">run-powershell-script-on-selected-devices-crate.md</a></td></tr><tr><td><strong>Agent Smith: Device Provisioning [Install First/ Install Second]</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.00.37 PM.png">Screenshot 2025-11-13 at 3.00.37 PM.png</a></td><td><a href="../../agent-smith/agent-smith-configuration-overview.md">agent-smith-configuration-overview.md</a></td></tr><tr><td><strong>Just in Time Admin Access</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.01.35 PM.png">Screenshot 2025-11-13 at 3.01.35 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/just-in-time-admin-access-crate.md">just-in-time-admin-access-crate.md</a></td></tr><tr><td><strong>Windows 11 Compatibility Checker</strong></td><td data-object-fit="cover"><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.02.29 PM.png">Screenshot 2025-11-13 at 3.02.29 PM.png</a></td><td></td></tr><tr><td><strong>Bulk Move Users to Specified OU</strong></td><td><a href="../../../.gitbook/assets/Screenshot 2025-11-13 at 3.02.05 PM.png">Screenshot 2025-11-13 at 3.02.05 PM.png</a></td><td><a href="../../crates/existing-crate-documentation/bulk-move-users-to-specified-ou-crate.md">bulk-move-users-to-specified-ou-crate.md</a></td></tr></tbody></table>

## Troubleshoot the N-able N-central integration

* **API authentication errors**: Verify JSON Web Token permissions and validity.
* **PowerShell script execution issues**: Check script API access permissions in N-able.

## Current limitations

There is currently no way to identify a domain controller via the N-able REST API. You must manually set the hostname of the preferred DC. Do this using the organization variable form that was discussed during your onboarding. The end result will be an organizational variable called **preferred\_domain\_controller** and a value of the hostname of that client's DC.

## N-able N-central actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).
{% endhint %}

For detailed endpoint documentation, log in to your N-able account or view their API documentation [here](https://documentation.n-able.com/).

<table data-search="false"><thead><tr><th>Category</th><th>Action</th><th>Description</th></tr></thead><tbody><tr><td><strong>Access Groups</strong></td><td>Create Device Type Access Group</td><td>Creates a new device type access group with the specified details. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Access Groups</strong></td><td>Create Organization Unit Type Access Group</td><td>Creates a new organization unit type access group with the specified details. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Access Groups</strong></td><td>Get Access Group Details</td><td>Retrieves detailed information for a specific Access Group, including its name, type, and associated devices or users. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Access Groups</strong></td><td>List Access Group Related Links</td><td>Description coming soon...</td></tr><tr><td><strong>Access Groups</strong></td><td>List Access Groups Information for Org Unit</td><td>Retrieves access group information for an organization unit with a specific id. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Active Issues</strong></td><td>List Active Issues</td><td>Fetch a list of active issues for the given organization unit.</td></tr><tr><td><strong>Custom Properties</strong></td><td>Get Device Custom Property</td><td>Get the device custom property for the given device id and property id. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Custom Properties</strong></td><td>Get Device Default Custom Property Information</td><td>Retrieves default custom properties information. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Custom Properties</strong></td><td>Get Device Custom Properties</td><td>Retrieves custom properties list for a device. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Custom Properties</strong></td><td>Get Organization Unit Custom Property</td><td>Get the organization unit custom property for the given organization unit id and property id</td></tr><tr><td><strong>Custom Properties</strong></td><td>List Organization Custom Properties</td><td>Get the list of organization unit custom properties for the given organization unit id</td></tr><tr><td><strong>Custom Properties</strong></td><td>Update Default Organization Unit Custom Property</td><td>Update the default organization unit custom property for the given organization unit id and property id</td></tr><tr><td><strong>Custom Properties</strong></td><td>Update Device Custom Property</td><td>Modifies one custom property for a device. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Custom Properties</strong></td><td>Update Organization Unit Custom Property</td><td>Update the organization unit custom property for the given organization unit id and property id</td></tr><tr><td><strong>Customers</strong></td><td>List Customers</td><td>List Customers</td></tr><tr><td><strong>Device Filters</strong></td><td>List Device Filters</td><td>Retrieves the list of filters from N-central for the logged in user. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Devices</strong></td><td>Get Computer</td><td>Get Computer</td></tr><tr><td><strong>Devices</strong></td><td>Get Service Monitor Status</td><td>Retrieves the status of the service monitoring tasks for a given device.</td></tr><tr><td><strong>Devices</strong></td><td>List Computers</td><td>List Computers</td></tr><tr><td><strong>Devices</strong></td><td>List Organization Unit Devices</td><td>Retrieves the list of devices from N-central for the logged in user.</td></tr><tr><td><strong>Generic Request</strong></td><td>N-central API Request</td><td>Generic action for making authenticated requests against the N-able N-central API</td></tr><tr><td><strong>Job Statuses</strong></td><td>List Job Statuses</td><td>Fetch a list of job statuses for the given organization unit.</td></tr><tr><td><strong>Maintenance Windows</strong></td><td>Add Maintenance Windows to Devices</td><td>Adds a set of maintenance windows for a given device. NOTE: This endpoint is in preview. The provided list of maintenance windows applies to every device in the list</td></tr><tr><td><strong>Maintenance Windows</strong></td><td>Delete Device Patch Maintenance Windows</td><td>Deletes patch maintenance windows by given list of Schedule IDs. Only supports Patch maintenance windows created at the device level. NOTE: This endpoint is in preview</td></tr><tr><td><strong>Maintenance Windows</strong></td><td>List Maintenance Windows For A Device</td><td>Retrieves all maintenance windows for a given device. NOTE: This endpoint is in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Create Customer</td><td>Creates a new customer with the specified details. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Create Service Organization</td><td>Creates a new service organization with the specified details. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Get Customer</td><td>Returns a customer. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Get Organization Unit</td><td>Returns an organization unit. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Get Service Organization</td><td>Returns a service organization. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>List Child Organization Units</td><td>Returns a list of all organization units under the specific organization unit. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>List Customer Sites</td><td>Returns a list of all sites under a customer. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>List Organization Units</td><td>Returns a list of all organization units</td></tr><tr><td><strong>Organization Units</strong></td><td>List Service Organization Customers</td><td>Returns a list of all customers under a service organization. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>List Sites</td><td>Returns a list of all sites</td></tr><tr><td><strong>Organization Units</strong></td><td>List Users in Organization Unit</td><td>Retrieves the list of users from N-central for the logged in user.</td></tr><tr><td><strong>Organization Units</strong></td><td>Create Site</td><td>Creates a new site with the specified details. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Organization Units</strong></td><td>Get Site</td><td>Returns a site. NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Psa</strong></td><td>Get Custom PSA Ticket Details</td><td>Retrieves detailed information for a specific Custom PSA Ticket. Exclusive to CUSTOM PSA Integrations only. NOTE: This is in preview</td></tr><tr><td><strong>Psa</strong></td><td>List Custom Psa Related Links</td><td>NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Psa</strong></td><td>List Custom Psa Tickets Related Links</td><td>NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Psa</strong></td><td>List Standard Psa Related Links</td><td>NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Psa</strong></td><td>Validate Standard PSA Credentials</td><td>Validates the credentials for the standard PSA system (Tigerpaw only). NOTE: This endpoint is currently in a preview stage</td></tr><tr><td><strong>Tasks</strong></td><td>Create Scheduled Task</td><td>Create Scheduled Task</td></tr><tr><td><strong>Tasks</strong></td><td>Get Device Tasks</td><td>Get Scheduled Tasks for a Device</td></tr><tr><td><strong>Tasks</strong></td><td>Get Task Info by ID</td><td>Get Task Info by ID</td></tr><tr><td><strong>Tasks</strong></td><td>Get Task Status by ID</td><td>Get Task Status by ID</td></tr><tr><td><strong>Tasks</strong></td><td>Get Detailed Task Status Info by ID</td><td>Get Detailed Task Status Info by ID</td></tr><tr><td><strong>User Roles</strong></td><td>Create User Role</td><td>Add a new user role for an organization unit and return the role id</td></tr><tr><td><strong>User Roles</strong></td><td>Get User Role</td><td>Returns a user role for a given organization unit and user role id</td></tr><tr><td><strong>User Roles</strong></td><td>List User Roles</td><td>Fetch a list of user roles for a given organization unit</td></tr></tbody></table>
