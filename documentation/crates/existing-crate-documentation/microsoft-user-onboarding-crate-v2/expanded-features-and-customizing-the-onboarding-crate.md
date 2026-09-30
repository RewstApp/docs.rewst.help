# Expanded features and customizing the Onboarding Crate

## **Approval requirement for new users**

By default, the Microsoft: User Onboarding Crate provisions users immediately upon form submission. However, some organizations may require an approval process before onboarding users.

### **How the approval workflow works**

1. The user submits the onboarding form.
2. The workflow pauses execution and notifies the designated approver—IT admin, HR, or supervisor.
3. The approver receives a notification via email, PSA ticket, or within Rewst.
4. If approved, the workflow proceeds with user creation.
5. If denied, the workflow terminates without creating the user.

### **How to enable the approval workflow**

Configure the following **organizational variable** in **Rewst > Configuration > Organizational Variables**:

| `require_approval_for_new_users` | Enables the approval step before user creation.          | `0` Disabled |
| -------------------------------- | -------------------------------------------------------- | ------------ |
| `new_user_approval_email`        | Defines the email address for sending approval requests. | None         |

{% hint style="warning" %}
If approvals are enabled, ensure that designated approvers regularly check for pending requests.
{% endhint %}

## **Ticketing and documentation handling**

The Crate automatically creates and updates tickets in supported PSA platforms.

### **Automated PSA ticket creation and management**

| **Create Ticket if None Exists** | A ticket is automatically created if one is not found.            |
| -------------------------------- | ----------------------------------------------------------------- |
| **Update Existing Ticket**       | If a ticket exists, it is updated with onboarding progress.       |
| **Track Onboarding Status**      | The ticket logs user details, licensing, and provisioning status. |
| **Define Ticket Prioritization** | Rewst assigns default priorities, work roles, and tech IDs.       |

### **Ticketing organizational variables**

| `default_psa`                     | Selects the PSA where tickets will be created.                   |
| --------------------------------- | ---------------------------------------------------------------- |
| `default_ticket_location`         | Defines the board for Rewst-created tickets.                     |
| `default_ticket_status`           | The ticket status when Rewst is actively processing.             |
| `ticket_status_waiting_input`     | The status when waiting for manual input-e.g., license purchase. |
| `ticket_status_workflow_complete` | The status when the onboarding workflow is completed.            |
| `default_priority`                | Assigns the default priority for onboarding tickets.             |
| `send_from_address`               | The reply-to address for emails sent from Rewst.                 |

{% hint style="warning" %}
Ensure that PSA permissions allow Rewst to create and modify tickets.
{% endhint %}

## **Delayed user creation**

The onboarding process can be scheduled for a future date instead of immediate provisioning.

{% hint style="info" %}
Limit: The account creation date cannot be more than 30 days in the future. A request scheduled beyond that limit will fail, and a note explaining the failure is added to the PSA ticket.
{% endhint %}

### **How it works**

1. Set `user_start_date_action` to `pause_workflow` in Configuration > Organizational Variables.
2. On the onboarding form, under Customize Advanced Options > Advanced - Delayed Creation, check **Enable Delay User Creation**.
3. Set the **Account Creation Date**, **Account Creation Time**, and **Timezone**.
4. On submission the workflow computes the correct UTC instant from those three fields, pauses until that time, then resumes and creates the user. If no timezone is selected, UTC is assumed.

### **Enable the feature**

Delayed creation is controlled by the organizational variable `user_start_date_action`:

| Value                     | Behavior                                                        |
| ------------------------- | --------------------------------------------------------------- |
| `document_only` - default | The start date is recorded on the ticket only. No delay occurs. |
| `pause_workflow`          | The workflow pauses and creates the user at the scheduled time. |

Because the default is `document_only`, delayed creation is off until an administrator sets this variable. The delayed-creation options do not appear on the onboarding form unless `user_start_date_action` is set to `pause_workflow`.

## **Multi-Factor Authentication enrollment**

The Crate does not enforce MFA directly but supports Microsoft Entra ID (Azure AD) conditional access policies.

### **Recommended MFA configuration**

1. Enable Azure AD Security Defaults to enforce MFA at the tenant level.
2. Use Conditional Access Policies to require MFA for new users.
3. Set up self-service MFA registration to allow users to enroll their devices.

{% hint style="warning" %}
Ensure that MFA policies align with company security requirements before enforcing them.
{% endhint %}

## **Security and password management**

The Crate includes flexible password handling options based on security policies.

<details>

<summary>Password handling options</summary>

| **Setting**                                | **Description**                                                  | **Default value** |
| ------------------------------------------ | ---------------------------------------------------------------- | ----------------- |
| **Require Password Change on First Login** | Forces the user to reset their password at first login.          | ✅ Enabled         |
| **Restrict User from Changing Password**   | Prevents users from modifying their own passwords.               | ❌ Disabled        |
| **Set Password to Never Expire**           | Ensures the user’s password does not require renewal.            | ❌ Disabled        |
| **Auto-Store Password in Documentation**   | Saves the password securely in external documentation platforms. | ✅ Enabled         |
| **Send Password via SMS or Email**         | Sends credentials to the manager via email or SMS.               | ✅ Enabled         |

</details>

<details>

<summary>Password storage locations</summary>

Rewst can store temporary passwords in the following locations:

* PSA internal ticket notes
* ITGlue
* Hudu
* Passportal
* PWPush, if configured

To configure where passwords are stored, update the following variables:

| **Variable name**                   | **Purpose**                                          | **Default value** |
| ----------------------------------- | ---------------------------------------------------- | ----------------- |
| `store_password_in_ticket`          | Saves the password in the PSA ticket internal notes. | `1` Enabled       |
| `onboarding_password_save_location` | Defines alternative storage (PSA, ITGlue, Hudu).     | None              |
| `pwpush_url`                        | The URL for PWPush if being used.                    | None              |

</details>

## **Licensing and group assignments**

The Crate supports multiple licensing and group assignment methods.

### **License assignment options**

| **Direct Assignment**        | The user is assigned an M365 license individually.          |
| ---------------------------- | ----------------------------------------------------------- |
| **License Group Membership** | The user is added to an M365 license group.                 |
| **Auto-Purchase Licenses**   | If no licenses are available, Rewst can purchase new seats. |

To enable license auto-purchasing, configure the following setting:

| **Variable name**                         | **Purpose**                                | **Default value** |
| ----------------------------------------- | ------------------------------------------ | ----------------- |
| `auto_purchase_license_if_none_available` | Enables license auto-purchase when needed. | ✅ Enabled         |

## Manual license purchase process

### **When is the manual license purchase process triggered?**

This process is triggered under the following conditions:

* The organization is not mapped to a distributor such as Pax8, Sherweb, Ingram Micro, etc., preventing automatic license purchasing.
* The user has selected manual purchase in the onboarding form or the workflow logic determines that auto-purchase is unavailable.
* There are no available licenses, and auto-purchasing is disabled in Rewst organizational settings.

### **Process flow**

{% hint style="info" %}
Expand each of the steps below to see the related part of the process flow.
{% endhint %}

<details>

<summary>1. Adding a note to the PSA ticket</summary>

* When a manual license purchase is required, the workflow adds an internal note to the PSA ticket.
* This note informs the technician that a license is needed and provides action URLs to confirm purchase or reject purchase.
*   The message added to the ticket is as follows:

    > `The organization Name requires a license and either you have selected to purchase the license manually or the organization is not mapped with the distributor.`
    >
    > `Please purchase the requested license and once complete, click the URL below. Note the window will close automatically:`
    >
    > **`Confirm License Purchase: Link`**
    >
    > `If you don't want to purchase the license right now, click the URL below. You will need to manually apply a license to the user after the workflow is complete:`
    >
    > \*\*`Reject License Purchase:** **Link**`
* The workflow pauses execution until one of these actions is taken.

</details>

<details>

<summary>2. Technician decision : Confirm or reject license purchase</summary>

The technician has two options:

**Option 1: Confirm license purchase**

* The technician clicks the **Confirm License Purchase** URL.
* This triggers a webhook **response** that allows the workflow to continue.
* The following actions occur:
  * A **ticket note is added** stating that the license has been purchased manually.
  * The workflow resumes and attempts to **assign the purchased license to the user**.
  * The workflow continues to the **next step in the onboarding process**.

**Option 2: Reject license purchase**

* The technician clicks the **Reject License Purchase** URL.
* This triggers a **webhook response** indicating that the purchase was not completed.
* The following actions occur:
  * A ticket note is added stating that the license was not purchased.
  * The workflow continues without assigning a license. The technician must assign the license manually at a later stage.

</details>

<details>

<summary>3. Handling timeouts: No action taken</summary>

* If **neither Confirm** nor **Reject** is selected within 24 hours, the workflow automatically adds a timeout note to the PSA ticket.
*   The message added to the ticket is:

    `No option was chosen to purchase the license, and the request has now timed out.`
* The workflow proceeds without assigning a license, requiring manual intervention later.

</details>

## **Workflow breakdown**

| Add PSA Note                         | Adds a note to the PSA ticket requesting manual license purchase confirmation. | Technician receives instructions to confirm or reject the purchase.                       |
| ------------------------------------ | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------- |
| Technician Confirms License Purchase | Clicks **Confirm License Purchase** link.                                      | The workflow assigns the license and proceeds with onboarding.                            |
| Technician Rejects License Purchase  | Clicks **Reject License Purchase** link.                                       | The workflow proceeds **without assigning a license**, requiring manual assignment later. |
| Technician Takes No Action           | No response within **24 hours**.                                               | The workflow adds a timeout note and proceeds without assigning a license.                |

## **Organizational variables affecting this workflow**

| `ms_licensing_distributor`                | Defines the distributor for license purchases (if auto-purchasing is enabled).                                         |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `auto_purchase_license_if_none_available` | Enables auto-purchase of licenses when none are available.                                                             |
| `default_psa`                             | Defines which PSA system to log ticket updates in.                                                                     |
| `default_ticket_status`                   | Defines the PSA ticket status when waiting for technician input.                                                       |
| `ticket_status_waiting_input`             | The status set in PSA when awaiting technician action.                                                                 |
| `ad_list_enabled_users_only`              | Controls filtering of disabled users; defaults to true with safe boolean conversion, with false reverting to all users |

## **Final notes**

* The manual license process ensures that a technician has full control over licensing decisions when auto-purchasing is unavailable.
* Clear ticketing updates and automation logs ensure visibility into whether a license was purchased, rejected, or timed out.
* If manual licensing becomes a frequent issue, consider updating organizational variables to enable auto-purchasing where possible.

## **User name format and offboarding defaults**

### **Username format options**

The Crate allows you to standardize username formats for new accounts.

| First Initial + Last Name | `jdoe`    |
| ------------------------- | --------- |
| First Name + Last Name    | `johndoe` |
| First Name + Last Initial | `johnd`   |

Set the username format using the following variable:

| `username_format` | Defines the standard username structure. | `firstinitiallastname` |
| ----------------- | ---------------------------------------- | ---------------------- |

### **Offboarding defaults**

The same workflow principles apply to user offboarding, ensuring proper deactivation and account cleanup.

| `offboarding_deactivate_user` | Disables the user account during offboarding. | ✅ Enabled |
| ----------------------------- | --------------------------------------------- | --------- |
| `offboarding_remove_groups`   | Removes the user from security groups.        | ✅ Enabled |

{% hint style="warning" %}
Offboarding settings should be reviewed periodically to ensure compliance with company policies.
{% endhint %}
