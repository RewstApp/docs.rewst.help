# REWST CA Policy Assistant Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the REWST CA Policy Assistant Crate do?

This Crate contains a form that retrieves parent tenant sign-in error logs from the last 14 days and emails a list of all enabled Conditional Access policies, with a link to each for easy navigation to the policy in Microsoft Entra. Policies are omitted if the selected user is excluded in the parent tenant, while child-tenant policies that exclude the tenant externally are still shown and highlighted. If no integration email is provided, all enabled policies are listed. Administrators can choose which actions to perform for specific organizations and users, and which reports to generate, including:

* Forcing password changes
* Invalidating user sessions
* Blocking sign-ins
* Generating various reports - sign-in activity, mailflow, MFA methods, etc.

This Crate does not list disabled Conditional Access policies, show parent-tenant policies where the selected user is excluded, or retrieve sign-in logs older than two weeks. It doesn't modify, enable or disable, or create Conditional Access policies—this Crate is for retrieval, listing, and highlighting only. It does, however, provide a link to each CA Policy in Entra.&#x20;

## Crate prerequisites

There are two ways to use this Crate: with the [Microsoft Cloud Integration Bundle](../../integrations/integration-guides/microsoft-cloud-integration-bundle/), and without the Bundle.&#x20;

With the Bundle, you'll select the proper option on the form, and Rewst will take care of the rest.

Without the Bundle, you'll need to follow additional steps given in the form to set up app registration with the specific needed permissions.

## Unpack the REWST CA Policy Assistant Crate

1. Navigate to **Marketplace > Crates** in the left side menu of the Rewst platform.
2. Search for `REWST CA Policy Assistant`.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-02-06 at 4.27.32 PM.png>)<br>
3. Click on the Crate tile to begin unpacking.
4. Click **Continue**.
5. Note that you have the option under each of the accordion menus to activate the Crate for all future organizations in addition to the current one.  You may also set activation to certain [tags](../../settings/tags-in-rewst.md). Ensure that **Enabled** is toggled on for each of the three triggers: **Webhook**, **Webhook**, and **Form Submission**.
6. Click **Unpack**.

## Use the Crate

The Crate runs off of form submission.&#x20;

1. Navigate to **Automations > Assets > Forms** in the left side menu of your Rewst platform.
2. Search for `[REWST] Rewst CA Policy Assistant`.
3. Click **⋮ > Usages > View Direct URLs**.
4. Click on the link for the organization which contains your relevant user and computer. This will launch the form in a new tab.
5. Select an answer to **Is the Microsoft Cloud Bundle Installed?**:
   1. Choose **Yes** if using the form with the bundle integrated in Rewst
   2. Choose **No** if using the form without bundle integration - additional fields will appear on the form with this selection
6. For the **Integration Email used to Authenticate the Microsoft Cloud Bundle** field:
   1. Enter the email address you used to authenticate the Bundle to generate a list of all the CA policies that are applied to that specific user.
   2. Leave the field blank to generate a list of all CA Polices which are not associated with that user.
7. Enter the **User Email Address** where you would like the form to send the resulting data.
8. If using the form without the Bundle:
   1. Check the **Click to View Steps to get the Application's Secret ID and Secret Value** box.
   2. Follow the steps that appear on screen to **Create and App Registration**, **Configure API Permissions**, and **Create a Client Secret**. Enter the **Tenant ID**, **Secret ID**, and **Secret Value** into the relevant fields.
9. Click **Submit**.
10. Check your indicated email's inbox for the list.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-02-06 at 4.15.39 PM (1).png" alt="" width="563"><figcaption><p>The standard form before selections are made</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2026-02-06 at 4.43.20 PM.png" alt="" width="479"><figcaption><p>The additional setup fields for use when there is no Bundle integration with Rewst</p></figcaption></figure>

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
