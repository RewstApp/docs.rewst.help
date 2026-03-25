# Add Users to Rewst via Group Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the Add Users to Rewst via Group Crate do?

Our Add Users to Rewst via Group Crate syncs membership from a Microsoft 365 group to Rewst by automatically inviting any group members who don't already have a Rewst account or pending invite. It's designed to run on a schedule, with Cron and Time Interval triggers, to keep Rewst user access in sync with an M365 group.

### Workflow breakdown

1. The workflow is initiated by one of two triggers: a **Cron Trigger** or a **Time Interval** trigger.
2. The first task, **microsoft\_graph\_list\_groups**, uses the **List Groups** action from the Microsoft Graph integration to search for a group whose display name matches the value stored in CTX.group\_name. This task uses a "follow first" transition mode, meaning only the first matching condition will be followed.
3. If the **microsoft\_graph\_list\_groups** task succeeds but returns zero results, the workflow transitions to the **rewst\_group\_not\_found** task, which uses the **noop** action to signal that the specified group could not be found, and the workflow ends.
4. If the **microsoft\_graph\_list\_groups** task fails entirely, the workflow transitions to the **failed\_to\_list\_groups** task, which uses the **noop** action and serves as a reminder to check that the organization is properly mapped. The workflow ends here.
5. If the **microsoft\_graph\_list\_groups** task succeeds and returns results, the group ID from the first result is published into context, and the workflow transitions to the **graph\_get\_transitive\_group\_members** task, which uses the **Graph API Request** action from the Microsoft Graph integration to retrieve all transitive members of that group. The result is published as "graph\_users" in context.
6. If the **graph\_get\_transitive\_group\_members** task fails, the workflow transitions to the **failed\_to\_get\_group\_members** task, which uses the **noop** action and advises checking delegated permissions. The workflow ends here.
7. If the **graph\_get\_transitive\_group\_members** task succeeds, the workflow transitions to the **rewst\_list\_users\_by\_organization** task, which uses the **List Users by Organization** action from the Rewst integration to retrieve all current users and pending invites for the organization. The result is published as "rewst\_users" in context.
8. After successfully listing Rewst users, the workflow transitions to the **find\_noninvited\_users** task, which uses the **noop** action. On its success transition, a data alias compares the graph group members against the existing Rewst users and pending invites, building a list of email addresses that have not yet been invited. This list is published as "new\_additions" in context.
9. The workflow then transitions to the **check\_for\_new\_adds** task, which uses the **noop** action with a follow first transition mode. If the "new\_additions" list has one or more entries, the workflow publishes an "index" variable set to zero and a "count" variable set to the total number of new additions, then transitions to the **loop\_check** task. If there are no new additions, the workflow ends.
10. The **loop\_check** task uses the **noop** action and acts as the loop controller with a join of one and a follow first transition mode. If the current index is less than the count, the workflow transitions to the **rewst\_create\_invite\_in\_user\_whitelist** task. If the index has reached the count, the workflow ends.
11. The **rewst\_create\_invite\_in\_user\_whitelist** task uses the **Invite User to Rewst** action from the Rewst integration to invite the user at the current index position in the "new\_additions" list, using the roles stored in CTX.roles, with email sending disabled.
12. If the **rewst\_create\_invite\_in\_user\_whitelist** task succeeds, the index is incremented by one and the workflow transitions back to the **loop\_check** task to process the next user.
13. If the **rewst\_create\_invite\_in\_user\_whitelist** task fails, the index is still incremented by one, and the workflow transitions to the **user\_already\_invited** task, which uses the **noop** action to acknowledge the failure — likely because the user was already invited — before transitioning back to the **loop\_check** task to continue processing remaining users.
14. The loop continues cycling through steps 10 through 13 until all users in the "new\_additions" list have been processed, at which point the **loop\_check** task's index equals the count and the workflow completes.

## Crate prerequisites

Rewst's [Microsoft Cloud Integration Bundle](../../integrations/integration-guides/microsoft-cloud-integration-bundle/) must be set up before unpacking this Crate.&#x20;

## Unpack the Add Users to Rewst via Group Crate

1. Navigate to **Marketplace** **> Crates** in the left side menu of the Rewst Platform.
2.  Search for `Add Users to Rewst via Group`.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot 2026-03-25 at 9.05.58 AM.png" alt="" width="262"><figcaption></figcaption></figure>
3. Click on the Crate tile to begin the unpacking process.
4. Click **Unpack Crate**.
5. Make your selections for the group you would like to be used with the Crate:
   1. Timing can be set to **Daily** or **Twice per Day**.
   2. Enter the name of your relevant Azure AD Group into the field.
   3. Choose the roles of the users to be included from the drop-down selector: **Forms Only**, **Member**, or **Admin**.
6. Click **Continue**.
7. By default, the cron trigger option of the Crate is set to enabled. If you wish to use the time interval trigger, disable the cron trigger. You'll need to go into the workflow after it's unpacked from the Crate and [enable the interval trigger](../../automations/intro-to-triggers/#modify-an-existing-trigger) from the Workflow Builder.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-03-25 at 9.16.48 AM.png>)
8. Note that you have the option under the **Configure Triggers** accordion menu to activate the Crate for all future organizations in addition to the current one. Current org-only is the default. You may also set activation to certain [tags](https://docs.rewst.help/documentation/settings/tags-in-rewst), [trigger criteria](../../automations/intro-to-triggers/trigger-criteria.md), or for integration overrides.
9. Click **Unpack Crate**.

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
