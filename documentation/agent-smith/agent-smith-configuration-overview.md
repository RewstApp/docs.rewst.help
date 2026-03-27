# Agent Smith configuration overview

{% hint style="info" %}
Agent Smith consists of three main components:

* An open-source agent written in GoLang in the [Rewst GitHub](https://github.com/RewstApp/agent-smith-go)
* The Microsoft [Azure IoTHub](https://azure.microsoft.com/en-us/products/iot-hub) service
* Rewst Crates to configure the IoTHub and interact with agents

Agent Smith operates as an Azure IoT Hub instance, integrated with Rewst workflows for command communication to endpoint agents. The agent software, running as a Windows Service on devices, registers via a webhook trigger in Rewst, creating an IoT Hub entry and receiving configuration data.

We recommend that anyone who attempts to set up and use Agent Smith be an admin in Microsoft Azure, and well versed in its functionality.
{% endhint %}

Budget between 50 to 200 messages per day per agent, depending on your workflows. Visit [Microsoft's own documentation](https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-scaling) for specifics.

## Set up Agent Smith

{% hint style="success" %}
Unpack the Agent Smith setup Crates at the MSP level. Then, set the [organization variable](../integrations/organization-variables.md#what-is-an-organization-variable) `default_rmm` at the customer level for the child organizations that you want to use with Agent Smith, or use the form unpacked during setup to apply Agent Smith as your RMM for all organizations.&#x20;
{% endhint %}

{% hint style="warning" %}
For the Azure integration to work, you’ll need to have an Azure Subscription that includes a Keyvault.

The Rewst integration user setup for the [Microsoft Cloud Integration Bundle](../integrations/integration-guides/microsoft-cloud-integration-bundle/) may require you to adjust permissions for your Azure subscription. Most commonly, it is recommended to grant the Rewst Service Account with Contributor access to your Azure subscription.
{% endhint %}

1. Install and authorize our Microsoft Cloud Integration Bundle by navigating to **Marketplace > Integrations** in the Rewst platform. This bundle contains an integration for Microsoft Azure, which is necessary to set up and use Agent Smith.
2. Navigate to **Marketplace > Crates** in the Rewst platform.\
   You'll need to install the below Crates in order for Agent Smith setup to complete. Only unpack the Crates in the indicated order, or setup will fail.
   1. Search for and install the `Agent Smith: Device Provisioning` Crate. This will unpack the workflows necessary for registering agents in the Azure IoT Hub. Ensure that the trigger in the **Webhook** accordion menu of the Crate's configuration page is toggled to **Enabled**.\
      \
      ![](<../../.gitbook/assets/Screenshot 2025-09-24 at 12.00.30 PM.png>)
   2. Search for and install the `Agent Smith: Service Provisioning` Crate. Unpacking this Crate will configure the Azure IoT Hub as a gateway for sending commands to endpoints. It will also unpack a form named **Agent Smith: Service Configuration.** You'll use this form to set up and execute all of Agent Smith's capabilities.\
      \
      ![](<../../.gitbook/assets/Screenshot 2025-09-24 at 12.00.55 PM.png>)
3. Navigate to **Automations > Assets > Forms** and search for the `Agent Smith: Service Configuration` form. Click **⋮> View Direct URLs**, then click on the URL of the form.&#x20;
4. Choose **Action: Create IoT Hub Instance** from the **Action** drop-down menu.
5. Use the relevant drop-down selectors to choose the proper:
   1. **Azure Subscription**
   2. **Azure Location.**
6. Type in a unique **IoT Hub Name.**
7. Select the desired **IoT Hub Service Tier**. Check prices in your regions for exact figures. Choosing the correct tier is essential to correctly setting up Agent Smith.
   1. Free Tier:
      1. No Cost
      2. Limited to 8,000 messages per day
      3. Cannot be upgraded to standard without re-provisioning
   2. Standard Tier:
      1. $25 Per Month for one unit in US Locations
      2. 400,000 messages per day per unit
      3. Can be upgraded to higher tiers

{% hint style="info" %}
Budget between 50 to 200 messages per day per agent, depending on your workflows. You won't be able to convert a Free tier deployment to Standard after creation. If you decide to switch later, you will need to deprovision your agents and set Agent Smith up again from the beginning.

Read more about tiers in [Microsoft's own documentation](https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-scaling). Since Rewst uses Cloud-to-Device (C2D) messaging, we can't use the basic tier.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-07 at 2.43.55 PM.png" alt=""><figcaption></figcaption></figure>

8. **Submit** the form and monitor workflow results for success.

## Display agent configuration instructions: Provision agents

This form option gives information about how you should configure your RMM to allow the flow of information between itself and Agent Smith. It will prefill the correct code, which you then copy and paste into your RMM to allow for the management.

1. Return to the same **Agent Smith: Service Configuration** form and choose **Display Agent Configuration Instructions**.
2. Choose your **Registration Organization**. Operations may fail unless your account is a Rewst Admin. The form will display instructions for using PowerShell to configure the agent for that organization. It also shows how the organization ID is filled in. Note that changing the registration organization will update the organization ID in the code snippets.
3. Copy the code relevant to your operating system.&#x20;
4. Follow the given instructions produced by the form to complete steps in your RMM to allow Agent Smith's management. \
   \
   ![](<../../.gitbook/assets/Screenshot 2025-02-07 at 2.50.37 PM.png>)

{% hint style="warning" %}
Only up-to-date versions of PowerShell have been tested to work. Make sure your devices are updated! We suggest you provision one or a few agents to test with before doing mass provisioning.
{% endhint %}

## Configure Agent Smith as your RMM

Fill out the form as follows to set Agent Smith-related organization variables in Rewst.

1. Return to the same **Agent Smith: Service Configuration** form and choose **Display Agent Configuration Instructions**.
2. Choose **Configure Agents Smith as RMM** from the **Action** drop-down selector. It may take a moment for the form to register this selection and update the following fields accordingly.
3. Check the **Set Agent Smith as a Possible "RMM Agent"** box. This will set Agent Smith as a fallback option for your company when other options are not available.
4. Optionally:
   1. Check the **Set as "Default RMM"** box if you wish to set Agent Smith as the default RMM for your MSP.
   2. Check the **Set as Default for Sub-Orgs** box to set your indicated settings for all child organizations, via inheritance.
5. Click **Submit**.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-13 at 4.39.25 PM.png" alt="" width="335"><figcaption></figcaption></figure>

## Deploy to Devices

This option is recommended for users who have an existing RMM, but are unsatisfied with its data transfer speed in Rewst. You can continue using your RMM while taking advantage of Agent Smith to deploy to devices for a customer. Follow the first two sections of the Agent Smith setup process. Then, fill out the form as follows to set the organization variables in Rewst for this particular setup.

Select the **Choose Devices** option to reveal a drop-down selector for all available devices.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-05 at 3.19.52 PM.png" alt="" width="375"><figcaption></figcaption></figure>

## Test Agent Smith

1. Return to the form and choose **Run PowerShell Code on Agent**
2. Type your desired PowerShell code into the **Type your PowerShell Here** field, or use the pre-filled code.
3. Monitor the workflow status to see the agent return data.\
   ![](<../../.gitbook/assets/Screenshot 2025-02-07 at 2.54.04 PM.png>)

{% hint style="warning" %}
Agent Smith uses the Microsoft Azure integration. You'll need to add that as an integration override to any workflows which will use it. This includes anything that calls the Run PowerShell subworkflows, such as New Employee, etc.
{% endhint %}

## Optional: Unpack the Agent Smith: Track Agent Inventory In Azure Tables Crate

This Crate will add some additional capabilities to your Agent Smith deployments. Using it is optional. See our total Crate setup and user guide [here](agent-smith-configuration-overview.md#agent-smith-track-agent-inventory-in-azure-tables-crate).&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/Screenshot 2026-02-12 at 12.47.39 PM.png" alt="" width="217"><figcaption></figcaption></figure></div>

Crate features include:

* Using Azure tables to store additional information about your agent endpoints
* Automatic agent data collection check-ins including installed applications and service, via Task Scheduler
* Automatic restart of the agent if the service stops, via Task Scheduler

## Uninstall Agent Smith

### Windows

Agent Smith installs itself as a service. You can use PowerShell or the SC command to modify or remove the service. Application logs and data are installed in `C:\ProgramData\RewstRemoteAgent` or whatever root path you've overridden in your environment. Application program files are in `%ProgramFiles%\RewstRemoteAgent` folders.

### Linux

Agent Smith installs itself as a service. You can use `systemd` and `bash` to stop and remove the service file. Application logs and data are installed in `/etc/rewst_remote_agent` folders. Application program files are in `/usr/local/bin/rewst_remote_agent` folders.

## Use custom PowerShell scripts with Agent Smith

Agent Smith allows PowerShell scripts to be passed via API. To report the script back to Rewst, you'lll need to add a manual webhook action. We recommend using the run PowerShell script subworkflow to handle this for you. If using custom scripts, you'll need to add the below code to the bottom of your script to ensure that the call back to Rewst is made.

```
$postData = $PS_Results | ConvertTo-Json Invoke-RestMethod -Method 'Post' -Uri $post_url -Body $postData -ContentType 'application/json; charset=utf-8
```

## Troubleshoot Agent Smith

{% hint style="info" %}
In our Discord server, the [#agent-smith ](https://discord.com/channels/936789089703845988/1184866106482110608)channel is a great place for community help with setting up and running Agent Smith. Post your questions and share your successes for how you're using Agent Smith to save time. Or, ask for assistance from Rewst Support in your dedicated Discord support channel.&#x20;
{% endhint %}

* Ensure admin-level account setup, so the service will install as SYSTEM.
* Verify the recent MS PowerShell version on your devices.
* Ensure that no firewalls are preventing communications with Rewst or your IoT Hub. Check our [Rewst Security Configuration Page](https://docs.rewst.help/security) for details.
* Ensure that endpoint security software is not preventing executions or communications.
* Check device connectivity to Azure IoT Hub via MQTT: `<your_iothub_name>.azure-devices.net:8883`.
* Get packet captures from the agent while workflows are running. This can help us determine if the agent is properly communicating with the IoT Hub and/or the Rewst engine.

### Agent Smith Crate installation bug

We've received rare reports of the setup Crates improperly generating secret keys. If you receive an error during setup, try the following steps.

1. Navigate to **Automations > Workflows**.
2. Search for and open the **Agent Smith: Agent Registration** workflow.
3. Click <img src="../../.gitbook/assets/Screenshot 2026-02-13 at 4.12.42 PM.png" alt="" data-size="line">to open the edit trigger menu.
4. Scroll down to **Trigger Parameters**.
5.  Choose **iothub\_registration\_secret** in the **Secret Key** drop-down selector.\
    <br>

    <figure><img src="../../.gitbook/assets/Screenshot 2026-02-13 at 4.14.09 PM.png" alt=""><figcaption></figcaption></figure>
6. Click **Submit**.&#x20;

