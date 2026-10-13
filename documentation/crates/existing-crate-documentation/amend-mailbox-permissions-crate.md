# Amend Mailbox Permissions Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Amend Mailbox Permissions Crate in our Crate Marketplace.
{% endhint %}

## What does the Amend Mailbox Permissions Crate do?

Easily manage permissions for mail-enabled mailboxes in your environment. This Crate allows you to add, remove, or view both FullAccess and SendAs permissions, ensuring that all changes are audited and logged in your PSA.

### How the Crate works

* Choose the mail-enabled mailbox you wish to manage.
* Add, remove, or view FullAccess and SendAs permissions as required.
* All changes are automatically logged in a ticket in your PSA for auditing purposes.

### Workflow breakdown

1. The workflow begins at the **START** task, which calculates a count of permission operations to be performed based on the input parameters for adding or removing full access and send as permissions.
2. The workflow checks if PSA integration is properly configured by verifying that a default PSA system is set in the organization variables and determines the appropriate company ID based on the PSA type.
3. The system validates that the workflow is being executed from the associated form by checking for the presence of a user\_id parameter in the context.
4. The workflow retrieves user information for the specified mailbox by executing a Get-Mailbox command through **Microsoft Exchange Online InvokeCommand** to obtain the display name and other mailbox details.
5. The system determines whether a ticket ID was provided as input and branches accordingly - if no ticket is provided, it proceeds to create a new PSA ticket, otherwise it updates the existing ticket with initial information.
6. If creating a new ticket, the workflow verifies that the company\_id organization variable is properly configured before proceeding with PSA ticket creation using **\[REWST - PROCESS] PSA: Create Ticket** and the mailbox user's display name in the summary.
7. After ticket handling, the workflow evaluates the add\_remove\_view parameter to determine the requested operation type and branches to the appropriate permission management path.
8. For adding permissions, the workflow first checks if there are users to be granted full access permissions and processes them using **\[REWST - TASK] Modify Mailbox Access** with iterative execution for each user.
9. The system then checks for users requiring send as access permissions and processes those additions using the same **\[REWST - TASK] Modify Mailbox Access** with appropriate permission settings.
10. For removing permissions, the workflow retrieves existing mailbox permissions using **\[REWST - OPT GEN] Get Mailbox Folder Permissions** to identify current permission holders.
11. The system processes the existing permissions data to create lists of users whose full access and send as permissions need to be removed based on the input parameters.
12. The workflow removes full access permissions for identified users by iterating through the removal list and executing **\[REWST - TASK] Modify Mailbox Access** for each user.
13. Similarly, the system removes send as permissions for the specified users through iterative execution of **\[REWST - TASK] Modify Mailbox Access**.
14. After completing permission modifications, the workflow updates the PSA ticket with detailed information about which users had permissions added or removed using **\[REWST - PROCESS] PSA: Update Ticket**, including their names and the specific permission types.
15. For view permissions operations, the workflow bypasses all modification steps and proceeds directly to the completion phase.
16. The workflow concludes at the **END** task using **noop**, which publishes the complete automation log containing all operation results and status information for tracking and auditing purposes.
17. Throughout the entire process, any task failures are routed to a failed task that logs the error using **noop** and proceeds to the End task to ensure proper workflow completion and logging.

## Crate prerequisites

* The [Microsoft Cloud Integration Bundle](../../integrations/integration-guides/microsoft-cloud-integration-bundle/) must be set up before unpacking this Crate.
* Your PSA must be [integrated with Rewst](https://docs.rewst.help/documentation/integrations/psa).

## Unpack the Amend Mailbox Permissions Crate

1. Navigate to **Marketplace** **> Crates** in the left side menu Rewst platform.
2. Search for the `Amend Mailbox Permissions` Crate.
3. Click on the Crate tile to begin unpacking.
4. This will open that PSA integration’s configuration form in a new tab. Note that this list will have check marks if you have already met the prerequisite integration and org variable setup needs.
5. Click **Unpack Crate**.
6. Choose your PSA from the drop down list.
7. Click **Continue**.
8. Change the **Workflow name**, if desired.
9. Leave form options at their default state.
10. Click **Unpack**.

## Amend Mailbox Permissions form

### Access the form

1. Navigate to **Automations** **> Assets > Forms** in the left side menu of your Rewst platform.
2. Search for `[Rewst] M365: Amend Mailbox Permissions`.
3. Click **⋮ > Usages > View Direct URLs.**
4.

```
<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>
```

5. Click on the form for the child organization, or use the parent org form for MSPs form users.

### Fill out the form

<figure><img src="../../../.gitbook/assets/Screenshot 2025-09-15 at 4.15.45 PM.png" alt=""><figcaption></figcaption></figure>

1. Choose the specific client for whom permissions will be modified. Click the drop down arrow of the **Client** field, or begin typing the name into the field to jump to the client name.
2. Click the drop down arrow of the **Ticket** field, or begin typing the name into the field to jump to the ticket name related to the request.
3. Select the mail-enabled user to perform the permission modification action on.
   1. Both of these mailbox types will work with the form:
      1. Individual User Accounts: `john.smith@pedroaviary.com`
      2. Shared Mailboxes: `hr-manager@pedroaviary.com`
4. Click on one of the following actions to specify the type of permission modification you would like to execute. Clicking on each will add additional relevant fields and options to the form.
   1. **Add Perms**: Grant new access rights via **Add Full Access Users to Selected Mailbox** and **Add Send As Access Users to Selected Mailbox**
   2. **Remove Perms**: Revoke existing access via **Remove Existing Full Access Users** and **Remove Existing Send As Users**
   3. **View Perms**: Check current access levels via **All Perms** permission data check
5. Click **Submit**.

### Add permissions form example

**Fields**:

* **Client**: Cluck-U
* **Ticket**: Grant John Smith the mailbox access.
* **User**: `john.smith@pedroaviary.com`
* **Action Type**: Add Perms
* **Add Full Access Users**:
  * `hr-assistant@pedroaviary.com`
  * `sys-admin@pedroaviary.com`
* **Add Send As Access Users**:
  * `regional-hr@pedroaviary.com`
  * `compliance-officer@pedroaviary.com`

<figure><img src="../../../.gitbook/assets/Add Permissions.gif" alt=""><figcaption></figcaption></figure>

### Remove permissions form example

**Fields**:

* **Client**: Cluck-U
* **Ticket**: Remove John Smiths access
* **User**: `john.smith@pedroaviary.com`
* **Action Type**: Remove Permissions
* **Remove Existing Full Access Users**:
  * `former-hr-assistant@pedroaviary.com`
*   **Remove Existing Send As Users**:

    * `transferred-manager@pedroaviary.com`

    <figure><img src="../../../.gitbook/assets/Remove Permissions.gif" alt=""><figcaption></figcaption></figure>

### View permissions form example

**Fields**:

* **Client**: Cluck-U
* **Ticket**: Report mailbox permissions for John Smith
* **User**: `john.smith@pedroaviary.com`
*   **Action Type**: View Permissions

    Example Permission Data for `john.smith@pedroaviary.com`

    > This user has access to the **Shared Mailbox - HR Assistant -** [**hr-assistant@pedroaviary.com**](mailto:hr-assistant@pedroaviary.com) **mailbox** Full Access Users

    **User:** [hr-assistant@pedroaviary.com](mailto:hr-assistant@pedroaviary.com) **Access Rights:** Full Access

    **User:** [sys-admin@pedroaviary.com](mailto:sys-admin@pedroaviary.com) **Access Rights:** Full Access

    Send As Users **User:** [regional-hr@pedroaviary.com](mailto:regional-hr@pedroaviary.com) **Access Rights:** Send As

    **User:** [compliance-officer@pedroaviary.com](mailto:compliance-officer@pedroaviary.com) **Access Rights:** Send As

    >

<figure><img src="../../../.gitbook/assets/View Permissions.gif" alt=""><figcaption></figcaption></figure>

### What happens during permission modifications?

#### Adding permissions

* **User verification process**
  * Validates user identities across the organization
  * Ensures users are correctly mapped to the intended mailbox
  * Checks existing permission levels before addition
* **Permission granting workflow**
  * Systematically applies requested access rights
  * Supports multiple simultaneous permission additions
  * Handles complex permission scenarios across different user groups
* **Comprehensive tracking**
  * Generates detailed audit trail of all permission changes
  * Captures metadata about the permission modification
  * Links permission changes to specific organization context
* **Notification and documentation**
  * Automatically creates or updates support tickets
  * Logs all permission modification details
  * Provides clear, traceable record of access changes

#### Removing permissions

* **Permission revocation process**
  * Methodically removes specified access rights
  * Supports bulk and individual user permission removals
  * Ensures complete and immediate access termination
* **Access validation**
  * Confirms current permission status before removal
  * Prevents unnecessary or redundant access revocation
  * Maintains integrity of mailbox access controls
* **Security and compliance tracking**
  * Creates comprehensive removal logs
  * Documents rationale for permission changes
  * Supports organization security and compliance requirements
* **Automated reporting**
  * Updates relevant ticketing systems
  * Generates immediate notifications of access changes
  * Provides clear audit trail for management review

#### Viewing permissions

* **Comprehensive access snapshot**
  * Retrieves complete permission landscape for a mailbox
  * Displays all current access levels and user rights
  * Offers granular visibility into mailbox access configurations
* **Detailed permission mapping**
  * Shows Full Access and Send As permission details
  * Identifies all users with specific mailbox access
  * Provides context for each permission type
* **Reporting and insights**
  * Generates instant permission overview
  * Supports security audits and access reviews
  * Enables quick identification of potential access risks
* **Flexible exploration**
  * Allows drill-down into specific permission details
  * Supports various reporting and export formats
  * Facilitates comprehensive access management

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
