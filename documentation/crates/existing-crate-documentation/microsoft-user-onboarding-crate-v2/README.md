# Microsoft: User Onboarding Crate

{% hint style="info" %}
This Crate is a big one! Unlike most of our other Crates, our documentation for the Microsoft: User Onboarding Crate is spread over several pages. Look in the left side tree of the navigation menu for our documentation site, and click through the pages nested under this one to see all related documentation.
{% endhint %}

## **What does the Microsoft: User Onboarding Crate do?**

The Microsoft: User Onboarding Crate automates the user onboarding process by streamlining account creation, group assignments, licensing, and additional configurations across Microsoft Entra ID, formerly known as Azure AD, and on-premises Active Directory.

Ensure that new employees or contractors are provisioned accurately and consistently based on predefined policies, integrating seamlessly with PSA, RMM, documentation, and licensing systems.

## **Why use the Microsoft: User Onboarding Crate?**

This Crate is ideal for MSPs and IT teams managing Microsoft environments.

* Automate user creation, group assignments, and licensing
* Configure On-Prem AD, Azure AD, or Hybrid environments
* Assign Microsoft 365 licenses, security groups, and shared mailboxes
* Enforce password policies, role-based access, and MFA registration
* Log user details in your PSA and external documentation platforms
* Create or update tickets or send emails
* Requires manual approval before provisioning users

## Supported configurations

<details>

<summary>Multi-environment support: Identity providers</summary>

Defines how users are created and managed across Active Directory and Azure AD.

* On-Prem AD Only – Users exist only in on-prem Active Directory, with no cloud integration.
* Azure AD Only – Users are created directly in Microsoft Entra ID (Azure AD), without an on-prem AD account.
* Hybrid with AD Sync – Users are created in both AD and Azure AD, synchronized via AD Connect.
* Hybrid with No AD Sync – Users are manually created in both AD and Azure AD, without synchronization.

</details>

<details>

<summary>Ticket creation: supported PSAs</summary>

Lists the PSA tools that support ticket creation.

* ConnectWise PSA – A popular PSA solution for IT service management.
* Datto Autotask PSA – Cloud-based PSA software designed for MSPs.
* Freshdesk – Customer support and ticketing platform.
* HaloPSA – IT service management platform with automation and reporting.
* Kaseya BMS – Business management solution for MSPs.
* ServiceNow – Enterprise IT service management and workflow automation.
* Email Only – Ticket creation via email, without PSA integration.

</details>

<details>

<summary>Active directory configurations: Supported RMMs</summary>

Lists the Remote Monitoring and Management (RMM) tools necessary for retrieving data from Active Directory.

* ConnectWise Automate – RMM platform for remote monitoring and automation.
* Datto RMM – Cloud-based RMM for endpoint management and automation.
* NinjaOne – IT management platform for monitoring and remote access.
* ImmyBot – Automated deployment and configuration management tool.
* ConnectWise Control – Remote support and remote access solution.
* Kaseya VSA – IT automation and RMM tool for IT professionals.
* Kaseya VSA X – Next-gen version of Kaseya VSA with enhanced capabilities.
* N-able N-central – RMM platform for endpoint and network management.
* Agent Smith – RMM tool for system automation and monitoring.

</details>

<details>

<summary>IT documentation platforms and password management systems</summary>

Tools used for IT documentation and secure password storage.

* Hudu – IT documentation and password management platform for MSPs.
* IT Glue – Documentation platform with password vault and automation features.

</details>

<details>

<summary>Automatic licensing: supported distributors</summary>

Lists distributors that support automatic license provisioning for Microsoft CSP and other software.

* Microsoft CSP Direct – Direct Microsoft Cloud Solution Provider.
* Pax8 – Cloud distributor specializing in SaaS solutions for MSPs.
* Ingram Micro – Global IT distributor with cloud services.
* Sherweb – Cloud solutions provider with Microsoft licensing.
* Synnex – IT distributor offering cloud and software licensing.
* Manual Process – For cases where automated provisioning isn't available, Rewst pauses the workflow, inserts a ticket note indicating a license needs to be purchased manually with a link to continue the workflow after the steps have been manually performed, and resumes automatically once the link to continue is clicked. The link should only be clicked after the license has been purchased. You don't need to assign the license to the user

</details>

## How the Crate works

Once the form unpacked from the Crate is submitted, the Microsoft: User Onboarding Crate executes the following steps:

#### **1. Form submission and validation**

* The process starts when a user submits the \[Crate] Microsoft: User Onboarding form.
* The workflow checks if the user already exists in AD or Azure AD.
* The form captures necessary user details, including personal information, group memberships, licensing, and security settings.
* PSA integration retrieves the user's location, if available.
* If the New User Approval System is enabled, an approval request is sent before proceeding.
* All required fields are validated before proceeding.

#### **2. Ticket creation and management**

* If no ticket exists, a new one is created.
* If a ticket already exists, it is updated with onboarding progress.

#### **3. User account creation**

* The user account is created based on the selected identity provider:
  * On-Prem AD Only: A new AD account is created.
  * Azure AD Only: A new Entra ID (Azure AD) account is created.
  * Hybrid with Sync: A new AD account is created and synced to Azure AD.
  * Hybrid with No Sync: Separate accounts are created in both directories.

#### **4. Group and license assignments**

* Security groups are assigned in AD or Azure AD.
* Microsoft 365 licenses are applied via direct assignment or group membership.
* Shared mailbox permissions are configured if applicable.

#### **5. Credential and notification handling**

* A secure temporary password is generated.
* The password is securely stored in PSA, ITGlue, Hudu, or sent via email or SMS.
* The user’s manager may optionally be notified of credential details.

#### **6. Ticket update and completion**

* Final provisioning details are logged in the PSA ticket.
* The onboarding process is marked complete, and workflow logs are stored.

### **Workflow breakdown by identity provider type**

{% hint style="info" %}
Expand each of the provider types below to see their individual workflow breakdown.
{% endhint %}

<details>

<summary> <strong>On-premise AD only</strong></summary>

* Main workflow: Creates a user in Active Directory.
* Subworkflows:
  * Assigns security groups.
  * Configures mapped drives and home directories.
  * The password is sent via email, SMS, or documented in ITGlue, Hudu, or the PSA system.
  * Updates PSA ticket with user details.

</details>

<details>

<summary>Azure Active Directory only</summary>

* Main workflow: Creates a user in Azure AD (Entra ID).
* Subworkflows:
  * Assigns Microsoft 365 licenses.
  * Adds users to Microsoft 365 groups and shared mailboxes.
  * The password is sent via email, SMS, or documented in ITGlue, Hudu, or the PSA system.
  * Updates PSA ticket with user details.

</details>

<details>

<summary>Hybrid with AD sync</summary>

* Main workflow: Creates a user in Active Directory and syncs to Azure AD.
* Subworkflows:
  * Assigns both on-prem AD and Azure AD groups.
  * Applies Microsoft 365 licensing.
  * The password is sent via email, SMS, or documented in ITGlue, Hudu, or the PSA system.
  * Updates PSA ticket with sync confirmation.

</details>

<details>

<summary>Hybrid with no AD sync</summary>

* Main Workflow: Creates separate accounts in Active Directory and Azure AD.
* Subworkflows:
  * Assigns security groups for each directory independently.
  * Applies Microsoft 365 licensing.
  * The password is sent via email, SMS, or documented in ITGlue, Hudu, or the PSA system.
  * Updates PSA ticket with user details.

</details>

{% hint style="warning" %}
Ensure that the correct organizational variables are set for each configuration to avoid provisioning issues.
{% endhint %}

## Crate prerequisites

Before unpacking the Microsoft: User Onboarding Crate, make sure that the following requirements are met.

### Required integrations

* The [Microsoft Cloud integration bundle](https://docs.rewst.help/documentation/integrations/cloud/-cloud-integration-bundle) must be set up first. This enables Microsoft Graph API access for Azure AD and M365 provisioning.
* &#x20;For Active Directory setup, you’ll need to first set up your [RMM integration](https://docs.rewst.help/documentation/integrations/rmm), or [Agent Smith](https://docs.rewst.help/documentation/agent-smith). This is optional.
* [PSA Integration](https://docs.rewst.help/documentation/integrations/psa) must be setup. This is required for automated ticket creation and ticket updates. This is optional.
* [Documentation Integrations](https://docs.rewst.help/documentation/integrations/documentation) must be set up if you wish to create documentation in your knowledge base. This is optional.
* [Licensing integrations](https://docs.rewst.help/documentation/integrations/licensing) should be completed if you wish to set up automated license purchases. Configure Pax8, Ingram Micro, Sherweb, or Synnex. This is optional.
* [OpenText SecureCloud](../../../integrations/integration-guides/opentext-secure-cloud-integration.md) must be integrated with Rewst if you wish to use OpenText SecureCloud with this Crate. This is optional.
* [ArrowSphere](../../../integrations/integration-guides/arrowsphere-integration.md) must be integrated with Rewst if you wish to use this Crate for user license purchasing. This is optional.
* [ConnectWise ASIO](../../../integrations/integration-guides/connectwise-asio-integration.md) must be integrated with Rewst if you wish to use this Crate with that integration.

### Overview of required context variables and organizational variables

The Microsoft: User Onboarding Crate uses context variables (CTX) and organizational variables to control user provisioning, security settings, licensing, and ticketing workflows.

* CTX variables store dynamic, user-specific data that persists throughout the onboarding process.
* Org variables define global settings for how Rewst interacts with Active Directory, Azure AD, PSA, RMM, and other integrations.

These variables must be correctly configured in Rewst before deploying the Crate. To update organizational variables, follow [this guide](https://docs.rewst.help/prebuilt-automations/existing-crate-documentation/configure-organization-variables).

{% hint style="warning" %}
Ensure all required variables are correctly set before using the onboarding workflow.
{% endhint %}

CTX variables hold dynamic, user-specific data used in automation.

{% hint style="info" %}
Expand each of the categories below to see that type of CTX variable's reference table.
{% endhint %}

<details>

<summary>User information CTX variable reference</summary>



| **CTX variable**                             | **Purpose**                                                        |
| -------------------------------------------- | ------------------------------------------------------------------ |
| `CTX.first_name`                             | Stores the user's first name.                                      |
| `CTX.last_name`                              | Stores the user's last name.                                       |
| `CTX.email`                                  | The user's primary email address.                                  |
| `CTX.username`                               | The assigned username for login.                                   |
| `CTX.user_title / CTX.job_title`             | Stores the user's job title.                                       |
| `CTX.user_location / CTX.site_name`          | Defines the user's location.                                       |
| `CTX.mobile_number / CTX.phone_number`       | Stores the user's mobile phone number.                             |
| `CTX.desk_phone_number / CTX.desk_extension` | Stores the user's desk phone and extension.                        |
| `CTX.supervisor_id`                          | References the assigned supervisor.                                |
| `CTX.contact_id`                             | Stores the unique contact ID for the user.                         |
| `CTX.child_company`                          | Defines the company or department under which the user is created. |

</details>

<details>

<summary>Identity and directory information CTX variable reference</summary>



| **CTX variable**                  | **Purpose**                                                      |
| --------------------------------- | ---------------------------------------------------------------- |
| `CTX.aad_user_id`                 | Stores the Azure AD (Entra ID) user ID.                          |
| `CTX.ad_user_id`                  | Stores the On-Prem AD user ID.                                   |
| `CTX.email_domain`                | Defines the email domain assigned to the user.                   |
| `CTX.group_lists_with_names`      | Stores assigned security/distribution groups.                    |
| `CTX.combined_user_attributes`    | Merges attributes for both AD and Azure AD.                      |
| `CTX.preferred_adconnect_server`  | Specifies the preferred domain controller for AD Sync.           |
| `CTX.child_company`               | Identifies the sub-company under which the user is created.      |
| `CTX.preferred_identity_provider` | Determines the primary directory (On-Prem AD, Azure AD, Hybrid). |

</details>

<details>

<summary>Ticketing and documentation CTX variable reference</summary>



| **CTX variable**                     | **Purpose**                                               |
| ------------------------------------ | --------------------------------------------------------- |
| `CTX.ticket_id`                      | Tracks the ticket ID for onboarding.                      |
| `CTX.create_company_contact`         | Determines if a company contact should be created in PSA. |
| `CTX.psa_system`                     | Tracks the PSA system used for documentation.             |
| `CTX.automation_log`                 | Logs automation execution details.                        |
| `CTX.onboard_excluded_org_variables` | Filters out sensitive organizational variables from logs. |

</details>

<details>

<summary>Security and password management CTX variable reference</summary>



| **CTX variable**                | **Purpose**                                                      |
| ------------------------------- | ---------------------------------------------------------------- |
| `CTX.requested_password`        | Stores the initial password for user onboarding.                 |
| `CTX.password_storage_location` | Defines where the password is stored (PSA, ITGlue, Hudu, etc.).  |
| `CTX.require_password_change`   | Indicates if the user must change the password upon first login. |
| `CTX.prevent_password_change`   | Restricts the user from manually updating their password.        |
| `CTX.store_password_in_ticket`  | Determines whether the password should be stored as a ticket.    |

</details>

<details>

<summary>License and group management CTX variable reference</summary>



| **CTX variable**               | **Purpose**                                                 |
| ------------------------------ | ----------------------------------------------------------- |
| `CTX.sku_infos`                | Stores assigned Microsoft 365 licenses.                     |
| `CTX.m365_direct_licenses`     | Lists direct license assignments.                           |
| `CTX.m365_security_groups`     | Defines Microsoft 365 security groups assigned to the user. |
| `CTX.ad_security_groups`       | Lists on-premises AD security group assignments.            |
| `CTX.m365_distribution_groups` | Defines Microsoft 365 distribution groups assigned.         |
| `CTX.shared_mailboxes`         | Tracks shared mailbox permissions.                          |
|                                |                                                             |

</details>

Org variables define **global settings** that control how onboarding workflows operate.

{% hint style="info" %}
Expand each of the categories below to see that type of org variable's reference table.
{% endhint %}

<details>

<summary>Identity and access management org variable reference</summary>



| **ORG.VARIABLES**             | **Purpose**                                                                |
| ----------------------------- | -------------------------------------------------------------------------- |
| `default_rmm`                 | Selects the RMM platform used for automation.                              |
| `primary_identity_provider`   | Defines whether users are created in On-Prem AD, Azure AD, or Hybrid mode. |
| `preferred_domain_controller` | The hostname of the domain controller used for running PowerShell.         |
| `preferred_adconnect_server`  | The name of the server running AD Connect.                                 |
| `onprem_exchange_server`      | The name of the On-Prem Exchange Server (leave blank if not used).         |

</details>

<details>

<summary>Ticketing and documentation org variable reference</summary>



| **ORG.VARIABLES**                 | **Purpose**                                                 |
| --------------------------------- | ----------------------------------------------------------- |
| `default_psa`                     | Selects the PSA system where tickets will be created.       |
| `default_ticket_location`         | The board where Rewst-generated tickets will be placed.     |
| `default_ticket_status`           | The status used when Rewst is actively working on a ticket. |
| `ticket_status_waiting_input`     | The status when Rewst is waiting for technician input.      |
| `ticket_status_workflow_complete` | The status when the onboarding workflow is complete.        |
| `default_priority`                | The priority for Rewst-created tickets.                     |
| `send_from_address`               | The reply-to address when sending emails from Rewst.        |

</details>

<details>

<summary>Licensing and purchases org variable reference</summary>



| **ORG.VARIABLES**                         | **Purpose**                                                                                                                       |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `ms_licensing_distributor`                | <p>Selects the default Microsoft 365 license distributor (Pax8, Sherweb, etc.).<br>For ArrowSphere, set to <code>Arrow</code></p> |
| `auto_purchase_license_if_none_available` | Enables auto-purchase of Microsoft 365 licenses when unavailable.                                                                 |
|                                           |                                                                                                                                   |

</details>

<details>

<summary>Security and password management org variable reference</summary>



<table data-header-hidden><thead><tr><th width="379.567626953125">ORG.VARIABLES</th><th>Purpose</th></tr></thead><tbody><tr><td><code>store_password_in_ticket</code></td><td>Saves the password in the PSA ticket internal notes.</td></tr><tr><td><code>onboarding_password_save_location</code></td><td>Defines alternative storage - PSA, ITGlue, Hudu.</td></tr><tr><td><code>new_user_password_save_location_custom_url</code></td><td>The URL for PWPush if used for secure password sharing. Use <a href="https://us.pwpush.com">https://us.pwpush.com</a> or <a href="https://eu.pwpush.com">https://eu.pwpush.com</a> - no authorization is needed. </td></tr></tbody></table>

</details>

<details>

<summary>User onboarding and offboarding defaults org variable reference</summary>



| **ORG.VARIABLES**                     | **Purpose**                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `user_start_date_action`              | Controls whether onboarding starts immediately or waits for the specified start date.                                                                                                                                                                                                                                                                        |
| `type_for_created_new_user_ticket`    | Defines the ticket type for new user onboarding.                                                                                                                                                                                                                                                                                                             |
| `subtype_for_created_new_user_ticket` | Defines the subtype for new user onboarding tickets.                                                                                                                                                                                                                                                                                                         |
| `item_for_created_new_user_ticket`    | Defines the item for new user onboarding tickets.                                                                                                                                                                                                                                                                                                            |
| `user_name_format`                    | Defines the username format for new users.                                                                                                                                                                                                                                                                                                                   |
| `no_ad_sync`                          | Specifies if the organization has an OnPrem AD without AD Sync.                                                                                                                                                                                                                                                                                              |
| `tz_country`                          | Reduces the number of options available when selecting a time zone for delaying user onboarding. The field is generated via the \[REWST - OPT GEN] List Timezones workflow, and will either generate all time zone options or only show ones for a set country. Values must be stored as the entire country name, for example Canada, Mexico, United States. |

</details>

<details>

<summary>Miscellaneous settings org variable reference</summary>



| **ORG.VARIABLES**               | **Purpose**                                             |
| ------------------------------- | ------------------------------------------------------- |
| `preferred_phone_number_format` | Defines the preferred format for phone numbers.         |
| `m365_usage_location`           | Defines the default Microsoft 365 usage location.       |
| `new_user_approval_email`       | Specifies the email address for user approval requests. |

</details>

#### OpenText SecureCloud organizational variables

If using OpenText SecureCloud with this Crate, you'll also need to set **`primary_identity_provider`&#x20;**&#x20; to one of the two values below:

* **`secure_cloud`** if you're creating a SecureCloud user for Microsoft 365 usage
* **`secure_cloud_and_on_prem`**  if you're using SecureCloud for Microsoft 365 usage and you have Active Directory without ad sync.

To pre-populate the fields for OpenText SecureCloud in the [**User Onboarding** **form**](onboarding-form-inputs-and-workflow-process.md#form-fields-present-if-using-opentext-securecloud) unpacked with this Crate to a specific location, you can create the org variable **`secure_cloud_usage_location`** and set the location as the value.

### Recommended organizational variable configuration

If not set, your organization's default settings will be applied.

| Variable                    | Description                                                                                 |
| --------------------------- | ------------------------------------------------------------------------------------------- |
| `primary_identity_provider` | Specifies whether users are created in On-Prem AD, Azure AD, or Hybrid mode.                |
| `ms_licensing_distributor`  | Determines the license distributor for M365 purchases or whether to use the manual process. |

## Unpack the Crate

1. Navigate to **Marketplace > Crates** in the left side menu of the Rewst platform.
2.  Search for `Microsoft: User Onboarding`.



    <div align="left"><figure><img src="../../../../.gitbook/assets/image (178).png" alt=""><figcaption></figcaption></figure></div>
3. Click on the Crate to open the details page.
4. Click **Unpack Crate**, then **Continue**.
5. Click **Unpack**. Note that this is a large Crate, and the process may take a few minutes.
6. The [organization variable](../../../integrations/organization-variables.md#manually-add-a-new-organization-variable) `user_onboard_form_name` must be set  to the name of the form unpacked with the Crate.&#x20;

## Use the Crate

### Use the new user onboarding form

Once the Crate is unpacked, use the onboarding form to create new users.

1. Navigate to **Automations > Assets > Forms**.
2. Search for `[Crate] Microsoft: User Onboarding`.
3. Click **⋮ > Usages > View Direct URLs.**
4. Click on the form link for the organization where you want to create a new user.
5. Fill out the form as desired. For detailed information on all form options, see [onboarding-form-inputs-and-workflow-process.md](onboarding-form-inputs-and-workflow-process.md "mention").
6. Click **Submit**.

### &#x20;**Validate workflow execution**

1. Go to **Automations > Results**.
2. Search for `Microsoft: User Onboarding`.
3. Open the latest execution result and verify that the workflow completed successfully.
4. Review the execution logs for any failed steps or warnings. If any failures occur, refer to the troubleshooting section below.

### **Verify user creation and assignments**

| Verification step                               | Expected outcome                                                 |
| ----------------------------------------------- | ---------------------------------------------------------------- |
| **Active Directory (On-Prem AD Only / Hybrid)** | User appears in **Active Directory Users & Computers (ADUC)**.   |
| **Azure AD (Cloud / Hybrid)**                   | User is created in **Microsoft Entra ID (Azure AD)**.            |
| **Security Groups**                             | User is assigned to **the selected security groups**.            |
| **Microsoft 365 Licensing**                     | License is assigned to the user (directly or via a group).       |
| **Shared Mailbox & Permissions**                | User has "Send As" or "Send on Behalf" permissions, if selected. |

If a user does not appear in AD or Azure AD, check the **workflow execution logs**.

### **Confirm ticket and documentation updates**

| **PSA Ticket Creation**               | A new ticket is created in ConnectWise, Autotask, Halo PSA, ServiceNow, etc.. |
| ------------------------------------- | ----------------------------------------------------------------------------- |
| **Ticket Updates**                    | The ticket logs user details, group assignments, and licensing information.   |
| **External Documentation (Optional)** | User credentials are stored in ITGlue, Hudu, or Passportal, if enabled.       |

{% hint style="success" %}
If the ticket was not created or updated, verify that [PSA integration is configured correctly](https://docs.rewst.help/documentation/integrations/psa).
{% endhint %}

## **Troubleshoot the Microsoft: User Onboarding Crate**

{% hint style="success" %}
Expand each of the issues below to see its full documentation and known solution.
{% endhint %}

<details>

<summary>Issue: User not created in Azure AD</summary>



#### **Symptoms:**

* No user is found in Microsoft Entra ID (Azure AD).
* The workflow fails before provisioning the account.

#### Possible causes:

* The identity provider configuration is incorrect.
* The workflow execution failed before user creation.
* The user already exists in Azure AD.

#### Solution:

1. Check the workflow execution logs in Automations > Results for errors.
2. Search manually for the user in Azure AD to confirm if the account exists.
3. Confirm your Microsoft GDAP configuration
   1. Proper GDAP setup is crucial for automation at the MSP level, eliminating the need for separate Microsoft integrations for each customer.
   2. Refer to the [GDAP Documentation](https://www.notion.so/Draft-Microsoft-User-Onboarding-Crate-V2-1a0b56f9907180c6af66fc86a836eb5e?pvs=21) for setup guidelines and best practices.
   3. Ensure that the necessary permissions and access levels are correctly assigned to prevent provisioning failures.
4. Verify Organizational Variables:
   * `primary_identity_provider = Azure AD / Hybrid`
   * `preferred_adconnect_server` is set (for hybrid sync).

</details>

<details>

<summary>Issue: User not created in Active Directory</summary>



#### **Symptoms:**

* No user appears in Active Directory Users & Computers (ADUC).
* The workflow fails before provisioning the account.

#### **Possible causes:**

* The RMM tool has not been configured.
* The identity provider configuration is incorrect.
* The workflow execution failed before user creation.
* The user already exists in Active Directory.

#### **Solution:**

1. Check the [integration guide](https://docs.rewst.help/documentation/integrations/rmm) for the following RMMs and ensure you have completed the process:
   * Datto RMM
   * NinjaOne
   * Immybot
   * Kaseya VSA
   * Kaseya VSA X
   * N-able N-central
   * Agent Smith - Check the Documentation for [Agent Smith](https://docs.rewst.help/documentation/agent-smith)
2. Verify the workflow execution logs in **Automations > Results** for errors.
3. Search manually for the user in ADUC to confirm if the account exists.
4. Verify Organizational Variables:
   * `primary_identity_provider = On-Prem AD / Hybrid`
   * `preferred_adconnect_server` is set (for hybrid sync).

</details>

<details>

<summary>Issue: Microsoft 365 license not assigned</summary>

#### **Symptoms:**

* The user is created in Azure AD but has no assigned license.
* The license purchase request fails in Microsoft 365 Admin Center.

#### Possible causes:

* No available licenses in the tenant.
* The user was not added to the correct license group.
* License auto-purchasing is disabled.

#### **Solution:**

1. Check available licenses in the Microsoft 365 Admin Center.
2. Enable automatic license purchasing in Rewst:
   * Set `auto_purchase_license_if_none_available = 1`.
3. Confirm license assignment method:
   * `m365_license_assignment_method = direct` for direct assignment.
   * `m365_license_assignment_method = group` for group-based assignment.

If using group-based licensing, ensure the user is added to the correct M365 License Group. If using the Manual Process, Check the Manual License Purchase Process

</details>

<details>

<summary>Issue: User not added to security groups</summary>



#### **Symptoms:**

* The user appears in AD/Azure AD but is not assigned to any security groups.
* Permissions are missing due to lack of group membership.

#### Possible causes:

* The group selection was missed during onboarding.
* The group name is incorrect or does not exist in AD/Azure AD.

#### Solution:

1. Check the selected groups in the onboarding form submission.
2. Manually search for the group in Active Directory Users & Computers or Azure AD.
3. Ensure group synchronization is active (for hybrid configurations).

</details>

<details>

<summary>Issue: PSA ticket not created or updated</summary>



#### **Symptoms:**

* No onboarding ticket appears in ConnectWise, Autotask, or other PSA.
* The ticket is created but missing onboarding details.

#### Possible causes:

* PSA integration is not configured correctly.
* PSA API credentials are incorrect or expired.
* The company contact does not exist in PSA.

#### **Solution:**

1. Verify PSA integration settings in Rewst.
2. Check the workflow execution logs for API errors.
3. Manually create a test ticket in PSA to confirm integration functionality.
4. Confirm the `default_psa` is not set to be `mail_only`

</details>

<details>

<summary>Issue: Required fields in Halo preventing ticket creation or updates</summary>



#### Symptoms:

* Ticket creation or updates in Halo PSA fail unexpectedly.
* Errors appear related to missing mandatory fields when attempting to create or update a ticket.
* The default Halo PSA ruleset causes validation failures.

#### Possible causes:

* Mandatory fields are enabled in Halo PSA, preventing Rewst from creating or updating tickets.
* The default Halo PSA ruleset requires additional fields not configured in the workflow.
* The \[REWST - TASK] PSA-Halo PSA: Create Ticket action does not include the required mandatory field values.

#### **S**olution:

1. Remove mandatory fields from your PSA to allow for seamless automation.
2. Unsync your PSA-Halo Create Ticket Crate to manually modify field requirements:
   * Navigate to \[REWST - TASK] PSA-Halo PSA: Create Ticket.
   * In the halo\_create\_ticket action, ensure all mandatory fields have valid values.
3. Understand the impact of unsyncing a Crate:
   * By default, all Crates are synced when unpacked.
   * Unsyncing a Crate allows customization but requires manual maintenance.
   * We recommend using synced Crates until you’ve completed Rewst training in Cluck University.

</details>

<details>

<summary>Issue: Password not stored in documentation system</summary>



#### **Symptoms:**

* The password does not appear in ITGlue, Hudu, or Passportal.
* The PSA ticket is missing the temporary password.

#### **Possible causes:**

* Documentation integration is not enabled.
* API credentials for ITGlue/Hudu/Passportal are incorrect or expired.

#### **Solution:**

1. Enable password storage by setting `store_user_credentials_in_external_doc = 1`.
2. Check the API integration settings in Rewst.
3. Test manual credential storage to confirm integration is working.

</details>

<details>

<summary>Issue: Delayed user creation not working</summary>



#### Symptoms:

* The user is created immediately, despite a future start date.
* The workflow does not pause as expected.

#### Possible causes:

* The Start Date field was missing or not populated.
* The `allow_scheduled_user_creation` setting is disabled.
* The workflow scheduler is not running correctly.

#### Solution:

1. Ensure that the **Start Date** field is enabled in the onboarding form.
2. Set `allow_scheduled_user_creation = 1` in organizational variables.
3. Check scheduled automations in Rewst to verify execution timing.

</details>



## **Onboarding Workflows, triggers, forms, scripts, and templates**

This section provides a detailed list of all workflows, triggers, forms, scripts, and templates included in the Microsoft: User Onboarding Crate.

<details>

<summary>Workflows</summary>

The following workflows are included in this Crate:

* **User Provisioning & Automation**
  * \[REWST - PROC] Microsoft: User Onboarding
  * \[REWST - PROC] User: Change Password
  * \[REWST - PROCESS] PSA: Update Ticket
  * \[REWST - PROCESS] PSA: Create Ticket
* **Identity and group management**
  * \[REWST - TASK] User Onboarding: Create User
  * \[REWST - TASK] User Onboarding: Create Azure AD User
  * \[REWST - TASK] User Onboarding: Create On-Prem User
  * \[REWST - TASK] On-Prem User To Copy Groups
  * \[REWST - TASK] M365 User To Copy Groups
  * \[REWST - TASK] On-Prem: Add User To Groups
  * \[REWST - TASK] M365: Add User to Security Group
  * \[REWST - TASK] M365: Add User to Distribution/Mail-Enabled Group
  * \[REWST - TASK] M365 Licensing: Assign License to Graph User
  * \[REWST - TASK] M365 Licensing: Manual License
  * \[REWST - TASK] M365 Licensing: Add User to License Group
  * \[REWST - TASK] OnPrem: Add To Global Group
* **Password and security**
  * \[REWST - TASK] User: Format Phone Number
  * \[REWST - TASK] Format Phone Numbers and Custom Display Name
  * \[REWST - TASK] M365: Change User Password
  * \[REWST - TASK] Rewst: Password Generator
  * \[REWST - TASK] Friendly: Password Generator
  * \[REWST - TASK] Send User Password
  * \[REWST - TASK] Email User Password To Supervisor
  * \[REWST - TASK] Validate Required Fields
  * \[REWST - TASK] Approval: Require Pre-Process
* **Shared mailboxes and communication**
  * \[REWST - TASK] M365: List Shared Mailboxes
  * \[REWST - TASK] M365: Add Shared Mailbox
  * \[REWST - TASK] List On-Prem Exchange Shared Mailboxes
  * \[REWST - TASK] M365: Send Mail as Impersonated User
* **Automation and system execution**
  * \[REWST - TASK] Run Powershell via RMM
  * \[REWST - TASK] Automate: Run Powershell
  * \[REWST - TASK] NAble: Run Powershell
  * \[REWST - TASK] NinjaOne: Run Powershell
  * \[REWST - TASK] Kaseya VSA: Run Powershell
  * \[REWST - TASK] Kaseya VSA X: Run Powershell
  * \[REWST - TASK] Datto RMM: Run Powershell
  * \[REWST - TASK] CW Control: Run Powershell
  * \[REWST - TASK] Immybot: Run Powershell
  * \[REWST - TASK] Agent Smith: Run Powershell
  * \[REWST - TASK] Powershell Webhooks
  * \[REWST - TASK] Run AD Sync/Entra Cloud Sync

</details>

<details>

<summary>Triggers</summary>

The following triggers initiate workflows and automation in the Crate:

* User onboarding process
  * Main Onboarding Trigger
  * M365 Trigger
* Automation and data retrieval
  * Options Trigger
  * Opt Gen
  * Pass Trigger
  * General Trigger
  * EXO Trigger
  * Options Gen

</details>

<details>

<summary>Forms</summary>

The following forms are included:

* \[Crate] Microsoft: User Onboarding
  * Used to submit new user onboarding requests.
  * Dynamically displays fields based on selected identity provider and advanced options.

</details>

<details>

<summary>Scripts</summary>

The following scripts automate key functions in the onboarding workflow:

* Active Directory & Entra ID (Azure AD) Management
  * \[REWST - TASK] Change On-Prem AD User Password
  * \[REWST - TASK] M365: Get Group Details
  * \[REWST - TASK] M365: Get User
  * \[REWST - TASK] M365: Start Entra Cloud Sync
  * \[REWST - TASK] On-Prem: Add User To Groups
  * \[REWST - TASK] List On-Prem Exchange Shared Mailboxes
* Password Management & Validation
  * \[REWST - TASK] Validate User Existence
  * \[REWST - TASK] Get User UPN
  * \[REWST - TASK] Generate Username
* Licensing & Group Management
  * \[REWST - TASK] M365 Licensing: Pax 8: Purchase License
  * \[REWST - TASK] M365 Licensing: Sherweb: Purchase License
  * \[REWST - TASK] M365 Licensing: Ingram Micro: Purchase License
  * \[REWST - TASK] M365 Licensing: Synnex: Purchase License
  * \[REWST - TASK] M365 Licensing: MS Tier1: Purchase License
* PSA & Ticketing Automation
  * \[REWST - TASK] PSA: Upsert Contact
  * \[REWST - TASK] PSA-Kaseya BMS: Update Ticket
  * \[REWST - TASK] PSA-Freshdesk: Upsert Contact
  * \[REWST - TASK] PSA-ServiceNow: Update Ticket
  * \[REWST - TASK] PSA-CWM: Upsert Contact
  * \[REWST - TASK] PSA-Halo PSA: Create Ticket
  * \[REWST - TASK] PSA-KaseyaBMS: Upsert Contact

</details>

<details>

<summary>Templates</summary>

The following templates define approval processes, ticket summaries, and structured outputs:

* Approval & Validation
  * \[REWST - TEMPLATE] Approval: Running Automation Requires Approval (HTML)
  * \[REWST - TEMPLATE] Approval: Running Automation Requires Approval (Markdown)
  * \[REWST - TEMPLATE] Approval: Running User Exists in Approval List (HTML)
  * \[REWST - TEMPLATE] Approval: Running User Exists in Approval List (Markdown)
* Onboarding Ticket Summaries
  * \[REWST - TEMPLATE] Onboarding: Dynamic New User Ticket Summary - HTML
  * \[REWST - TEMPLATE] Onboarding: Dynamic New User Ticket Summary (Markdown)
  * \[Rewst Master] Onboarding: Dynamic New User Ticket Summary
* PowerShell & Active Directory Utilities
  * \[REWST - TEMPLATE] Powershell: Get All Unique Values for AD Attribute
  * \[REWST - TEMPLATE] PAX8 MS Mapping
  * \[REWST - TEMPLATE] M365 License Lookup
  * \[REWST - TEMPLATE] Licenses To Assign Last

</details>

## Migration guide: Moving from a previous onboarding Crate

{% hint style="warning" %}
If you’re using a previous version of the onboarding workflow, follow these migration steps below. If this is your first time using this Crate, this information isn't relevant to you.
{% endhint %}

{% content-ref url="../../migrating-between-crate-versions.md" %}
[migrating-between-crate-versions.md](../../migrating-between-crate-versions.md)
{% endcontent-ref %}

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
