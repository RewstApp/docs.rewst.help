---
icon: hexagon
---

# Integrations

## What is an integration?

_Integrations_ are a core part of Rewst. Simply put, an integration is the successful linking of the Rewst platform and a separate tool, to allow the free back and forth flow of information between platform and tool. Integrations are achieved with a variety of setup steps that will differ depending on the type of tool—PSA versus RMM, for example—and brand of tool type.

## Why use integrations?

Once you’ve set up an integration, you can unpack Crates to achieve automations that depend on those integrated tools. More on Crates and how unpacking works can be found in our Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates).

## Custom integrations

If Rewst doesn’t have an integration for your particular tool, you have the option to build one custom. Any tool that has an API can be integrated with Rewst via custom integration. We recommend that new Rewst users start with stock integrations, and complete all training in Cluck University before attempting custom integration builds.

Our intro to custom integrations can be found [here](https://docs.rewst.help/documentation/integrations/custom-integrations). Information on how to set up custom integrations can be found [here](https://docs.rewst.help/documentation/integrations/custom-integrations/custom-integrations-v2).

## View integrations in Rewst

Access integrations that are both installed and available for installation in the Rewst platform by navigating to **Marketplace > Integrations** in the left side menu.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-06 at 10.10.39 AM.png" alt=""><figcaption></figcaption></figure>

### View installed integrations

Uninstall any installed integration by clicking the ⋮ on its integration tile. You’ll be asked to confirm that you want to **Delete** the integration in a new dialogue. Click on any installed integration tile to view its configuration page.

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-05 at 4.13.05 PM.png" alt=""><figcaption></figcaption></figure>

## Set up an integration

{% hint style="warning" %}
Clicking on any of the available integrations under the **Installed Integrations** section will automatically begin that installation.
{% endhint %}

The information needed to set up an integration will differ slightly for each integration. Some may ask for an API Key, while some may require you to list scopes or domains. The same basic principal applies for setting up all integrations: you'll pull information from the app you want to integrate with Rewst, input it into Rewst's configuration page for that integration, and link the two tools.

Each of our integrations has a separate integration setup and configuration guide, organized by type of integrated tool in this documentation site under the **Documentation > Integrations > Individual integration documentation** section of the left side documentation menu.

In the Rewst platform, search for any of Rewst’s integrations in the **Find Integrations** search bar at the top right of the Integrations page.

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-05 at 4.20.10 PM.png" alt=""><figcaption></figcaption></figure>

Click the **+New** button to reveal two options for how to set up a custom integration:

1. **New Integration**
2. **Add OpenAPI Integration**

Alternatively, you can kickoff the custom integration setup process by clicking **+ Add New Integration** further down the page in the **Get More Integrations** section.

<figure><img src="../../.gitbook/assets/Screenshot 2025-02-05 at 4.20.53 PM.png" alt=""><figcaption></figcaption></figure>

## Map your organizations to finish integrating

### What is organization mapping?

_Organization mapping,_ or _org mapping_ for short, is the process of connecting each Rewst integration with your child organizations, enabling automations that leverage that integration to work for your customers. When setting up your integrations, this is frequently the last step.

Org mapping isn't necessary for a few of our integrations because the tool you're integrating with doesn't itself have a concept of organizations. When this is the case for a particular integration, we'll call that out in that integration's setup documentation.

{% hint style="warning" %}
Organization mapping for Microsoft integrations is slightly different than the process outlined on this page. Refer to the video on mapping and consenting organizations for the Microsoft Cloud bundle.
{% endhint %}

For org mapping to work properly, it's best to aim for having the names of organizations in Rewst match the names of organizations in your PSA.  If they don't, you can make the mapping match manually, but having 1:1 names will speed up the mapping process and have you reap the benefits of automation more quickly.

Additionally, we recommend that you unpack the [Add Client to Rewst Crate](../crates/existing-crate-documentation/add-client-to-rewst-setup.md) when onboarding into Rewst to prepare for easier org mapping.&#x20;

### How to map organizations: Org mapping

{% hint style="info" %}
Note that the mapping menu won't be visible during initial integration set up. It appears at the bottom of that integration's configuration page after you click **Save Configuration**. Once you've saved the configuration, you can go back into that installed integration later on via the Integrations menu to update your org mapping as needed.
{% endhint %}

{% embed url="https://youtu.be/8Cv-j_NADqw?si=eGAWqtSbts2AM0Dc" %}

The general steps to map each organization are as follows.

1. Navigate to **Configuration > Integrations** in the Rewst platform.
2. Select the integration that you want to map from your collection of already set up integrations, or complete the integration configuration setup process for your new desired integration.
3. Scroll down the page to the **Organization Mapping** submenu. Here you'll see your **Organizations** listed in a table.

<div data-full-width="true"><figure><img src="../../.gitbook/assets/Screenshot 2025-02-21 at 10.48.43 AM.png" alt="An image of the organizational mapping sub menu inside an integration. It contains four columns across a page with customer information."><figcaption><p>An example of the Organization Mapping sub menu, in an installed integration's configuration page</p></figcaption></figure></div>

4. Click **Refresh Options** to pull customer accounts from your integration. This will refresh the potential mapping options for both organizations and companies in the partner tool.
   1. If the blank text box turns into a dropdown field, the sync was successful.
   2. If accounts are missing:&#x20;
      1. Check if the customer account exists in your integrated tool.
      2. Adjust any applied filters that might be excluding accounts.
5. Click **Suggest Values**. Rewst will try to match organization names automatically. This generates mappings between Rewst organizations and corresponding entities in the partner app.&#x20;
   1. If Rewst can't find a matching option, the drop-down field will remain blank. You should then click the drop-down to expand the list, scroll through the list, and manually choose the org associated with the desired org in Rewst.
   2. If it does find an option, the corresponding name will appear in the drop-down field automatically.
6. Review the suggestions to ensure that organizations in Rewst and customer names in the integrated tool are aligned. If a match is missing, manually select the correct organization from the dropdown menu.
7. Double-check all mappings, especially if you have multiple pages of organizations. By default, only the first 10 organizations will be listed.
8. Click **Save Mappings** to finalize the connections.&#x20;
9. Once you map an integration, Rewst will create an org variable for that organization. You can view the related org variables and their corresponding IDs by navigating to the total org variable list in **Configuration > Organization Variables**. Note that this will not be the case for any Microsoft integration in the Microsoft Cloud Bundle.

{% hint style="info" %}
If you uninstall an integration and reinstall it again, you won't need to redo your org mapping. Rewst will have this information stored and will repopulate it into the new installation.
{% endhint %}

### Integration overrides

Integration overrides allow you to specify which integration configurations should be used. When a workflow is triggered by and running within the context of a [child organization](organization-variables.md#what-is-an-organization), by default they only have access to their own integrations and configurations. To give the workflow access to integrations and credentials owned by the parent organization, that default behavior must be explicitly overridden.  Integration overrides are set in the trigger menu of the workflow in question, not from the actual integration configuration page in Rewst. Learn more about integration overrides in our [triggers](../automations/intro-to-triggers/) documentation.

## Request an integration

We’re constantly adding new integrations to Rewst. Vote for which upcoming integrations should take priority by creating a post with your thoughts or upvoting other existing suggestion posts [in our Canny.](https://rewst.canny.io/integrations)
