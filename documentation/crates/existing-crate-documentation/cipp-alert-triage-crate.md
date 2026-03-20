# CIPP Alert Triage Crate

## What does the CIPP Alert Triage Crate do?

This Crate automatically processes alerts from CIPP (CyberDrain Improved Partner Portal) and routes them to the appropriate PSA ticketing boards. Alerts are filtered based on configurable exclusion lists for tenants and messages, and tickets are automatically created or updated in your PSA system. A configuration form unpacked with the Crate allows technicians to set up board mappings and exclusion rules per organization without modifying the workflow directly.

This Crate doesn't send email notifications to users or administrators or modify any configuration within CIPP itself. It won't automatically resolve or close tickets when alerts are cleared, manage CIPP API authentication or webhook security, or send email notifications to users or administrators.

### How the Crate works

* Automatically receives and processes CIPP alerts, kicked off via webhook trigger
* Filter out specific tenants or message types from creating tickets with configurable exclusion lists
* Route different alert types alerts to separate PSA boards: changes, updates, standards, scheduled tasks
* Set up organization variables through a user-friendly form
* Handles multiple alerts simultaneously for faster throughput

### PSA note format

| Format     | Used for                                                               |
| ---------- | ---------------------------------------------------------------------- |
| HTML       | Halo PSA and Freshdesk — includes formatted headers and styled content |
| Plain text | All other PSAs — clean, readable text formatting                       |

### Workflow breakdown

{% hint style="info" %}
The workflow can be started by two triggers:

* **CIPP Alert Triage - Form - Create or Update ORG Variables** - A form trigger for configuring organization variables
* **CIPP Alert Triage - Webhook - Notifications** - A webhook trigger that receives CIPP alert notifications
{% endhint %}

1. The workflow begins at the **check\_trigger\_source** task, which uses the **noop** action to determine how the workflow was triggered by checking if the form\_trigger context variable is set to true.
2. If the workflow was triggered by the form, the flow transitions to the **get\_organization\_variable** task, which uses the **Get Organization Variable** action to look up an organization by searching for a `cipp_tenant_id` variable that matches the provided tenant name.
3. If the **get\_organization\_variable** task finds a matching organization, the organization\_id is published to the context and the flow continues to the **run\_org\_variables\_workflow** task. If no matching organization is found, the parent organization ID is used instead and the flow still proceeds to the **run\_org\_variables\_workflow** task. If the task fails, the flow transitions to the **FAILURE** task.
4. The **run\_org\_variables\_workflow** task executes the **\[REWST - UTILITY] CIPP: Alert Triage - Create or Update ORG Variables** subworkflow action, passing in the organization ID and various board configuration parameters for CIPP alerts, changes, general notifications, updates, scheduled tasks, and standards.
5. If the workflow was triggered by a webhook or other non-form trigger, the flow transitions from **check\_trigger\_source** to the **filter\_and\_validate\_alerts** task, which uses the **noop** action to filter out alerts from excluded tenants and messages based on organization variables, normalize the alert data format, and validate that valid tenants exist in the payload.
6. If the **filter\_and\_validate\_alerts** task determines there are valid tenants to process, the filtered and normalized alert body is published to the context and the flow transitions to the **process\_alerts** task. If no valid tenants remain after filtering, the flow transitions to the **no\_valid\_tenants\_exit** task.
7. The **process\_alerts** task uses the **\[REWST - TASK] CIPP: Process Single Alert** subworkflow action with a with-items configuration to iterate over each alert in the body with a concurrency of 2. Each alert is processed individually to create or update PSA tickets.
8. The **no\_valid\_tenants\_exit** task uses the **noop** action to handle the case where all alerts were filtered out, publishing an empty output array before transitioning to the **END** task.
9. The **FAILURE** task uses the **noop** action as a centralized failure handler that collects errors from any failed upstream tasks before transitioning to the **END** task.
10. The **END** task uses the **noop** action to aggregate all results and prepare the final output. It compiles an automation\_log by collecting all context variables that start with log\_ and calculating an overall status code, success indicator, warnings, and errors.
11. The workflow completes by outputting the processed results in the output variable and the compiled automation\_log containing status codes, success indicators, any warnings, errors, and detailed log entries from each task.

## Crate prerequisites

* Your[ PSA must be integrated](../../integrations/top-5-integration-types-get-started-with-integrations-in-rewst.md#psa-integrations) with Rewst.&#x20;
* Your [CIPP integration](../../integrations/integration-guides/cipp-cyberdrain-improved-partner-portal-integration.md) must successfully be set up in Rewst.

## Unpack the CIPP Alert Triage Crate

1. Navigate to **Crates > Crate Marketplace** in the left side menu of the Rewst platform.
2. Search for `CIPP Alert Triage`.
3. Click on the Crate tile to begin unpacking.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-03-16 at 3.34.37 PM.png>)
4. Click **Continue**.
5. Click **Unpack**.

### Use the form

This form should be used to create or update organization variables for the Crate.

1. Navigate to **Automations > Assets > Forms** in the left side menu of your Rewst platform.
2. Search for `[REWST] CIPP: Alert Triage - Create or Update ORG Variables`.
3. Click **⋮ > Usages > View Direct URLs.**
4. Click on the link for the organization which contains the user you wish to manage. This will launch the form in a new tab.
5. Fill out the form as follows:
   1. If running for parent organization:
      1. Select the tenant names to exclude from alerts from the **Do Not Alert Tenants** drop-down selector.
      2. Enter JSON array of message strings to exclude from alerts into the **Do Not Alert Messages** field - for example: `["Message1", "Message2"]`
   2. If running for child organization:
      1. Choose the CIPP Tenant associated with the child organization to configure from the **Select CIPP Tenant** drop-down selector.
   3. All fields under **PSA Board IDs** are optional. If any one of them is not provided, the default board for that alert type will be the value set for the organization's `psa_default_board_id`.&#x20;
      1. **CIPP Updates Board ID** - PSA board ID for alerts from the CIPP "Updates" API
      2. **CIPP Standards Board ID** - PSA board ID for alerts from the CIPP "Standards" API
      3. **CIPP Alerts Board ID** - PSA board ID for alerts from the CIPP "Alerts" API
      4. **CIPP Changes Board ID** - PSA board ID for alerts from the CIPP "AddGroup" or "EditUser" API
      5. **CIPP Scheduled Task Board ID** - PSA board ID for alerts from the CIPP "ScheduledTask" API
      6. **CIPP General Board ID** - PSA board ID for any alerts not handled in previous fields
6. Click **Submit**.

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-16 at 4.16.43 PM.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-16 at 4.16.34 PM.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

## Organization variables associated with this Crate

{% hint style="info" %}
For more on organization variables and how to use them, see our org variable documentation [here](https://docs.rewst.help/documentation/configuration/organization-variables).

Organization variables not found in our standard organization variables documentation, such as the ones listed below. are typically system variables that are handled by integration mappings.

If you haven't done so already, we recommended that you run the [Configure Organization Variables Crate](https://docs.rewst.help/documentation/crates/existing-crate-documentation/configure-organization-variables), which will help you set org variables that are relevant to you and your customer's environments.
{% endhint %}

| Variable name                | Purpose                                                                                                                     |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `cipp_tenant_id`             | Created when the CIPP integration is configured. Maps CIPP tenant names to Rewst organization IDs for proper ticket routing |
| `cipp_do_not_alert_tenants`  | JSON array of tenant names to exclude from alerting                                                                         |
| `cipp_do_not_alert_messages` | JSON array of message strings to exclude from alerting                                                                      |
| `cipp_alerts_board_id`       | Optional PSA board ID for alert-type tickets                                                                                |
| `cipp_changes_board_id`      | Optional PSA board ID for change-type tickets - user edits, group additions                                                 |
| `cipp_general_board_id`      | Optional PSA board ID for general/uncategorized tickets                                                                     |
| `cipp_updates_board_id`      | Optional PSA board ID for update notification tickets                                                                       |
| `cipp_scheduled_board_id`    | Optional PSA board ID for scheduled task tickets                                                                            |
| `cipp_standards_board_id`    | Optional PSA board ID for standards compliance tickets                                                                      |

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
