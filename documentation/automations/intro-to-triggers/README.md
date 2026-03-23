# Triggers

## What is a trigger?

_Triggers_ initiate [workflows](https://docs.rewst.help/documentation/workflows) in Rewst. Every workflow must have a trigger to define when and how it starts. Essentially, triggers put the automate in automation. Choosing the right trigger ensures that your workflows execute at the right time, with the right data, to drive efficiency and consistency in your operations.

A trigger is also used on any [form](https://docs.rewst.help/documentation/forms) input that requires a workflow. If a form uses the **Dynamic** button, then you must also create a trigger on the workflow associated with that form.

For more on how to see which triggers appear on a specific workflow, view our documentation [here](../workflows/#view-triggers-for-a-specific-workflow).

## View all triggers

Navigate to **Automations > Triggers** in the left side menu of Rewst to view the total triggers page, which contains a sortable list of all triggers in your Rewst instance, organized by tabs labeled with automation type. This includes triggers from your custom-built workflows and from unpacked Crates. Click on any of the column headers to sort the list by that criteria. Use the **Tags** drop-down selector to filter the list by specific tags.&#x20;

<figure><img src="../../../.gitbook/assets/image (85) (1).png" alt=""><figcaption></figcaption></figure>

Toggle any trigger to enabled or disabled in the **Status** column. Once toggled on, the slider will turn green, and a green checkmark will appear to the right to let you know that the enablement is complete.

{% hint style="warning" %}
We're currently working on a feature limitation that prevents the last activity display for Always Pass and Interval triggers. Instead of listing the last activity, the trigger will show that it has never been activated. For these particular trigger types, confirm the last time the trigger was activated directly in the trigger rather than in the triggers page.
{% endhint %}

## Create a trigger

Add a trigger to a workflow by clicking the **Add Trigger** button in the workflow builder, which will open up a new dialog with a form. \
![](<../../../.gitbook/assets/Screenshot 2025-02-21 at 11.13.39 AM.png>)

Note that you can have multiple triggers per workflow, for example a webhook and a trigger that runs when a ticket gets saved in the PSA.

<figure><img src="../../../.gitbook/assets/add-trigger-form.png" alt=""><figcaption></figcaption></figure>

Update the relevant fields in the setup menu as needed, to set up your trigger. This might include [integration overrides](./) or [tags](../../settings/tags-in-rewst.md).

### Trigger criteria

When you're comfortable with the basics of triggers, learn more about [trigger criteria here](./#trigger-criteria). It's a separate submenu within the trigger menu, and has its own documentation page. The below table outlines the fields in the trigger criteria configuration menu.<br>

<table data-full-width="false"><thead><tr><th width="267">Item</th><th>Description</th></tr></thead><tbody><tr><td><strong>Name</strong></td><td>Whatever you would like to name your trigger, with a descriptive word or phrase for what it does.</td></tr><tr><td><strong>Enabled</strong></td><td>Toggle this on or off.</td></tr><tr><td><strong>Organizations</strong></td><td>Select all the organization that exist within Rewst that may need to use this workflow. If you add a new client, they will have to be added in that workflow trigger.</td></tr><tr><td><strong>Integration Override</strong></td><td>To give the workflow access to integrations and credentials owned by the parent organization, that default behavior must be explicitly overridden. In the above example image, the trigger allows your clients to use your PSA, RRM and licensing integration. See more about integration overrrides in the next section of this document.</td></tr><tr><td><strong>Trigger Type</strong></td><td>There are a number of types to choose from, such as a webhook, form submission, ticket saved, M365 alerts. See <a data-mention href="./#core-triggers">#core-triggers</a> for more information on common trigger types.</td></tr><tr><td><strong>Form</strong></td><td>If your trigger type is a form submission, you would select the form that links to the workflow.</td></tr></tbody></table>

### Integration overrides

Integration overrides allow you to specify which integration configurations should be used. When a workflow is triggered by and running within the context of a child organization, by default they only have access to their own integrations and configurations. To give the workflow access to integrations and credentials owned by the parent organization, that default behavior must be explicitly overridden. In the above example image, the trigger allows your clients to use your PSA, RRM and licensing integration.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-23 at 3.09.52 PM.png" alt="" width="375"><figcaption><p>Choose the integration for which to apply configuration overrides to from the drop-down list.</p></figcaption></figure>

1. Click <img src="../../../.gitbook/assets/Screenshot 2026-03-23 at 3.14.04 PM.png" alt="" data-size="line"> next to integration overrides.
2.  Choose your desired integration from the drop-down selector that appears. This will populate the options for that integration below the selector.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot 2026-03-23 at 3.14.59 PM.png" alt="" width="375"><figcaption></figcaption></figure>

### Activate trigger to run for

This submenu controls which organization**s** a workflow trigger is enabled for. When a triggered, it determines which organizations the workflow can execute in the context of. Each trigger on a workflow has its own Activate Trigger To Run For settings. They aren't shared between multiple triggers on the same workflow.

Find the **Activate Trigger To Run For** section at the very bottom of the configuration screen with the following options:

1. **Selected Organization** toggle
   1. Toggled on by default, this enables the trigger for the organization that owns the workflow, usually the parent organization
   2. Toggle off if you don't want the workflow to run for the owning organization
2. **Organizations** drop-down selector
   1. Manually select specific organizations
   2. Choose individual child organizations that should have this trigger active
3. **All Current and Future Managed Organizations** toggle
   1. Toggle on to automatically enable the trigger for:
      1. All currently existing child organizations
      2. Any new organizations added in the future - automatically included

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 5.27.56 PM.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="warning" %}
* If you don't enable All current and future managed organizations, you must manually add new clients to the trigger when they're onboarded.
* You can't filter organizations by tags in this menu - it's either individual selection, all, or all plus future.
* Even if a trigger is activated for an organization, the workflow will only work if that organization has the required integrations configured and mapped.
* If the workflow uses parent organization integrations like your PSA, you must configure integration overrides on the trigger to give child orgs access to those credentials.
{% endhint %}

## Modify an existing trigger

To modify an existing trigger, click **Edit Trigger**. If there are multiple triggers for the workflow, select the appropriate trigger from the dropdown menu.\
![](<../../../.gitbook/assets/Screenshot 2025-02-21 at 11.20.06 AM.png>)

### How to use a trigger on a form

Once the trigger has been created on a workflow, it can then be used on a form. This must be an options generator workflow. The requirements for this[ can be found here](../workflows/option-generator-workflows.md).

<figure><img src="../../../.gitbook/assets/form-trigger.png" alt=""><figcaption></figcaption></figure>

The above is a snippet from a form where a dropdown field has been selected and the output will be based on the workflow output. When running the form, if the client is added on the trigger and the trigger is set on the form, the workflow will run, and the options will fill into the form field.

## Core triggers

There are seven key triggers to understand when getting started with Rewst. These triggers cover a range of automation scenarios, from scheduled executions to real-time event responses. In Rewst, we denote these from other triggers by calling them _core triggers_. Type `core` into the **Trigger Type** field to isolate most of these trigger types from the total list.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-21 at 11.44.46 AM (1).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Core - Always Pass</summary>

The _always pass trigger_ allows a workflow to start without conditions. It is commonly used in workflows that do not depend on external events or schedules. It's mostly used with the **Test** button in the Workflow Builder Canvas, and options generators for forms that need an override for its fields. You might use this trigger when testing workflows, executing a workflow from another workflow without needing a specific event, or populating dynamic options in a Rewst form.

This trigger is most useful for:

* Manual workflow execution: running a workflow on demand&#x20;
* Subworkflows or completion handlers: workflows triggered by other workflows
* Testing automation: verifying workflow functionality
* Option generators: dynamically populating form fields in Rewst

{% hint style="info" %}
For more information on option generators, refer to [Rewst Foundations](https://learn.rewst.io).
{% endhint %}

</details>

<details>

<summary>Core - App Platform</summary>

This trigger functions the same as Core - Always Pass. By using this trigger type, you create a clear indication that the intended use case is for Rewst's [App Builder](../../app-builder/). Note that it is only useful in locations where you can select a trigger— Data Tables and Charts.&#x20;

</details>

<details>

<summary>Core - Cron Job</summary>

The _cron job trigger_ initiates a workflow on a predefined schedule. This allows you to automate recurring tasks without manual intervention.

Schedules are configured using cron syntax. Consult [crontab guru](https://crontab.guru/) for help configuring this syntax.

For example, you can configure a workflow to run every Monday at 3:00 PM to generate weekly reports or clean up outdated records.

This trigger is most useful for:

* Scheduled maintenance workflows: clearing stale data, running audits
* Recurring notifications: sending reminders, generating reports
* Automated check-ins: verifying system statuses, updating dashboards

</details>

<details>

<summary>Core - Form Submission</summary>

A workflow can be triggered when a user submits a form. Forms collect structured information, ensuring the workflow has the necessary data to proceed.

For example, you can submit an employee onboarding form to trigger a workflow that creates user accounts, assigns permissions, and sends welcome emails.

This trigger is most useful for:

* Request-based workflows: access requests, service requests
* Intake processes: user registrations, issue reporting
* Approval workflows: leave requests, expense approvals

{% hint style="info" %}
For help building a form, refer to [form-best-practices.md](../forms/form-best-practices.md "mention").
{% endhint %}

</details>

<details>

<summary>Core - Time Interval</summary>

Time intervals can be set to trigger a workflow repeatedly over specified periods. This trigger is suitable for workflows that need to repeat on a regular basis.

* **Examples**:
  * Every 5 minutes
  * Every hour
  * Daily
  * Weekly

{% hint style="info" %}
Check out our [using-webhook-triggers.md](use-cases-and-examples/using-webhook-triggers.md "mention") page for a more detailed example.
{% endhint %}

</details>

<details>

<summary>Core - Webhook</summary>

A _webhook_ _trigger_ starts a workflow when external data is received in real time. Webhooks eliminate the need for manual checks, making them efficient for event-driven automation.

The webhook URL serves as a _listening endpoint_. When an external system like a CRM, ticketing system, or another Rewst workflow sends data to the webhook URL, the workflow is triggered immediately. This enables seamless integration between Rewst and external applications without requiring a direct API connection.

For example, a webhook could trigger a workflow whenever a new customer signs up in a CRM, automatically assigning them an account manager and setting up follow-up tasks.

This trigger is most useful for:

* Event-driven automation: responding to new leads, updating records on status changes
* Real-time notifications: escalating high-priority tickets, alerting teams to critical updates
* External system integrations: syncing data between platforms, processing incoming requests

{% hint style="info" %}
For more information on webhook triggers, refer to [using-webhook-triggers.md](use-cases-and-examples/using-webhook-triggers.md "mention").
{% endhint %}

</details>

<details>

<summary>PSA: Ticket record saved</summary>

{% hint style="info" %}
Note that this is the only common trigger type that does not start with Core, as the trigger name will be specific to your brand of PSA. Search for that in the trigger type list instead.
{% endhint %}

This trigger is similar to the webhook trigger but is specific to PSA systems. When a ticket record is saved in an integrated PSA, the workflow starts automatically. This includes both newly created tickets and updates to existing tickets.

For example, if a ticket is updated to **Escalated**, a workflow can trigger an alert to the appropriate team or assign a senior technician.

This trigger is most useful for:

* Automating ticket management: escalating high-priority tickets, auto-assigning technicians
* SLA enforcement: sending reminders for unresolved tickets, auto-responding to specific cases
* Status-based automation: triggering follow-up workflows when a ticket is created or reaches a certain stage

{% hint style="info" %}
For more detailed information on PSA triggers, refer to [customizing-psa-ticket-triggers.md](use-cases-and-examples/customizing-psa-ticket-triggers.md "mention").
{% endhint %}

</details>

## Rewst triggers

_Rewst_ triggers are additional triggers that can be used across all integrations and relate directly to the Rewst platform. Type `Rewst` into the **Trigger Type** field to isolate most of these trigger types from the total list.

<details>

<summary>Rewst - Added User</summary>

The Rewst - Added User trigger starts the workflow when a new user is added in Rewst. The triggering event is when the user signs in for the first time, not when the invite is sent. This trigger is useful for:

* Onboarding automation when new users are added to Rewst
* Sending welcome notifications to new users
* Syncing new user accounts to external systems
* Auditing and logging new user creation events
* Automatically assigning resources or permissions to new users

When this trigger kicks off, it provides the following data in `triggering_user_data`:

| Field          | Type             | Description                             |
| -------------- | ---------------- | --------------------------------------- |
| `id`           | string           | The user's unique identifier            |
| `role`         | string           | The user's role                         |
| `org_id`       | string           | The organization ID the user belongs to |
| `role_ids`     | array of strings | List of role IDs assigned to the user   |
| `username`     | string           | The user's username                     |
| `created_at`   | datetime         | When the user was created               |
| `updated_at`   | datetime         | When the user was last updated          |
| `is_superuser` | boolean          | Whether the user is a superuser         |

</details>

<details>

<summary>Rewst - Added User in Whitelist</summary>

The Rewst - Added User in Whitelist trigger starts the workflow when a user is whitelisted, or invited, in Rewst. This trigger is useful for:

* Sending custom welcome emails when users are invited to Rewst
* Logging and auditing user invitation events
* Triggering approval workflows before invites are finalized
* Syncing invite information to external ticketing or documentation systems
* Tracking who is inviting users and to which organizations

When this trigger kicks off, it provides the following data in `triggering_user_invite_data`:

| Field           | Type             | Description                                      |
| --------------- | ---------------- | ------------------------------------------------ |
| `id`            | string           | The invite's unique identifier                   |
| `email`         | string           | The email address of the invited user            |
| `org_id`        | string           | The organization ID the user is being invited to |
| `role_ids`      | array of strings | List of role IDs assigned to the invited user    |
| `created_at`    | datetime         | When the invite was created                      |
| `updated_at`    | datetime         | When the invite was last updated                 |
| `accepted_at`   | datetime         | When the invite was accepted - if applicable     |
| `is_accepted`   | boolean          | Whether the invite has been accepted             |
| `created_by_id` | string           | The ID of the user who created the invite        |

</details>

<details>

<summary>Rewst - Crate Published Trigger</summary>

The Rewst - Crate Published Trigger kicks off the workflow when a Crate is published in Rewst, allowing you to react programmatically. This trigger is useful for:

* Automating notifications when new crates are published to the Rewst marketplace
* Triggering review or approval workflows when crates are published
* Logging and auditing crate publication events
* Syncing crate publication information to external documentation or communication systems
* Automating post-publication tasks like announcements or version tracking

The Crate will include the following in the workflow execution once triggered.

`CTX.triggering_crate_data.crate_id`                 ID of the Crate `CTX.triggering_crate_data.workflow_id`             ID of the parent workflow in the Crate

</details>

<details>

<summary>Rewst - Deleted User</summary>

The Rewst - Added User trigger starts the workflow when an existing user is removed in Rewst. This trigger is useful for:

* Offboarding automation when users are removed from Rewst
* Auditing and logging user deletion events for compliance
* Syncing user deletions to external systems (e.g., removing access elsewhere)
* Sending notifications when users are removed
* Cleaning up resources or permissions associated with deleted users

When this trigger kicks off, it provides the following data in `triggering_user_data`:

| Field          | Type             | Description                                     |
| -------------- | ---------------- | ----------------------------------------------- |
| `id`           | string           | The deleted user's unique identifier            |
| `role`         | string           | The user's role (at time of deletion)           |
| `org_id`       | string           | The organization ID the user belonged to        |
| `role_ids`     | array of strings | List of role IDs that were assigned to the user |
| `username`     | string           | The user's username                             |
| `created_at`   | datetime         | When the user was originally created            |
| `updated_at`   | datetime         | When the user was last updated                  |
| `is_superuser` | boolean          | Whether the user was a superuser                |

</details>

<details>

<summary>Rewst - Deleted User in Whitelist</summary>

The Rewst - Deleted User in Whitelist trigger starts the workflow when a user is deleted from a whitelist, meaning that their invite is removed in Rewst. This trigger is useful for:

* Auditing and logging when user invites are revoked or removed
* Sending notifications when pending invites are cancelled
* Syncing invite deletions to external ticketing or documentation systems
* Tracking invite lifecycle events for compliance purposes
* Cleaning up any resources or pending actions associated with revoked invites

When this trigger kicks off, it provides the following data in `triggering_user_invite_data`:

| Field           | Type             | Description                                             |
| --------------- | ---------------- | ------------------------------------------------------- |
| `id`            | string           | The invite's unique identifier                          |
| `email`         | string           | The email address of the invited user                   |
| `org_id`        | string           | The organization ID the user was invited to             |
| `role_ids`      | array of strings | List of role IDs that were assigned to the invited user |
| `created_at`    | datetime         | When the invite was originally created                  |
| `updated_at`    | datetime         | When the invite was last updated                        |
| `accepted_at`   | datetime         | When the invite was accepted - if applicable            |
| `is_accepted`   | boolean          | Whether the invite had been accepted                    |
| `created_by_id` | string           | The ID of the user who created the invite               |

</details>

<details>

<summary>Rewst - Managed Organization Added</summary>

The Rewst - Managed Organization Added trigger starts the workflow when a new parent organization is added in Rewst. This trigger is useful for:

* Automating client onboarding workflows when new managed organizations are added
* Sending notifications to internal teams about new clients
* Automatically provisioning resources or configurations for new organizations
* Syncing new organization data to external PSA, documentation, or CRM systems
* Triggering initial setup tasks like creating default users, permissions, or integrations
* Auditing and logging new organization creation events

When this trigger kicks off, it provides the following data in `triggering_organization_data`:

| Field             | Type     | Description                                  |
| ----------------- | -------- | -------------------------------------------- |
| `id`              | string   | The organization's unique identifier         |
| `tid`             | string   | The tenant ID                                |
| `name`            | string   | The organization's name                      |
| `domain`          | string   | The organization's domain                    |
| `is_msp`          | boolean  | Whether the organization is an MSP           |
| `created_at`      | datetime | When the organization was created            |
| `updated_at`      | datetime | When the organization was last updated       |
| `customer_id`     | string   | The customer ID                              |
| `roc_site_id`     | string   | The ROC site ID                              |
| `managing_org_id` | string   | The ID of the managing (parent) organization |
| `subscription_id` | string   | The subscription ID                          |

</details>

<details>

<summary>Rewst - Managed Organization Deleted</summary>

The Rewst - Managed Organization Added trigger starts the workflow when an existing parent organization is removed in Rewst. This trigger is useful for:

* Automating client offboarding workflows when managed organizations are removed
* Sending notifications to internal teams about client departures
* Cleaning up resources, configurations, or integrations associated with the deleted organization
* Syncing organization deletions to external PSA, documentation, or CRM systems
* Auditing and logging organization deletion events for compliance
* Revoking access or permissions tied to the deleted organization
* Archiving data or records related to the removed client

When this trigger fires, it provides the following data in `triggering_organization_data`:

| Field             | Type     | Description                                  |
| ----------------- | -------- | -------------------------------------------- |
| `id`              | string   | The deleted organization's unique identifier |
| `tid`             | string   | The tenant ID                                |
| `name`            | string   | The organization's name                      |
| `domain`          | string   | The organization's domain                    |
| `is_msp`          | boolean  | Whether the organization was an MSP          |
| `created_at`      | datetime | When the organization was originally created |
| `updated_at`      | datetime | When the organization was last updated       |
| `customer_id`     | string   | The customer ID                              |
| `roc_site_id`     | string   | The ROC site ID                              |
| `managing_org_id` | string   | The ID of the managing (parent) organization |
| `subscription_id` | string   | The subscription ID                          |

</details>

<details>

<summary>Rewst - Managed Organization Updated</summary>

The Rewst - Managed Organization Added trigger starts the workflow when an existing parent organization is updated in Rewst. This trigger is useful for:

* Syncing organization changes to external PSA, documentation, or CRM systems
* Sending notifications when client organization details are modified
* Auditing and logging organization update events for compliance
* Triggering workflows when organization settings or configurations change
* Updating related resources or integrations when organization data is modified
* Tracking changes to organization names, domains, or other key attributes

When this trigger kicks off, it provides the following data in `triggering_organization_data`:

| Field             | Type     | Description                                  |
| ----------------- | -------- | -------------------------------------------- |
| `id`              | string   | The organization's unique identifier         |
| `tid`             | string   | The tenant ID                                |
| `name`            | string   | The organization's name                      |
| `domain`          | string   | The organization's domain                    |
| `is_msp`          | boolean  | Whether the organization is an MSP           |
| `created_at`      | datetime | When the organization was originally created |
| `updated_at`      | datetime | When the organization was last updated       |
| `customer_id`     | string   | The customer ID                              |
| `roc_site_id`     | string   | The ROC site ID                              |
| `managing_org_id` | string   | The ID of the managing parent organization   |
| `subscription_id` | string   | The subscription ID                          |

</details>

<details>

<summary>Rewst - Updated User</summary>

The Rewst - Updated User trigger starts the workflow when a user is updated in Rewst. This trigger is useful for:

* Auditing user changes within Rewst
* Syncing user updates to external systems
* Triggering notifications when user roles or permissions change
* Logging user modifications for compliance purposes

When this trigger kicks off, it provides the following data in `triggering_user_data`:

| Field          | Type             | Description                             |
| -------------- | ---------------- | --------------------------------------- |
| `id`           | string           | The user's unique identifier            |
| `role`         | string           | The user's role                         |
| `org_id`       | string           | The organization ID the user belongs to |
| `role_ids`     | array of strings | List of role IDs assigned to the user   |
| `username`     | string           | The user's username                     |
| `created_at`   | datetime         | When the user was created               |
| `updated_at`   | datetime         | When the user was last updated          |
| `is_superuser` | boolean          | Whether the user is a superuser         |

</details>

<details>

<summary>Rewst - Updated User in Whitelist</summary>

The Rewst - Updated User in Whitelist trigger starts the workflow when a whitelist is updated in Rewst. This trigger is useful for automating actions when user invitations are modified in Rewst, such as:

* Logging changes to user access
* Notifying administrators of whitelist updates
* Triggering onboarding or offboarding workflows based on invite status changes

When this trigger kicks off, it provides the following data in `triggering_user_invite_data`:

| Field           | Type     | Description                                  |
| --------------- | -------- | -------------------------------------------- |
| `id`            | string   | The unique identifier of the user invite     |
| `email`         | string   | The email address of the invited user        |
| `org_id`        | string   | The organization ID the invite belongs to    |
| `role_ids`      | array    | List of role IDs assigned to the user        |
| `created_at`    | datetime | When the invite was created                  |
| `updated_at`    | datetime | When the invite was last updated             |
| `accepted_at`   | datetime | When the invite was accepted (if applicable) |
| `is_accepted`   | boolean  | Whether the invite has been accepted         |
| `created_by_id` | string   | The ID of the user who created the invite    |

</details>

## Other triggers

Rewst offers additional triggers for some of our integrations tailored to different automation needs. Explore the available triggers in the trigger type list to find the best fit for your specific processes. Try asking [RoboRewsty](../../rewst-tools/roborewsty.md) what each integration-specific trigger does to learn more about how it can be used, or read more about included triggers on each integration's info page in this site.

<figure><img src="../../../.gitbook/assets/trigger drop-down gif.gif" alt="A moving GIF image depicting scrolling through the trigger type list in an example organization in Rewst. Various integrations&#x27; actions are shown."><figcaption><p>The contents of the complete trigger type list will depend on your particular integrations</p></figcaption></figure>

