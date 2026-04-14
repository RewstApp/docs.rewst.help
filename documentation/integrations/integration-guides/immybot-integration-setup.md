---
description: This document outlines the requirements and setup for the ImmyBot integration.
---

# ImmyBot integration

{% hint style="info" %}
&#x20;If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

{% hint style="warning" %}
ImmyBot does not suppot multi-instance integration. For more on this topic, see our documentation [here](../multi-instance-integration/),&#x20;
{% endhint %}

## What does the ImmyBot integration do?

Our ImmyBot integration enables the automation of remote machine management and monitoring. Use the ImmyBot API within Rewst workflows to gather detailed information and perform various operations on remotely managed machines, people, software, and scripts.

## Set up the ImmyBot integration

### Set up steps in ImmyBot

Before configuring the Rewst integration,  you'll need to get the application ID and client secret value from your ImmyBot account. To retrieve these, your permissions in ImmyBot must be set to System Administrator. If your account was previously designated as Admin, ImmyBot automatically granted you the permission level of System Administrator (Legacy) in their recent permissioning change update. This is sufficient to set up the integration with Rewst.

Please refer to [ImmyBot's Documentation](https://docs.immy.bot/azure-graph-permissions-setup.html) for up-to-date instructions on retrieving your API key information. Once you have the client secret, store the value somewhere safe. You'll need it for further set up steps in Rewst.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `ImmyBot` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-05-05 at 3.42.15 PM.png>)
3. Click on the integration tile to launch the configuration setup page.
4. Enter your ImmyBot **Hostname**. Click **Next**.
5. Under **Azure App Registration**, enter the information copied from ImmyBot into the relevant fields:
   * **Microsoft Tenant ID** - The ID of the Microsoft 365 Tenant associated with your ImmyBot instance
   * **Application ID -** The Application ID of the Azure Enterprise App that Rewst will use to authenticate with ImmyBot
   * **Client Secret -** The Client Secret of the Azure app registration Rewst will use to authenticate with ImmyBot
6. Click **Next**.
7. Click the link that appears on the integration configuration screen to navigate to ImmyBot's Persons Settings. Create a new Person for Rewst to use. Use your primary Tenant, and set the AD External ID field value.
8. Click **Continue** to create your user and assign the admin Role.
9. Click **Test configuration**. If the integration is working properly, a green confirmation message will appear at the top of your screen.&#x20;

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Triggers for ImmyBot integration

| Trigger type name     | Type    | Description                                                         |
| --------------------- | ------- | ------------------------------------------------------------------- |
| New Computer Detected | Polling | Triggers when new computer is found that has not yet been onboarded |

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

| Category                | Action                       | Description                                                                                                |
| ----------------------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Assignments**         | List Target Assignments      | Get a list of target assignments (deployments) available                                                   |
| **Assignments**         | List Recommended Assignments | Get a list of pre-configured target assignments (deployments) that can be approved or dismissed            |
| **Assignments**         | Create Target Assignment     | Create a new target assignment (deployment) for a software or task                                         |
| **Assignments**         | Update Target Assignment     | Updates an existing target assignment (deployment) for a software or task                                  |
| **Assignments**         | Delete Target Assignment     | Delete an existing target assignment (deployment) for a software or task                                   |
| **Auth**                | Check Auth                   | Description coming soon...                                                                                 |
| **Computers**           | List Computers               | Get a list of computers                                                                                    |
| **Computers**           | Get Computer                 | Get a computer by ID                                                                                       |
| **Computers**           | Assign Person to Computer    | Updates an existing target device with a primary user                                                      |
| **Generic Request**     | ImmyBot API Request          | Generic action for making authenticated requests against the ImmyBot API                                   |
| **Maintenance Actions** | List Actions For Computer    | Get a list of available maintenance actions for a given computer                                           |
| **People**              | List People                  | Get a list of People                                                                                       |
| **Scripts**             | List Scripts                 | Get a list of scripts available in ImmyBot                                                                 |
| **Scripts**             | Get Script                   | Get a script by ID                                                                                         |
| **Scripts**             | Get Script References        | Gets any software, software versions or tasks referencing a given script                                   |
| **Scripts**             | Create Script                | Creates a new script in ImmyBot                                                                            |
| **Scripts**             | Run Script                   | Runs a script defined in ImmyBot against a target computer                                                 |
| **Scripts**             | Run Ad Hoc Script            | Runs an on demand script against a computer in ImmyBot                                                     |
| **Service**             | Run Immy Service             | Allows you to run target assignments, maintenance actions, install software or onboard a list of computers |
| **Sessions**            | List Sessions                | Get a list of maintenance sessions                                                                         |
| **Software**            | List Software                | Get a list of software                                                                                     |
| **Software**            | Get Software                 | Get a software entry by ID                                                                                 |
| **Software**            | Upload Software Installer    | Upload a new software installer                                                                            |
| **Software**            | Analyze Software Installer   | Analyze a software installer to automatically gather details about it in ImmyBot                           |
| **Software**            | Fast Create Software         | Create a software and a corresponding software version from an uploaded installer or URL                   |
| **Software**            | Search Inventory Software    | Searches across computer inventory for installed software matching the given name                          |
| **Tasks**               | Create Task                  | Creates a new maintenance task in the local environment                                                    |
| **Tenants**             | List Tenants                 | Retrieve a list of tenants from ImmyBot                                                                    |
| **Tenants**             | Get Tenant Preferences       | Get preferences for a given tenant in ImmyBot                                                              |
