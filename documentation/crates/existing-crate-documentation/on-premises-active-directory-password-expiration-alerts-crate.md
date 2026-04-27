# On-Premises Active Directory Password Expiration Alerts Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the On-Premises Active Directory Password Expiration Alerts Crate do?

Our On-Premises Active Directory Password Expiration Alerts Crate automates the process of monitoring password expiration for on-premises Active Directory users, ensuring that users are notified well in advance. By sending timely email alerts, it helps maintain security and minimizes disruptions by prompting users to update their passwords before they expire.

This workflow is designed for on-premises Active Directory only. It does not monitor or interact with cloud-based directories like Entra ID. This Crate doesn't perform password resets; it only sends notifications. Users must update their passwords manually through the appropriate channels. The workflow does not provide real-time alerts. There may be a slight delay between when a password expiration is detected and when the notification is sent.

### How the Crate works <a href="#how-the-crate-works" id="how-the-crate-works"></a>

* Automatically checks for user passwords expiring in 14, 7, 3, and 1 day, ensuring users are well-informed ahead of time
* Sends email alerts to users, reminding them to change their passwords before the expiration date, reducing the risk of account lockout
* Ensures that passwords are updated promptly, reducing the likelihood of unauthorized access due to expired passwords
* Streamlines the password management process, lowering the frequency of IT support tickets related to password issues and freeing up resources for other critical tasks

The workflow is initiated by a scheduled task that runs a PowerShell script at predefined intervals.&#x20;

If Rewst's [PowerShell interpreter](../../settings/powershell-interpreter.md) tool is installed, Crate workflows which have multiple-system dependencies will have increased efficiency with faster and more consistent cloud-native executions that are completed in seconds.

## Crate prerequisites

One of the following RMM integrations must be set up before unpacking this Crate:

* [ConnectWise Control](../../integrations/integration-guides/connectwise-control-screenconnect.md)
* [Datto RMM](../../integrations/integration-guides/datto-rmm-integration-setup.md)
* [ImmyBot](https://app.gitbook.com/u/kmMNMlugUvf2cfCtyBQgNnIYH1H2)
* [Kaseya VSA](../../integrations/integration-guides/kaseya-vsa-integration-setup.md)
* [Kaseya VSA X](../../integrations/integration-guides/kaseya-vsa-x-integration-setup.md)
* [N-able (NAble)](../../integrations/integration-guides/n-able-n-sight-integration.md)
* [NinjaOne](https://app.gitbook.com/o/mdGoyUomPKsvu1TSazxc/s/AQQ1EHVcEsGKBPVHmiav/documentation/configuration/integrations/integration-guides/ninjaone-integration-setup)
* [SuperOps](../../integrations/integration-guides/superops-integration.md)

The following must be set up before unpacking this Crate:

* [PowerShell](../../jinja/use-powershell-scripts-in-rewst.md) scripts
* `password_expiry_crate_admin_email`  [organization variable](../../integrations/organization-variables.md#what-is-an-organization-variable)

## Unpack the On-Premises Active Directory Password Expiration Alerts Crate <a href="#unpack-the-browse-rewst-form-triggers-within-a-form-and-attach-to-a-ticket-crate" id="unpack-the-browse-rewst-form-triggers-within-a-form-and-attach-to-a-ticket-crate"></a>

1. Navigate to **Marketplace > Crates** in the left side menu Rewst platform.
2.  Search for `On-Premises Active Directory Password Expiration Alerts`.​



    ![](<../../../.gitbook/assets/image (259).png>)
3. Click on the Crate tile to begin unpacking.
4. Click **Unpack Crate**.
5. Click **Continue**.
6. Enter **Time Saved** under **Crate Configuration**.
7. Ensure that **Enabled** is toggled on under **Configure Triggers**.\
   Note that you have the option under the **Cron Job** accordion menu to activate the Crate for all future organizations in addition to the current one. You may also set [trigger criteria](../../automations/intro-to-triggers/trigger-criteria.md) or [integration overrides](../../automations/intro-to-triggers/).
8. Click **Unpack**.

### Test the Crate <a href="#test-the-crate" id="test-the-crate"></a>

{% hint style="info" %}
Since this workflow sends real emails to real users, consider testing against a smaller organization or one where you control the mailboxes, so you don't accidentally notify end users during your test run. Alternatively, you could temporarily mock the **alert\_user** task to prevent emails from going out while you validate the rest of the flow.
{% endhint %}

1. Navigate to **Automations > Workflows** in the left side menu of your Rewst platform.
2. Search for `Alert: Password Expiry - Notify End User`.
3. Click on the workflow to view it in the Workflow Builder.
4. Click **Test**.
5. Click **Run Test** to confirm.&#x20;
6. You'll see a green success message at the top of your screen if the execution is successful. You'll see a red failure message if the execution fails. Click **View Results** for a more detailed breakdown of each.
7. Confirm that the **check\_expiring\_passwords** task successfully connected to the domain controller and returned data. If it failed, check that your RMM integration is properly configured and the domain controller is reachable.
8. Check your inbox or the inbox of the test users to confirm the password expiry notification emails were actually delivered.
9. If no passwords are currently expiring in your environment, the workflow will follow the No Expiring Passwords path of the workflow, and end cleanly at the **no\_expiring\_passwords** task. This is still a successful test, but there was nothing to alert on.

## Organization variables associated with this Crate

{% hint style="info" %}
For more on organization variables and how to use them, see our org variable documentation [here](https://docs.rewst.help/documentation/configuration/organization-variables).

Organization variables not found in our standard organization variables documentation, such as the ones listed below. are typically system variables that are handled by integration mappings.

If you haven't done so already, we recommended that you run the [Configure Organization Variables Crate](https://docs.rewst.help/documentation/crates/existing-crate-documentation/configure-organization-variables), which will help you set org variables that are relevant to you and your customer's environments.
{% endhint %}

The organization variable `password_expiry_crate_admin_email` must be set if you want a fallback email address for users who don't have one on file. You can check this under the organization variable menu in Rewst.

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
