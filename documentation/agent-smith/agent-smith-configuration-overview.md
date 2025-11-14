# Agent Smith configuration overview

{% hint style="info" %}
Agent Smith consists of three main components:

* An open-source agent written in GoLang in the [Rewst GitHub](https://github.com/RewstApp/agent-smith-go)
* The Microsoft [Azure IoTHub](https://azure.microsoft.com/en-us/products/iot-hub) service
* Rewst Crates to configure the IoTHub and interact with agents

Agent Smith operates as an Azure IoT Hub instance, integrated with Rewst workflows for command communication to endpoint agents. The agent software, running as a Windows Service on devices, registers via a webhook trigger in Rewst, creating an IoT Hub entry and receiving configuration data.
{% endhint %}

## Choose the correct IoT Hub subscription&#x20;

The Basic tier of Azure's IoT Hub will not provide the needed cloud-to-device messages functionality for Agent Smith. You can choose the S0 Free tier, but messages will be limited to 8,000 per day. The number of messages you need will depend on how many devices you create in total. Microsoft does not support converting from the Free tier to S1 or above without wiping and reprovisioning the account.

Budget between 50 to 200 messages per day per agent, depending on your workflows. Visit [Microsoft's own documentation](https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-scaling) for specifics!

## Set up Agent Smith

{% hint style="warning" %}
For the Azure integration to work, you’ll need to have an Azure Subscription that includes a Keyvault.

The Rewst integration user setup for the [Microsoft Cloud Integration Bundle](../configuration/integrations/integration-guides/microsoft-cloud-integration-bundle/) may require you to adjust permissions for your Azure subscription. Most commonly, it is recommended to grant the Rewst Service Account with Contributor access to your Azure subscription.
{% endhint %}

1.  Install and authorize our Microsoft Cloud Integration Bundle by navigating to **Configuration > Integrations** in the Rewst platform. This bundle contains an integration for Microsoft Azure.


2. Navigate to **Crates > Crate Marketplace** in the Rewst platform.\
   NOTE: You'll need to install the below Crates in order for Agent Smith setup to complete. Only unpack the Crates in the indicated order, or setup will fail.
   1. Search for and install the **Agent Smith: Device Provisioning** Crate.\
      \
      ![](<../../.gitbook/assets/Screenshot 2025-09-24 at 12.00.30 PM.png>)
   2. Search for and install the **Agent Smith: Service Provisioning** Crate. Unpacking this Crate will install a form named **Agent Smith: Service Configuration.**\
      \
      ![](<../../.gitbook/assets/Screenshot 2025-09-24 at 12.00.55 PM.png>)
3. Navigate to the live **Agent Smith: Service Configuration** form and choose **Action: Create IoT Hub Instance** from the **Action** drop down menu.
4.  Select the proper **Azure Subscription**, **Azure Location**, type in a unique **IoT Hub Name**, and select the desired **IoT Hub Service Tier**.

    <figure><img src="../../.gitbook/assets/Screenshot 2025-02-07 at 2.43.55 PM.png" alt=""><figcaption></figcaption></figure>
5. **Submit** the form and monitor workflow results for success.

### 4. Workaround for installation bug

* Agent Registration Workflow: Update the secret key in the trigger configuration.
  * Open Agent Smith: Agent Registration Workflow.
  * Update the Agent Smith Registration Webhook Trigger.
* Choose **iothub\_registration\_secret i**n the **Secret Key** drop-down selector.

## Provision agents

1. Return to the same **Agent Smith: Service Configuration** form and choose **Display Agent Configuration Instructions**.
2. Choose your **Registration Organization**. The form will display instructions for using PowerShell to configure the Agent for that organization. It also shows how the ORG ID is filled in. If desired, you could use an existing RMM to deploy the agent using variables.\
   \
   ![](<../../.gitbook/assets/Screenshot 2025-02-07 at 2.50.37 PM.png>)

{% hint style="warning" %}
Only Up-to-date versions of PowerShell have been tested to work. Make sure your devices are updated! We suggest you provision one or a few agents to test with before doing mass provisioning.
{% endhint %}

### Test Agent Smith

1. Return to the form and choose **Run PowerShell Code on Agent**
2. Type some PowerShell code into the **Type your PowerShell Here** field, or use what's pre-filled.
3. Monitor the workflow status to see the agent return data.\
   ![](<../../.gitbook/assets/Screenshot 2025-02-07 at 2.54.04 PM.png>)

{% hint style="warning" %}
* Agent Smith uses the Microsoft Azure integration. You'll need to add that as an integration override to any workflows which will use it.
* This includes anything that calls the Run PowerShell subworkflows, such as New Employee, etc.
{% endhint %}

### Agent Smith: Track Agent Inventory In Azure Tables Crate

This Crate will add some additional capabilities to your Agent Smith Deployments. Using it is optional.

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-07 at 2.57.50 PM.png" alt=""><figcaption></figcaption></figure>

Crate features include:

* Using Azure Tables to store additional information about your agent endpoints
* Automatic agent data collection check-ins including installed applications and service, via Task Scheduler
* Automatic restart of the agent if the Service stops, via Task Scheduler

## Uninstall Agent Smith

### Windows

Agent Smith installs itself as a service. You can use PowerShell or the SC command to modify or remove the service. Application logs and data are installed in `C:\ProgramData\RewstRemoteAgent` or whatever root path you've overridden in your environment. Application Program files are in `%ProgramFiles%\RewstRemoteAgent` folders.

### Linux

Agent Smith installs itself as a service. You can use `systemd` and `bash` to stop and remove the service file. Application logs and data are installed in `/etc/rewst_remote_agent` folders. Application program files are in `/usr/local/bin/rewst_remote_agent` folders.

## Use custom PowerShell scripts with Agent Smith

Agent Smith allows PowerShell scripts to be passed via API. To report the script back to Rewst, you'lll need to add a manual webhook action. We recommend using the run PowerShell script subworkflow to handle this for you and if using custom scripts you will need to add this to bottom to ensure the call back to Rewst is made.

```
$postData = $PS_Results | ConvertTo-Json Invoke-RestMethod -Method 'Post' -Uri $post_url -Body $postData -ContentType 'application/json; charset=utf-8
```

## Troubleshoot Agent Smith

* Ensure admin-level account setup, so the service will install as SYSTEM.
* Verify the recent MS PowerShell version on your devices.
* Ensure that no firewalls are preventing communications with Rewst or your IoT Hub. Check our [Rewst Security Configuration Page](https://docs.rewst.help/security) for details.
* Ensure that endpoint security software is not preventing executions or comms.
* Check device connectivity to Azure IoT Hub via MQTT: `<your_iothub_name>.azure-devices.net:8883`.
* Get packet captures from the agent while workflows are running. This can help us determine if the agent is properly communicating with the IoT Hub and/or the Rewst engine.

## Agent Smith Support

Contact the [Rewst Support Team](https://docs.rewst.help/support-and-community/roc-support) if you need help at any time!

In our Discord server, the [#agent-smith ](https://discord.com/channels/936789089703845988/1184866106482110608)channel is a great place for community help with setting up and running Agent Smith. Post your questions and share your successes for how you're using Agent Smith to save time.

## Agent Smith FAQs

* **Am I allowed to customize Agent Smith?**
  * Yes, you're free to [fork and modify it](https://github.com/RewstApp/agent-smith-go).
* **Will new features be added? Can you add Feature X?**
  * Our focus for Agent Smith is on simplicity. Consider adding additional functionality by writing a PowerShell script and kicking it off with a workflow.
* **Does Rewst provide Agent Smith support for older operating systems?**
  * No, support for outdated OS is not available.
* **Will there be MacOS support?**
  * Eventually! If you feel strongly about the timeline for this, add it to our Canny feature request form [here](https://rewst.canny.io/agent-smith).
* **I want to deploy agents to my endpoints in bulk. How should I prepare?**
  * View the separate guide for how to do this [here](bulk-onboarding-with-agent-smith.md).
