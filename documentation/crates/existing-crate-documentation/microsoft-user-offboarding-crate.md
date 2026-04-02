# Microsoft: User Offboarding Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Crate in our Crate Marketplace.
{% endhint %}

## What does the Microsoft: User Offboarding Crate do?

Our Microsoft: User Offboarding Crate streamlines the offboarding process for users within an organization, for time savings and increased efficiency. The automation is triggered via a form submission, allowing designated personnel to initiate the offboarding tasks.

* **Detailed ticketing**: Automation logging steps that are done throughout the offboarding process are documented by logging entries to the ticket, via a single note, making it easier to tell where an issue occurred and what steps were performed.
* **Efficiency**: Streamline the user offboarding process by increasing time savings and decreasing the potential for user error.
* **Security**: Ensure that necessary offboarding steps are performed when an account is terminated.

{% hint style="warning" %}
This Crate does not handle On-Prem Exchange and will only handle Exchange functionality via Office 365.\
It does not take action to remove the licenses from your license vendor.&#x20;
{% endhint %}

This Crate does the following tasks:

* Detailed Ticketing
* Offboarding Approval Process
* Offboarding Delay
* Supervisor Notifications
* Session Invalidation
* Password Reset
* Exchange Actions
* Convert to shared mailbox
* Assignment of shared mailbox permissions
* Hide from GAL
* Forward mail
* Set out of office
* Remove mobile devices
* Disable Accounts
* Move OU
* Group Membership Removal
* Employee ID Removal
* Disable PSA Contact
* Removal of Supervisor Assignment
* License Removal

## Crate prerequisites

The [Microsoft Cloud Integration Bundle](../../integrations/integration-guides/microsoft-cloud-integration-bundle/) must be set up before unpacking this Crate.

### Identity provider configuration

* Azure AD Only
* Hybrid On-Prem and Azure AD: Synced
* Hybrid On-Prem and Azure AD: No Sync
* On-Prem Only

## Set up the Microsoft: User Offboarding Crate

1. Navigate to **Marketplace > Crates** in the Rewst platform.
2. Search for `Microsoft: User Offboarding`.
3. Click on the Crate tile to begin unpacking.\
   \
   ![](<../../../.gitbook/assets/image (177).png>)
4. Click **Unpack Crate**.
5. Click **Continue**.
6. Click **Unpack.**
7. The [organization variable](../../integrations/organization-variables.md#manually-add-a-new-organization-variable) `user_offboard_form_name` must be set  to the name of the form unpacked with the Crate.&#x20;

## Use the Microsoft: User Offboarding Crate

1. Navigate to **Automations > Workflows** in the Rewst platform
2. Search for `Microsoft: User Offboarding`.
3. Click into the workflow.
4.  Click ![](<../../../.gitbook/assets/image (196).png>) to navigate to the trigger.\
    <br>

    <figure><img src="../../../.gitbook/assets/image (61) (3).png" alt=""><figcaption></figcaption></figure>
5. Click **View Direct URLs.**
6.  Select the company you'd like to use to test the workflow. Copy the URL and paste it into a new window.<br>

    <figure><img src="../../../.gitbook/assets/image (62) (4).png" alt=""><figcaption></figcaption></figure>
7.  Fill out the form as appropriate for the company and user you are offboarding. Make sure to click **Submit** at the end of the form.<br>

    <figure><img src="../../../.gitbook/assets/image (63) (2).png" alt=""><figcaption></figcaption></figure>
8.  Once the form is submitted, the workflow will begin to run. To view the results, click <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.40.07 PM (1).png" alt="" data-size="line"> in the workflow editor page.<br>

    <figure><img src="../../../.gitbook/assets/image (65) (2).png" alt=""><figcaption></figcaption></figure>
9. Click into the results to see the execution results with successes and failures, if there are any.

<figure><img src="../../../.gitbook/assets/image (66) (2).png" alt=""><figcaption></figcaption></figure>



### Example of end of ticket output

<details>

<summary>Example of end of ticket output for the Microsoft: User Offboarding Crate</summary>

Offboading for John Smith completed.

User was removed from the following groups: test distro list test security group Actual No Really LLC

Could Not Remove User from Dynamic Groups: All Users

Automation Logs:

Automation Complete

Succeeded: True

Status Code: 1001

Warnings: Entry: Group removal completed with warning, this is usually due to the user being a member of a dynamic group. - Status: 1001

Errors: No errors reported.

Full Automation Log:

Entry: Successfully sanitised all expected strings - Status: 1000

Entry: Determined IDP to be: on\_prem - Status: 1000

Entry: Valid IDP was determined. - Status: 1000

Entry: Gathered user details successfully. - Status: 1000

Entry: No ticket provided via form, creating ticket. - Status: 1000

Entry: Successfully created the PSA Ticket - Status: 1000

Entry: Successfully updated the PSA Ticket - Status: 1000

Entry: No approval needed, continuing. - Status: 1000

Entry: Delay requested. - Status: 1000

Entry: Successfully delayed automation until expected time. - Status: 1000

Entry: Successfully returned a defined password. - Status: 1000

Entry: Notification to supervisor requested. - Status: 1000

Entry: Successfully completed call to lookup supervisor. - Status: 1000

Entry: Successfully verified email of supervisor. - Status: 1000

Entry: Notified supervisor. - Status: 1000

Entry: Invalidate sessions chosen in form, initiating invalidation of sessions. - Status: 1000

Entry: Successfully invalidated sessions. - Status: 1000

Entry: Successfully changed password. - Status: 1000

Entry: Exchange actions chosen in form, initiating Exchange actions. - Status: 1000

Entry: Performed Exchange actions. - Status: 1000

Entry: Disable account chosen in form, disabling user. - Status: 1000

Entry: Successfully disabled account. - Status: 1000

Entry: Environment variables indicate AD Sync is needed, attempting AD Sync. - Status: 1000

Entry: Attempted to run AD Sync. Workflow completed successfully but this doesn't indicate a successful AD Sync. - Status: 1000

Entry: Group removal completed with warning, this is usually due to the user being a member of a dynamic group. - Status: 1001

Entry: Employee ID removal not requested, skipping. - Status: 1000

Entry: PSA contact removal requested, attempting removal. - Status: 1000

Entry: Successfully ran disable\_psa\_contact task. - Status: 1000

Entry: Supervisor/Manager attribute removal requested, attempting removal. - Status: 1000

Entry: Successfully removed supervisor. - Status: 1000

Entry: Attempted to run AD Sync. Workflow completed successfully but this doesn't indicate a successful AD Sync. - Status: 1000

Entry: Attempting to move user to another OU. - Status: 1000

Entry: Moved user to the requested OU. - Status: 1000

Entry: Workflow complete, attempting ticket update. - Status: 1000

</details>

## Org variables in use for the Microsoft: User Offboarding Crate

{% hint style="info" %}
For information specific to these org variables please review our guidance organization variables [here](../../integrations/organization-variables.md).&#x20;

Note that org variables not found in the organization variables documentation are typically system variables that are handled by the integration mappings.

If you haven't done so already, it's recommended that you run the [org variable configuration crate](https://app.rewst.io/marketplace/crates/eb2e46d9-56b1-4561-b9e6-c281a1275c67), which will help you set org variables that are relevant to you and your customer's environments.
{% endhint %}

* `agent_smith_is_installed`
* `automation_task_new_user_time`
* `automation_task_offboard_user_time`
* `azure_iothub_name`
* `azure_iothub_resource_group`
* `azure_iothub_subscription_id`
* `cwControl_CompanyName`
* `cw_automate_client_id`
* `cw_control_session_group_override`
* `cw_manage_company_id`
* `datto_company_id`
* `datto_note_type`
* datto\_rmm\_site\_id
* `default_psa`
* `default_rmm`
* `failure_email`
* `freshdesk_company_id`
* `halo_psa_client_id`
* `halo_ticket_site_name`
* `immybot_tenant_id`
* `kaseya_bms_account_id`
* `kaseya_vsa_10_scriptid`
* `kaseya_vsa_org_id`
* `kaseya_vsa_x_org_id`
* `nable_customer_id`
* `nable_device_filter_id`
* `nable_rewst_powershell_script_id`
* `new_user_approval_email`
* `ninja_org_id`
* `ninja_run_as_user`
* `no_azure_ad`
* `no_ticket_time`
* `onprem_no_adsync`
* `preferred_domain_controller`
* `primary_domain_controller`
* `primary_identity_provider`
* `priority`
* `psa_alert_ticket_type`
* `psa_all_notes_internal`
* `psa_datto_default_issue_type`
* `psa_datto_default_sub_issue_type`
* `psa_datto_default_ticket_category`
* `psa_datto_default_ticket_type`
* `psa_default_agreement_name`
* `psa_default_board_id`
* `psa_default_tech_id`
* `psa_default_tech_workrole`
* `psa_default_tech_worktype`
* `psa_default_ticket_impact`
* `psa_default_ticket_priority`
* `psa_default_ticket_source`
* `psa_default_ticket_status`
* `psa_default_ticket_urgency`
* `psa_halo_cab_id`
* `psa_halo_cab_type`
* `psa_halo_ticket_outcome_completed_task`
* `psa_new_user_ticket_subtype`
* `psa_new_user_ticket_type`
* `psa_no_ticket_time`
* `psa_offboarding_user_ticket_item`
* `psa_offboarding_user_ticket_subtype`
* `psa_offboarding_user_ticket_type`
* `psa_ticket_status_completed_task`
* `psa_ticket_status_waiting_input`
* `require_approval_for_offboarding_users`
* `rmm_preferred_adconnect_server`
* `servicenow_account_id`
* `time_entry_ticket_status`

## Recommended migration path

{% hint style="warning" %}
☝️If you’re using a previous version of the onboarding workflow, follow these migration steps below. If this is your first time using this Crate, this information isn't relevant to you.
{% endhint %}

1. Unpack this Crate in your environment.
2. Perform testing to make sure that you have all the required organization variables set correctly. The same variables are used in this updated Crate as were used in the previous version. If you need to update any organization variables, then please follow [this guide](https://docs.rewst.help/prebuilt-automations/existing-crate-documentation/configure-organization-variables).
3. After testing and confirming that it is functioning as expected, please move forward with the steps below:
   1. If you plan to utilize the updated form in this crate, rather than the legacy form:
      1. Go to the [previous crate's](https://app.rewst.io/marketplace/crates/018fdeb1-347e-7de5-93d9-61f6ce9fba31) top level workflow and disable any form triggers. This will prevent users from submitting requests to the wrong workflow.
      2. Update your internal documentation with the new form links.
      3. If Applicable, provide your customers with their new form link.
   2. You are able to link the previous Crates form to this version, though given the minimal differences there may not be a clear advantage other than not needing to change the link destinations. The previous form will not receive any further updates or enhancements.

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
