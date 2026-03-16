# Billing Count Report Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the Billing Count Report Crate do?

Our Billing Count Report Crate is designed to streamline and enhance the process of compiling billing counts from various integrations. This tool iterates through multiple integrations, collects relevant billing data, and generates a comprehensive report, ensuring accuracy, efficiency, and consistency.&#x20;

### How the Crate works

* This Crate supports a wide range of integrations, including Datto RMM, ConnectWise Automate, NinjaOne, Microsoft 365 licensing, Huntress, SentinelOne, Pax8, ITG, Auvik, Proofpoint, Cork, Immybot, Duo, and Dropsuite.
* It retrieves billing data from each integration, eliminating the need for manual data collection, and aggregates data from different sources to provide a holistic view of the billing counts.
* Users can schedule the report generation at regular intervals: daily, weekly, or monthly.
* Choose one of three delivery mechanisms: attachment to a PSA ticket, attachment on an email, retrieve data running it as a subworkflow
* Data is compiled into CSV format with all possible products, leaving blanks where applicable items are not configured or available

### Workflow breakdown

#### Phase 1: Initialization and validation

1. The workflow begins at the **BEGIN** task using the noop action, which initializes the output structure with empty data, a success flag set to true, and an empty automation log array.
2. The **Check Running Org** task executes the **\[REWST - TASK] General: Check Running Org** subworkflow to verify that the workflow is running in the correct organization context.
3. If the organization check passes, the **Get Integration Ids** task runs the **\[PROD TASK] Rewst: Get All Integration Ids** subworkflow to retrieve all integration identifiers for every managed organization, including mappings for PSA, RMM, security, and cloud licensing platforms.

#### Phase 2: Data collection - RMM and device counts

1. The **Is Datto RMM Installed** task uses the **noop** action to check whether the Datto RMM integration is installed for the organization.
2. If Datto RMM is installed, the **Get Datto RMM Counts** task executes the **\[PROD PROCESS] Datto: Get RMM Device Count Loader** subworkflow to retrieve device counts from all Datto RMM sites.
3. The **Is CWA Installed** task uses the **noop** action to check whether ConnectWise Automate is installed.
4. If ConnectWise Automate is installed, the **Get CWA Device Counts** task runs the **\[PROD TASK] CWA: Get Counts** subworkflow to retrieve server and workstation counts from ConnectWise Automate.
5. The **Is Ninja Installed** task uses the **noop** action to check whether NinjaOne RMM is installed.
6. If NinjaOne is installed, the **Get Ninja Device Counts** task executes the **\[PROD TASK] Ninja: Get Device Counts** subworkflow to retrieve workstation, server, and network device counts.
7. The **Is\_CW\_ASIO\_Installed** task uses the **noop** action to check whether ConnectWise ASIO is installed.
8. If ConnectWise ASIO is installed, the **Get\_CW\_ASIO\_Device\_Counts** task runs the **\[PROD TASK] CW ASIO: Get Counts** subworkflow to retrieve device counts from ConnectWise ASIO.
9. The **Is Graph Installed** task uses the **noop** action to check whether Microsoft Graph is installed.
10. If Microsoft Graph is installed, the **Get 365 License Counts** task executes the **\[PROD PROCESS] M365: M365 User License Launcher** subworkflow using a with-items loop to iterate through each organization that has an M365 tenant configured, retrieving license counts for each.

#### Phase 3: Data collection - security integrations

1. The **Is Huntress Installed** task uses the **noop** action to check whether Huntress is installed.
2. If Huntress is installed, the **Get Huntress License Counts** task runs the **\[PROD TASK] Huntress: Get License Counts** subworkflow to retrieve agent counts from Huntress.
3. The **Is SentinelOne Installed** task uses the **noop** action to check whether SentinelOne is installed.
4. If SentinelOne is installed, the **Get Sentinel One Counts** task executes the **\[REWST - TASK] SentinelOne: Get License Counts** subworkflow to retrieve active license counts and SKU information.
5. The **Is Duo Installed** task uses the **noop** action to check whether Duo is installed.
6. If Duo is installed, the **Get Duo User Counts** task runs the **\[PROD TASK] Duo: Get User Counts** subworkflow to retrieve user counts from all Duo accounts.
7. The **Is Pax8 Installed** task uses the **noop** action to check whether Pax8 is installed.
8. If Pax8 is installed, the **Get Pax8 License Counts** task executes the **\[PROD - TASK] Pax8: Get License Counts** subworkflow to retrieve subscription quantities and product information.
9. The **Is ItGlue Installed** task uses the **noop** action to check whether IT Glue is installed.
10. If IT Glue is installed, the **Get MyGlue License Counts** task runs the **\[PROD TASK] MyGlue: Get License Counts** subworkflow to retrieve MyGlue user counts per organization.
11. The **Is Auvik Installed** task uses the **noop** action to check whether Auvik is installed.
12. If Auvik is installed, the **Get Auvik Counts** task executes the **\[PROD TASK] Auvik: Get Counts** subworkflow to retrieve device counts from Auvik tenants.
13. The **Is Proofpoint Installed** task uses the **noop** action to check whether Proofpoint is installed.
14. If Proofpoint is installed, the **Get Proofpoint Counts** task runs the **\[PROD TASK] Proofpoint: Get Counts** subworkflow to retrieve user license counts from Proofpoint organizations.
15. The **Is Immybot Installed** task uses the **noop** action to check whether ImmyBot is installed.
16. If ImmyBot is installed, the **Get ImmyBot Counts** task executes the **\[PROD TASK] Immybot: Get User Count** subworkflow to retrieve device counts grouped by tenant.
17. The **is\_cork\_installed** task uses the **noop** action to check whether Cork is installed.
18. If Cork is installed, the **get\_cork\_counts** task runs the **\[PROD - TASK] Cork: Get Device Counts** subworkflow to retrieve device counts, user counts, and warranty status information.
19. The **is\_dropsuite\_installed** task uses the **noop** action to check whether Dropsuite is installed.
20. If Dropsuite is installed, the **get\_dropsuite\_counts** task executes the **\[REWST - TASK] Dropsuite: Get Counts** subworkflow to retrieve seat counts including active seats, used seats, and paid shared mailboxes.

#### Phase 4: Data collection - distributor integrations

1. The **is\_sherweb\_installed** task uses the **noop** action to check whether Sherweb is installed.
2. If Sherweb is installed, the **get\_sherweb\_count** task runs the **\[PROD TASK] Sherweb: Get License Counts – Rewst** subworkflow to retrieve subscription counts from Sherweb customers.
3. The **is\_synnex\_installed** task uses the **noop** action to check whether TD Synnex Stellr is installed.
4. If TD Synnex Stellr is installed, the **td\_synnex\_stellr\_get\_count** task executes the **\[PROD TASK] TD Synnex Stellr: Get License Counts – Rewst** subworkflow to retrieve license counts from Synnex Stellr.
5. The **is\_streamone\_installed** task uses the **noop** action to check whether TD Synnex StreamOne ION is installed.
6. If StreamOne ION is installed, the **stream\_one\_ion\_get\_license\_counts\_rewst** task runs the **\[PROD TASK] TD Synnex StreamOne ION: Get License Counts – Rewst** subworkflow to retrieve subscription counts.
7. The **is\_synnex\_au\_installed** task uses the **noop** action to check whether Synnex AU is installed.
8. If Synnex AU is installed, the **synnex\_au\_get\_license\_counts** task executes the **\[PROD TASK] Synnex AU: Get License Counts** subworkflow to retrieve license counts from Synnex Australia.

#### Phase 5: Data consolidation

1. The **Begin Consolidation** task uses the **noop** action to start the data consolidation phase, creating the initial integration output structure that maps each company to its collected counts from security integrations including Duo, SentinelOne, IT Glue, Huntress, Auvik, and Proofpoint.
2. If Microsoft Graph is installed, the **Append\_365\_data** task uses the **noop** action to merge Microsoft 365 license counts into the consolidated output by matching company IDs.
3. The **check\_pax\_append** task uses the **noop** action to determine whether Pax8 data should be appended.
4. If Pax8 is installed, the **Append\_pax8\_data** task uses the **noop** action to merge Pax8 subscription quantities into the consolidated output, prefixing each product name with PAX8.
5. The **check\_cork\_append** task uses the **noop** action to determine whether Cork data should be appended.
6. If Cork is installed, the **Append\_cork\_data** task uses the **noop** action to merge Cork device counts, user counts, and warranty status into the consolidated output.
7. The **check\_dropsuite\_appended** task uses the **noop** action to determine whether Dropsuite data should be appended.
8. If Dropsuite is installed, the **Append\_dropsuite\_data** task uses the **noop** action to merge Dropsuite seat information including active seats, organization details, and shared mailbox counts.
9. The **check\_sherweb\_append** task uses the **noop** action to determine whether Sherweb data should be appended.
10. If Sherweb is installed, the **Append\_sherweb\_data** task uses the **noop** action to merge Sherweb subscription counts into the consolidated output, prefixing each product with Sherweb.
11. The **check\_synnex\_append** task uses the **noop** action to determine whether TD Synnex Stellr data should be appended.
12. If Synnex is installed, the **Append\_synnex\_data** task uses the **noop** action to merge Synnex Stellr license counts into the consolidated output.
13. The **append\_streamone\_data** task uses the **noop** action to check whether StreamOne data should be appended and merges StreamOne ION subscription counts if the integration is installed.
14. If StreamOne is installed, the **Append\_streamone\_data** task uses the **noop** action to merge StreamOne subscription data with product names and unit types.
15. The **append\_synnex\_au\_data** task uses the **noop** action to check whether Synnex AU data should be appended.
16. If Synnex AU is installed, the **Append\_Synnex\_AU\_data** task uses the **noop** action to merge Synnex Australia license counts with product and unit information.
17. The **check\_rmm\_append** task uses the **noop** action to determine whether any RMM data should be appended by checking if ImmyBot, Datto RMM, ConnectWise Automate, NinjaOne, or ConnectWise ASIO is installed.
18. If any RMM integration is installed, the **Append\_rmm\_data** task uses the **noop** action to merge all RMM device counts including workstation counts, server counts, and network device counts into the consolidated output.

#### Phase 6: Output generation

1. The **Remove Integration Ids** task uses the **noop** action to clean up the final output by removing the internal integration ID mappings that were used for data matching, leaving only the company names and their associated counts.
2. The **create\_csv** task uses the **Set Variable** action to convert the final consolidated output into CSV format, dynamically determining all column headers from the collected data and ensuring the Company column appears first.

#### Phase 7: Report delivery

1. The **choose delivery method** task uses the **noop** action to evaluate the billing report delivery mechanism input parameter and route to the appropriate delivery method.
2. If the delivery mechanism is set to PSA, the **workflows\_dev\_process\_psa\_create\_ticket** task executes the **\[REWST - PROCESS] PSA: Create Ticket** subworkflow to create a new ticket titled Billing Reconciliation in the configured PSA system.
3. After the PSA ticket is created, the **workflows\_upload\_csv\_to\_ticket** task runs the **\[REWST - TASK] Upload Attachment To Ticket** subworkflow to attach the generated CSV file to the ticket.
4. If the delivery mechanism is set to email and recipients are configured, the **workflows\_function\_send\_email\_with\_attachment** task executes the **\[PROD - TASK] Rewst: Send Email with Attachment** subworkflow to send the billing report as an email attachment to the specified recipients.
5. If no delivery method is configured, the **no\_delivery\_method\_set** task uses the **noop** action to handle the case where the report is generated but not delivered.

#### Phase 8: Completion

1. The **build automation log** task uses the **noop** action to compile all log entries from throughout the workflow execution into a consolidated automation log structure that includes status codes, success indicators, warnings, and errors.
2. The **END** task uses the **noop** action to finalize the workflow output by updating the output structure with the generated CSV data and completing the workflow execution.

## Crate prerequisites

Your [RMM integration](../../integrations/top-5-integration-types-get-started-with-integrations-in-rewst.md#rmm-integrations) with Rewst must be set up before unpacking this Crate.

If choosing to deliver the report via PSA ticket, you'll also need to set up your [PSA integration](../../integrations/top-5-integration-types-get-started-with-integrations-in-rewst.md#psa-integrations) before unpacking this Crate.

If choosing to use any auxiliary tools with this Crate, such as security or licensing tools, they must first be successfully integrated with Rewst before unpacking.

Below is the total list of tools that work with our Billing Count Report Crate.

<table data-header-hidden><thead><tr><th valign="top">Integration</th><th valign="top">Usage</th></tr></thead><tbody><tr><td valign="top"><a href="../../integrations/integration-guides/connectwise-integration-setup.md">ConnectWise PSA</a></td><td valign="top">Create tickets, upload attachments</td></tr><tr><td valign="top"><a href="../../automations/kits/datto-psa-integration-kit.md">Datto PSA</a></td><td valign="top">Create tickets, upload attachments</td></tr><tr><td valign="top"><a href="../../automations/kits/halo-psa-integration-kit.md">Halo PSA</a></td><td valign="top">Create tickets, upload attachments</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/kaseya-bms-integration-setup.md">Kaseya BMS</a></td><td valign="top">Create tickets</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/servicenow-integration-setup.md">ServiceNow</a></td><td valign="top">Create tickets</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/freshdesk-integration-setup.md">Freshdesk</a></td><td valign="top">Create tickets</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/superops-integration.md">SuperOps</a></td><td valign="top">Create tickets</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/ninjaone-integration-setup.md">NinjaOne</a></td><td valign="top">Create tickets - PSA functionality<br>Get device counts - servers, workstations, network devices</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/connectwise-automate-integration-setup.md">ConnectWise Automate</a></td><td valign="top">Get device counts - servers, workstations</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/connectwise-asio-integration.md">ConnectWise ASIO</a></td><td valign="top">Get device counts - servers, workstations</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/datto-rmm-integration-setup.md">Datto RMM</a></td><td valign="top">Get device counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/immybot-integration-setup.md">ImmyBot</a></td><td valign="top">Get device and user counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/huntress-integration-setup.md">Huntress</a></td><td valign="top">Get license counts - agent counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/sentinelone-integration-setup.md">SentinelOne</a></td><td valign="top">Get license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/duo-integration-setup.md">Duo</a></td><td valign="top">Get user counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/proofpoint-integration-setup.md">Proofpoint</a></td><td valign="top">Get user and license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/cork-integration.md">Cork</a></td><td valign="top">Get device counts, user counts, warranty status</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/microsoft-cloud-integration-bundle/microsoft-graph-subscriptions.md">Microsoft Graph</a></td><td valign="top">Get M365 license counts, send emails</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/pax8-integration-setup.md">Pax8</a></td><td valign="top">Get license counts - subscriptions</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/sherweb-integration-setup.md">Sherweb</a></td><td valign="top">Get license counts - subscriptions</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/synnex-integration-setup.md">TD Synnex Stellr</a></td><td valign="top">Get license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/td-synnex-streamone-ion-integration.md">TD Synnex StreamOne ION</a></td><td valign="top">Get license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/synnex-australia-integration-setup.md">Synnex AU</a></td><td valign="top">Get license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/it-glue-integration-setup.md">IT Glue</a></td><td valign="top">Get MyGlue license counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/auvik-integration-setup.md">Auvik</a></td><td valign="top">Get device counts</td></tr><tr><td valign="top"><a href="../../integrations/integration-guides/dropsuite-integration.md">Dropsuite</a></td><td valign="top">Get seat counts - active seats, used seats, shared mailboxes</td></tr></tbody></table>

## Unpack the Billing Count Report Crate

1. Navigate to **Marketplace > Crates** in the left side menu of the Rewst platform.
2.  Search for the `Billing Count Report` Crate.

    \
    ![](<../../../.gitbook/assets/image (126).png>)
3. Click on the Crate tile to begin unpacking.
4. Click **Unpack Crate**.
5. Scroll to the bottom of the page. Choose how you want the billing report delivered by selecting your option from the **Billing Report Delivery Mechanism** drop-down. Fill out the other required information fields, depending on your delivery method.

<figure><img src="../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

6. Click **Continue**.
7. Click **Unpack**.

### Test the Crate

To test this Crate, you'll need to adjust the cron trigger's schedule to a few minutes in the future, then adjust it back to your regular schedule after the test. Alternatively, you could wait until the regularly scheduled run occurs and check your result, which would not require you to update the cron trigger schedule.<br>

1. Navigate to **Automations > Workflows**.
2. Search for `billing count` .
3. Click on the workflow to open it in the workflow builder.
4. Adjust the cron trigger's schedule to five minutes from your current time. The workflow will trigger then on its own. A ticket or email will be generated if the workflow is successful.

<figure><img src="../../../.gitbook/assets/image (49) (2).png" alt=""><figcaption></figcaption></figure>

## Troubleshoot the Billing Count Report Crate

This workflow is meant to run from your parent organization only. If you’re seeing workflow failures for child organizations, disable the trigger for child organizations in the configuration page for the Crate.

<figure><img src="../../../.gitbook/assets/image (48) (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}

