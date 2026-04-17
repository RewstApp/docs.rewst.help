# Alert on Unused M365 Licenses Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the Alert on Unused M365 Licenses Crate do?

This Crate checks daily for unused M365 licenses that can be returned to Pax8, then creates a ticket in your PSA with the information. The ticket will include hyperlinks to update the purchased quantity to match the used quantity and remediate unused licenses. This Crate does facilitate the removal of extra licenses, but only when the end-user clicks the URL generated in the PSA ticket, which is then executed via the webhook trigger in the Crate's workflow. It doesn't automatically remove licenses.

{% hint style="info" %}
Note that the existence of an SKU in Microsoft doesn’t mean that it was purchased through Pax8. Customers can still buy directly from Microsoft. If a SKU doesn’t have a matching Pax8 subscription, it won’t be alerted on because the automation wouldn’t be able to modify or validate quantities for something that doesn’t exist in Pax8.
{% endhint %}

### How the Crate works

The workflow unpacked with this Crate runs on a cron trigger, and will generate the ticket at the same time each day. It also contains a webhook trigger, which acts as the external API endpoint that kicks off Pax8 license quantity reconciliation — either for a specific SKU or as a full scan — across your managed organizations.

Tickets or alerts are generated only when all of the following is true:

* The subscription is oversubscribed
* The commit term is monthly
* The subscription is not included in the ignored subscriptions list

No action is taken when any of the following is true:

* The subscription has a yearly commit, even if it's oversubscribed
* The subscription is in the ignored subscriptions list
* There's no corresponding Pax8 subscription for that SKU

### Workflow breakdown

1. The workflow begins with the **start** task which initializes the process by setting the retry count to zero and preparing the workflow for execution.
2. The **check\_for\_exclusions** task examines whether an organization variable exists that contains a list of organizations excluded from the Pax8 license removal process.
3. If exclusions are found, the **exclusions\_var\_found** task checks if the current organization ID is in the exclusion list, and if so, routes to the **org\_excluded** task to terminate processing.
4. If the organization is not excluded, the **continue\_workflow** task allows the process to proceed to the main workflow logic.
5. The **set\_ignored\_subs** task creates a list of Microsoft 365 SKUs that should be ignored during the license removal process, including free trials, consumption-based apps, and products with extremely high license counts.
6. If the Pax8 company ID is not configured for the organization, the **pax8\_not\_configured\_for\_org** task determines whether to create an alert ticket for unmapped organizations.
7. The **check\_operation** task evaluates input parameters to determine if this is a single subscription update operation or a bulk listing operation.
8. For listing operations, the **delay\_based\_on\_org\_name** task introduces a delay based on the alphabetical order of the organization name to prevent API overload.
9. The **list\_graph\_subscriptions** task retrieves all Microsoft 365 subscriptions from Microsoft Graph API and identifies undersubscribed SKUs where consumed units are less than enabled units.
10. The **check\_undersubscribed\_skus** task determines if any undersubscribed SKUs were found and routes accordingly.
11. If undersubscribed SKUs exist, the **look\_up\_products** task loads lookup tables to map Microsoft 365 SKU part numbers to Pax8 product names.
12. The **look\_up\_skus** task processes the lookup information to prepare for Pax8 subscription matching.
13. The **pax\_8\_list\_subscriptions** task retrieves all active Pax8 subscriptions for the organization.
14. The **workflows\_aw\_get\_pax\_8\_order** task iterates through each Pax8 subscription to get detailed product information with a concurrency of 2.
15. The **find\_eligible\_subs** task matches Microsoft 365 undersubscribed SKUs with eligible Pax8 subscriptions, excluding annual commitments and identifying over-purchased subscriptions.
16. The **make\_ticket\_if\_needed** task determines if any over-purchased subscriptions were found and creates a PSA ticket if necessary.
17. If a ticket is created, the **create\_psa\_service\_ticket** task generates a service ticket with details about the underprovisioned licenses.
18. The **apply\_template** task formats the ticket note content based on the PSA system type, using different templates for Halo PSA/Freshdesk versus other systems.
19. The **update\_ticket** task adds the formatted note to the created ticket with details about the license discrepancies.
20. For single subscription updates, the **get\_subscription** task retrieves the specific subscription details and calculates the quantity delta.
21. If ConnectWise Manage is installed, the **connect\_wise\_manage\_get\_service\_ticket** task retrieves the existing ticket information.
22. The **adjust\_pax8\_license\_counts** task performs the actual license quantity adjustment in Pax8, reducing the subscription by the calculated delta.
23. If the adjustment succeeds, the workflow updates the ticket with a success message; if it fails, it updates the ticket with error details.
24. The **rewst\_list\_triggers** task retrieves webhook trigger information if the organization variable for the trigger ID is not set.
25. The **rewst\_bulk\_upsert\_organization\_variables** task creates or updates the webhook trigger ID organization variable for future use.
26. The **core\_delay\_workflow\_for\_period** task introduces a one-minute delay and manages retry logic if the maximum retry count has not been reached.
27. If no undersubscribed SKUs are found, the **no\_unaligned\_subs\_found** task terminates the workflow without taking any action.

The workflow will do the main license adjustment in Pax8 without any required user action, and has three possible outcomes after attempting license removal.

1. **Success** - updates the PSA ticket with success message
2. **Failure** where the condition is succeeded but part of the execution did not work - updates ticket with failure details and error messages
3. **Complete failure** - updates ticket with failure details and error messages

#### What the Crate excludes

The workflow unpacked with this Crate won't process any licenses that have 10,000 or more purchased units. This is an intentional safety mechanism to prevent:

* Processing massive enterprise licenses that might be intentionally over-provisioned
* Accidental reduction of licenses for organizations with very large license pools

Licenses under 10,000 units will be processed normally and included in the PSA ticket for potential reduction. Licenses with more than 10,000 units will be automatically excluded from processing, but no notification will be sent when these licenses are excluded.&#x20;

The workflow will also exclude free, trial, and consumption-based licenses, as well as licenses with Year in the commitment term.

{% hint style="info" %}
Optionally, you can set the organization variable `pax8_license_removal_exclusions` to exclude specific organizations.
{% endhint %}

## Crate prerequisites

Before unpacking this Crate:

The[ Pax 8 integration](../../integrations/integration-guides/pax8-integration-setup.md) must first successfully be set up in Rewst .

The [Microsoft Cloud Integration Bundle](../../integrations/integration-guides/microsoft-cloud-integration-bundle/) must be set up to enable the Microsoft Graph integration with Rewst.

Your[ PSA must be integrated](../../integrations/top-5-integration-types-get-started-with-integrations-in-rewst.md#psa-integrations) with Rewst.&#x20;

## Unpack the Alert on Unused M365 Licenses Crate

1. Navigate to **Marketplace** **> Crates** in the left side menu of the Rewst Platform.
2. Search for `Alert on Unused M365 Licenses`.\
   \
   ![](<../../../.gitbook/assets/image (133).png>)
3. Click **Unpack Crate**.
4. Click **Continue.**
5. Enter your **Time Saved**.
6. Expand the **Cron Job** accordion menu and ensure that **Enabled** is toggled on.&#x20;
7. Click **Unpack**.

## Test the Crate

{% hint style="info" %}
The workflow must first be run as the top level parent organization. Then, the workflow can be used by  child organizations.
{% endhint %}

The Crate runs on a cron trigger, and will execute the workflow to generate the ticket at the same time each day. You can adjust the chosen time for execution in the workflow itself. To test the Crate, adjust the trigger to five minutes in the future. Then, check your PSA to see if tickets were created. If your execution is successful, go back into the workflow and reset the cron trigger's timing to your normal desired schedule.

1. Navigate to **Automations > Workflows** in the left side menu of your Rewst platform.
2. Search for `Pax8 Extra License Removal.`
3. Click on the workflow to view it in the workflow builder.
4.  Click ![](<../../../.gitbook/assets/image (205).png>) to open the edit trigger menu.\
    &#x20;

    <figure><img src="https://docs.rewst.help/~gitbook/image?url=https%3A%2F%2F1835401289-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FAQQ1EHVcEsGKBPVHmiav%252Fuploads%252FwnXIbYjmeXtTETWFBKkI%252FScreenshot%25202025-06-25%2520at%25205.53.42%25E2%2580%25AFPM.png%3Falt%3Dmedia%26token%3D53680b5e-a0a9-4260-8d31-4802c66355e8&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=e56327e1&#x26;sv=2" alt=""><figcaption></figcaption></figure>
5. Update the timing of the cron trigger as desired in the fields under **Trigger Parameters**. Note that when entering the time into the **Cron Schedule** field, the correct format is minutes followed by hour. For example. 18 3, not 3 18.
6. Click **Submit**.

&#x20;If tickets are not created, check the workflow's execution results.

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
