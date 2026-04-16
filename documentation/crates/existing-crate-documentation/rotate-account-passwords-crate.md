# Rotate Account Passwords Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the Rotate Account Passwords Crate do?

This Crate automates the secure rotation of administrative account passwords. It improves security by ensuring credentials are updated on a set schedule and stored safely in Hudu or IT Glue.

This Crate does not update accounts not listed in the configuration, grant or revoke permissions, or perform emergency password resets.

### How the Crate works

The Crate runs on a scheduled rotation, based on configured frequency preference. There's also a manual trigger for immediate rotation, if needed.&#x20;

* Identifies configured admin accounts
* Generates strong, random passwords that meet your policy
* Updates the account password in the target system
* Stores the new password in Hudu or IT Glue

## Crate prerequisites

Before unpacking this Crate, you'll need to successfully integrate either [IT Glue](../../integrations/integration-guides/it-glue-integration-setup.md) or [Hudu](../../integrations/integration-guides/hudu-integration-setup.md) with Rewst.

## Workflow breakdown

1. The workflow has a disabled trigger named `Monthly`, which when enabled would kick off this workflow on a recurring schedule.
2. The **START** task executes the **noop** action, serving as the entry point of the workflow and performing no operation other than initiating the flow.
3. On success, the **START** task transitions to the **workflows\_rewst\_task\_rotate\_admin\_password** task, which calls the sub-workflow action **\[REWST - TASK] Rotate Account Password**. This task is configured with a with-items loop that reads the organization variable `ORG.VARIABLES.rotate_admins`, splits it by comma into a list of usernames, and iterates over each one with a concurrency of 1. Each iteration passes the current username via `item()` as the `user_name` input to the sub-workflow.
4. If the **workflows\_rewst\_task\_rotate\_admin\_password** task succeeds, it transitions to the **END** task and publishes a data alias called `log_workflows_rewst_task_rotate_admin_password`. This alias contains a structured log object with a computed status code, an empty message, an empty data object, and the sub-automation log extracted from the result.
5. If the **workflows\_rewst\_task\_rotate\_admin\_password** task fails, it also transitions to the **END** task and publishes the same `log_workflows_rewst_task_rotate_admin_password` data alias with identical log-aggregation logic, ensuring that failure information is still captured.
6. The **END** task executes the **noop** action and has a single terminal transition that publishes the `automation_log` variable into CTX. This Jinja template iterates over all CTX variables whose keys start with "log\_", aggregates them into a list of log entries, computes an overall status code — 1000 for full success, 1001 for warnings, or 2000 for errors — and assembles a final summary object containing the status code, a succeeded flag, aggregated data, a list of errors, a list of warnings, and all individual log entries.
7. The workflow outputs the `automation_log` from CTX as its final output, making the aggregated results of all password rotation operations available to any parent workflow.

## Unpack the Rotate Account Passwords Crate

1. Navigate to **Marketplace > Crates** in the left side menu of the Rewst platform.
2. Search for `Rotate Account Passwords`**.**\
   \
   ![](<../../../.gitbook/assets/image (191).png>)
3. Click on the Crate tile to begin unpacking.
4. Click **Continue**.
5. Decide if you want the workflow in the Crate to run on a schedule or by manual triggering.
   1. Leave **Enabled** toggled on to use a cron trigger and schedule
   2. Toggle **Enabled** to off to use the workflow with a manual trigger
6. Choose which organizations you would like to activate this Crate for via the **Activate for organizations** drop-down selector.&#x20;
7. Add **Trigger Criteria** and **Integration Overrides**, if desired.
8. Click **Unpack**.

### Set up the organization variable for the Crate

Make an organization variable called `rotate_admins`  for each organization that you want to rotate passwords for. Follow setup instructions here for [how to create new organization variables](../../integrations/organization-variables.md).

In the organization variable, give a list of users for all accounts you want to rotate. Format that list comma delimited. For example, `job_admin,paul_admin,steve_admin`.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-08-19 at 3.52.50 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Note that if you test or run the workflow in this Crate before setting up the rotate\_admins organization variable, your workflow will still show as successful, but will consider the list of users to be empty.&#x20;
{% endhint %}

### Update the cron trigger

{% hint style="info" %}
To test this Crate, you'll need to adjust the cron trigger's schedule to a few minutes in the future, then adjust it back to your regular schedule after the test. Alternatively, you could wait until the regularly scheduled run occurs and check your result, which would not require you to update the cron trigger schedule.&#x20;
{% endhint %}

1. Navigate to **Automations > Workflows** in the left side menu of your Rewst platform.
2. Search for `[REWST - CRATE] Rotate Admin Passwords`.
3. Click the workflow to view it in the Workflow Builder.
4. Click on the trigger in the workflow to open its settings in the right side menu.
5. Update the timing of the cron trigger as desired. Note that when entering the time into the Cron Schedule field, the correct format is minutes followed by hour. For example, 18 3, not 3 18.
6. Click **Save Trigger**.

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
