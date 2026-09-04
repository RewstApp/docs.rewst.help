---
description: >-
  Explore what new changes the Rewst developer team has deployed in the last
  week. This can be anything from new features, new Crates, bug fixes, or QoL
  changes.
---

# 2026 Dev updates

{% hint style="info" %}
As of 2026, our Dev updates now include our Crate Marketplace updates in the same document. Click the **RSS** button at the top of this page to subscribe to all Dev updates, or view older [Dev](./) and [Marketplace ](../marketplace-updates/)updates in the Updates section of this site's navigation tree.
{% endhint %}

{% updates format="numeric" %}
{% update date="2026-09-04" %}
## 💻 September 4, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Check back next week!**

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Fixed App Builder exports to include templates referenced in page HTML, preventing broken template references when apps are imported.
* **Integrations**
  * Fixed an issue where adding the SentinelOne “List RBAC Roles” action could crash the workflow canvas.
  * Fixed an issue where the Get Graph Users action could return incomplete results for tenants with large numbers of users.
  * Fixed an issue where ConnectWise pods could fail to find the correct Rewst workflow when ticket numbers overlapped across customers.
* **RoboRewsty**
  * Improved RoboRewsty publishing to report actual save failures instead of incorrectly claiming a workflow was published successfully.
  * Improved RoboRewsty feedback so longer comments are saved successfully and submission errors are clearly surfaced to users.
* **Workflows**
  * Fixed precision loss for large numeric values in integer and array action inputs, preserving long identifiers exactly.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Include M365 Copilot SKU in license lookup; stop retry loops on failed purchases
    * Add support for M365 Copilot for Business SKU in license lookup template&#x20;
    * Rewst's AI PSA Analyzer
      * Wire pipeline end-to-end; include\_custom\_automations flows via Bedrock webhook -> CTX -> subworkflow prompt flag&#x20;
  * [Rewst's AI PSA Analyzer](../../documentation/crates/existing-crate-documentation/rewsts-ai-psa-analyzer-crate.md)
    * Improve sub\_id matching: prefix and active filter, then word-overlap scoring to select best subscription
    * Fix Jinja to trim extra space in product name to match Pax8
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Align override trigger settings across regions; remove mismatched overrides to fix sync errors (105726)

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* Engine Improvements Rollout

</details>


{% endupdate %}

{% update date="2026-08-28" %}
## 💻 August 28, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Improved Custom Integration creation options with clearer guidance on choosing between OpenAPI and manual setup.
  * Added a new ConnectWise ASIO List Computers v2 action option for retrieving endpoint choices from the v2 API.
* **Workflows**
  * New workflow engine rollout - synced crates
  * Restored iframe embed code copying for Form Triggers in the new Workflow Canvas.
  * Improved the Transition Settings panel to show more Data Aliases when screen space is available.
  * Added telemetry to detect and measure intermittent connecting-line render failures in the new Workflow Builder.
  * Restored quick links for opening referenced templates and scripts directly from action parameters in the new Workflow Builder.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Forms**
  * Fixed the Form Builder org context picker to display organization names instead of raw IDs for saved selections.
* **Integrations**
  * Fixed OneDrive uploads failing after successful binary file transfers due to UTF-8 response parsing errors.
  * Fixed fallback icons for Custom Integration actions displaying incorrectly on the workflow canvas.
  * Fixed Core HTTP Request handling so valid file attachments could be uploaded successfully.
  * Fixed Core and Rewst integrations to reliably install and display correctly for newly created organizations.
  * Fixed the NinjaOne List Tickets action to return all paginated ticket results instead of stopping at 50.
  * Improved the Google Workspace List Users action to work without additional configuration by defaulting to the current customer.
  * Improved ScreenConnect script execution to surface clear, actionable errors instead of generic failure messages.
  * Fixed ConnectWise ScreenConnect credential validation so authorization tests and workflow actions use the currently saved credentials.
* **Permissions**
  * Fixed Member role access to installed custom integrations when configuring trigger overrides.
* **RoboRewsty**
  * Improved RoboRewsty workflow editing to validate builds correctly and add workflow notes successfully on the first attempt.
  * Improved RoboRewsty’s usage dial to accurately show how much of a conversation remains before reaching its limit.
  * Fixed RoboRewsty approval prompts failing to appear during multi-step workflow builds.
  * Fixed RoboRewsty to keep the latest system context and custom instructions across turns and conversation compaction.
* **Workflows**
  * Fixed workflow cloning to preserve trigger pack overrides so cloned multitenancy triggers continue working across managed organizations.
* **Crates**
  * [Clean up Global Address List from Disabled Users](../../documentation/crates/existing-crate-documentation/clean-up-global-address-list-from-disabled-users-crate.md)
    * \[ROC] EXO: Hide User from GAL subworkflow: Replaced noop on failure path with `core.fail` so failures surface to parent workflow
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Updated `Product_Display_Name` for GUID a6d18b68-a67e-4cbd-ba00-8744bc468faa to `Microsoft 365 Business Premium with Copilot`
    * Corrected subscription field mappings and types to match API, preventing silent purchase failures and retry loops
    * Fixed the Kaseya BMS Upsert Contact workflow to correctly send phone numbers
  * [Use AI to Suggest Responses to New Tickets](../../documentation/crates/existing-crate-documentation/use-ai-to-suggest-responses-to-new-tickets-crate.md)
    * Fixed empty AI-generated notes from Anthropic thinking blocks and added safeguard to block empty posts

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* Engine Improvements Rollout

</details>


{% endupdate %}

{% update date="2026-08-21" %}
## 💻 August 21, 2026 - Dev update



<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Simplified Custom Integration setup by making custom icons optional and automatically applying a default icon when one isn’t provided.
  * Updated Azure OpenAI setup instructions to warn that deployment names cannot contain periods and should use hyphens instead.
* **Roborewsty**
  * Improved RoboRewsty usage limits by including sub-agent token usage in conversation spend and cost calculations.
  * Improved RoboRewsty reliability by preventing oversized tool results from exceeding context limits and guiding agents to use filtering, pagination, or narrower requests instead.
  * Improved RoboRewsty efficiency by improving prompt caching so large tool results aren’t repeatedly reprocessed during the same turn.
* **Workflows**
  * Improved how existing workflows open in the new builder by preserving their original node positioning instead of automatically rearranging the canvas.
  * Simplified adding trigger integration overrides by keeping users on the override list instead of automatically opening the configuration screen.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Updated the SonicWall NSM “Get License for Device” action to use the new supported device license API endpoint, restoring successful license lookups.
  * Fixed a Custom Integrations issue that could crash the workflow builder after an action’s path parameter was changed or removed.
* **Permissions**
  * Fixed a permissions issue that allowed users with view-only custom roles to execute workflows from the Workflow Builder.
* **Workflows**
  * Fixed an issue in the new canvas where removing an entry from a multi-entry field could silently clear the values of entries below it.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/automations/kits/microsoft-onboarding-solution-kit.md)
    * Replaced `ad-hoc start_date` with `account_creation_date` + preset `account_creation_time` + `creation_date_timezone`; fixed browser-locale bug and UndefinedError; safe fallback to "now".&#x20;
    * Added defaults for `account_creation_date` and `account_creation_time` to prevent failures on empty input.&#x20;
    * Added support for generating a friendly password with complexity. To enable this, both `ORG.VARIABLES.friendly_password` and `ORG.VARIABLES.use_friendly_password_with_complexity` must be set to `true`. If only `ORG.VARIABLES.friendly_password` is true, the standard non-complex friendly password will be used.
    * \[REWST - TASK] M365: Purchase Licenses subworkflow
      * Added Synnex AU support — new list\_subs task and distributor transition—  and corrected TD Synnex StreamOne Ion purchase path; adjusted transition order in `choose_disti`.
  * [Document BitLocker Information](../../documentation/crates/existing-crate-documentation/document-bitlocker-information-crate.md)
    * Hardened trigger variable by using `ORG.VARIABLES.documentation_platform|d` to avoid pre-start failures when org var is missing.&#x20;
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Replaced the remove\_licenses task with a new Remove Licenses subworkflow to correctly handle users with both group-based and directly assigned licenses.



</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* [Engine Improvements Beta](https://rewst.io/go/engine-next-beta-signup)

</details>
{% endupdate %}

{% update date="2026-08-14" %}
## 💻 August 14, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **RoboRewsty**
  * RoboRewsty per-conversation usage limits
  * Clarified when RoboRewsty carried conversation context forward so users could confidently continue where they left off.
  * Added structured in-chat questions so RoboRewsty could gather required details and continue with user responses.
  * Improved RoboRewsty naming so created tasks, triggers, and transitions used clear, descriptive labels instead of placeholders.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Prevented long Custom Integration action descriptions from causing workflow save failures.
  * Restored Acronis Fetch Archives action by correcting token scoping.
  * Enabled Custom Integrations to connect reliably to APIs hosted on non-standard ports.
* **RoboRewsty**
  * Preserved existing data aliases when RoboRewsty updated individual aliases on workflow transitions.
  * Ensured RoboRewsty workflow edits continued applying correctly after starting a new chat or draft reset.
  * Corrected RoboRewsty’s synced-workflow messaging to accurately reflect that unsyncing can be reversed.
* **Workflows**
  * Protected synced workflow clone settings in the new builder from edits that would be overwritten during synchronization.
  * Restored automatic canvas centering on actions when deep-linking into the new Workflow Builder.
  * Improved webhook trigger testing to identify invalid HTTP methods instead of incorrectly reporting them as valid.
  * Fixed sub-workflow usage navigation so the workflow list table updates correctly when switching between workflows.
  * Fixed Input Configuration checkbox changes so Required and Multiline settings persist correctly.
* **Crates**
  * Add Rewst Form Link to New User Request Tickets
    * Removed deprecated crates from the crate marketplace&#x20;
  * Microsoft: User Onboarding
    * Added time-of-day selection and UTC computation for Account Creation Date; backward compatible&#x20;
    * Prevent false-positive 2000 rollups: adjusted logging for Ingram license purchase and "already in group" cases&#x20;
    * Fixed On-Prem with Sync to find Entra ID users when SAM and UPN differ&#x20;
    * Fixed "with items" variable causing license-group purchases to fail&#x20;
  * Microsoft: User Offboarding
    * Split date/time into date + preset time + timezone; compute correct UTC instant and preserve legacy var&#x20;
  * Export PSA Ticket Overview to CSV
    * Limited trigger to parent organization only&#x20;
  * Just-In-Time Admin Access
    * Added retry loop for M365 user creation after immediate delete/recreate&#x20;
  * PSA: Update Ticket with New User Onboard Form Links
    * Don't post form links for unselected orgs; renamed crates to include "Form Links"&#x20;
  * Agent Smith: Device Provisioning \[Install First]
    * Updated ConnectWise Asio actions to use renamed "companies" resource type
  * CIPP: Alert Triage
    * Added normalization for payload\[] shape and updated gate check to avoid premature filtering&#x20;

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* [Engine Improvements Beta](https://rewst.io/go/engine-next-beta-signup)

</details>


{% endupdate %}

{% update date="2026-08-07" %}
## 💻 August 7, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Added filtering to the password generator action to reduce the chance of creating passwords containing potentially offensive or sensitive terms.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Forms**
  * Prevented duplicate form submissions from creating multiple workflow executions by gating submissions while requests are in flight.
* **Integrations**
  * Fixed the N-sight List Servers action so it correctly retrieves servers for the selected site.
  * Fixed automatic OAuth 2.0 token refreshes for custom integrations so workflows can continue running after access tokens expire.
* **RoboRewsty**
  * Fixed an edge issue where RoboRewsty could disconnect workflow steps when making small edits to the connection between them.
  * Fixed RoboRewsty workflow link updates to preserve existing data aliases when only one alias is changed.
* **Crates**
  * [Google: User Onboarding](../../documentation/crates/existing-crate-documentation/google-user-onboarding-crate.md)
    * Updated GWS Remove Mobile Devices task to use the correct DELETE method
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added missing Microsoft Defender Suite for Business Premium SKU to the M365 License Lookup&#x20;
    * Correctly copies Office Location and Company Name from the selected reference user when using Copy User Attributes&#x20;
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Error now shows in ticket when a ConnectWise Manage contact fails to disable because it is set as a primary point of contact&#x20;
  * [Sync AzureAD Account Information with ConnectWise PSA Contacts (v3)](../../documentation/crates/existing-crate-documentation/sync-azuread-account-information-with-connectwise-psa-contacts-v3-crate.md)
    * Fixed case-sensitive email matching that skipped contacts when Graph and PSA email casing differed&#x20;

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* [Engine Improvements Beta](https://rewst.io/go/engine-next-beta-signup)
* RoboRewsty per-conversation usage limits

</details>


{% endupdate %}

{% update date="2026-07-31" %}
## 💻 July 31, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Added a save check that prevents overwriting a newer version of a workflow
  * Added the selected trigger to the workflow URL so that shared and bookmarked links open with the trigger in context

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed Pax8 list actions, such as List Products, to return all assets by properly handling paginated responses
  * Fixed the Ingram Micro Cloud Marketplace Get Report action, which failed when a report ID was provided
* **RoboRewsty**
  * Fixed RoboRewsty-generated ConnectWise PSA service ticket tasks crashing the parameter editor in the new Workflow Builder Canvas
* **Workflows**
  * Fixed boolean values in action query parameters not displaying in the key/value pairs UI when loading an action in the new Workflow Builder Canvas
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added missing params to the Microsoft Tier 1 Purchase License subworkflow&#x20;
    * Updated `get_datto_devices` to use `dc_filter_id` when available
    * Removed placeholder text from the `device_id default`
    * Added Business Premium/Standard/Basic with Co-Pilot entries to license lookup
    * Added Microsoft Defender for Office 365 F1 to license lookup
    * Reordered transitions to fix Synnex StreamOne path execution
    * Increased device query retry delay to 10s in Agent Smith workflows
    * Fixed rehired ConnectWise contacts remaining inactive during onboarding
  * [AI Ticket Categorization](../../documentation/crates/existing-crate-documentation/openai-ticket-categorisation-setup.md)
    * Added validation and fallback for invalid AI-generated ticket type/subtype/item combos
  * [Just-In-Time Admin Access](../../documentation/crates/existing-crate-documentation/just-in-time-admin-access-crate.md)
    * Added failure ticket notes, M365 account cleanup, and technician email notifications
    * Added Microsoft Graph integration override to Always Pass trigger for TAP policy options via GDAP&#x20;
    * Updated SuperOps to show selected customer tickets correctly
  * [Add Client to Rewst](../../documentation/crates/existing-crate-documentation/add-client-to-rewst-setup.md)
    * Set `cw_asio_company_id` field resource to Company&#x20;
    * Fixed whitespace control in `create_general_org_var` task value at crate source
  * [Alert on Expiring App Reg Secrets](../../documentation/crates/existing-crate-documentation/alert-on-expiring-app-reg-certificates-crate.md)
    * Now uses ORG.VARIABLES.psa\_default\_ticket\_status for default ticket status
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Added Microsoft User Attributes To Copy field to Configure Org Var form

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* RoboRewsty Conversation Handoff

</details>
{% endupdate %}

{% update date="2026-07-24" %}
## 💻 July 24, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Check back next week!**

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **RoboRewsty**
  * Prevented workflow changes from being lost when users and RoboRewsty edited the same workflow at the same time.
  * Improved RoboRewsty reliability to prevent conversations from getting stuck during summarization.
  * Prevented RoboRewsty from editing synchronized workflows and guided users to unsync or clone them first.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* Engine Improvements Beta

</details>
{% endupdate %}

{% update date="2026-07-17" %}
## 💻 July 17, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **RoboRewsty**
  * Improved RoboRewsty’s “Start fresh” experience so conversation summaries now carry over correctly.
  * Added one-click RoboRewsty analysis for failed workflows, with suggested fixes that can be reviewed and applied directly to the canvas.
* **Workflows**
  * Made it easier to troubleshoot workflow runs in the new workflow canvas by letting Ctrl+F or Cmd+F search all execution data, including collapsed details.
  * Improved trigger and action field selectors to display selected field names instead of raw IDs.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Improved custom domain reliability by providing more accurate status reporting and reducing unnecessary certificate retry attempts.
  * Fixed an issue that could prevent App Builder apps from cloning successfully between organizations.
* **Forms**
  * Fixed an issue that prevented integration-based dropdowns from loading options in Rewst forms.
* **General**
  * Improved database performance for looking up referenced objects.
* **Integrations**
  * Fixed the Google Workspace **List Group Members** action to return all group members by properly handling paginated results.
  * Fixed an issue that could cause the Microsoft Cloud Bundle page to crash when loading.
* **Crates**
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Restructured Remove Employee ID to add an on-prem branch; Azure users use Graph PATCH, AD Sync clears employeeID via RMM; parent now passes `on_prem_id` and `idp_config`
    * Updated gates and added UPN fallback mappings to unblock steps when only on-prem identifier is provided - Hybrid AD Sync
  * [Dropsuite: Backup Monitoring](../../documentation/crates/existing-crate-documentation/dropsuite-backup-monitoring-crate.md)
    * Removed duplicate triggers
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added resolution note parameter and handling logic

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* Engine Improvements Beta

</details>
{% endupdate %}

{% update date="2026-07-10" %}
## 💻 July 10, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Ubiquity Network - [documentation](../../documentation/integrations/integration-guides/ubiquiti-network-api-integration.md)
  * Ubiquity Protect - [documentation](../../documentation/integrations/integration-guides/ubiquiti-protect-api-integration.md)
  * Improved Cisco Meraki API Request errors by displaying detailed error messages returned by the Meraki API.
* **Organizations**
  * Improved organization restoration with a dedicated Restore button, confirmation prompt, and automatic list refresh.
* **RoboRewsty**
  * Improved RoboRewsty performance to reduce slowdowns during long workflow analysis sessions.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed Google Workspace integration overrides so workflows run against the correctly mapped child organization integration.
* **RoboRewsty**
  * Prevented RoboRewsty from resuming chats with stale workflow context when switching between workflows, ensuring edits stay scoped to the active workflow.
  * Fixed individual Jinja filter documentation responses so RoboRewsty and other consumers receive complete names, descriptions, signatures, and parameter details.
* **Workflows**
  * Fixed trigger activation failures in the new canvas by preserving default parameters required by Autotask PSA and other integration triggers.
* **Crates**
  * [Just-In-Time Admin Access](../../documentation/crates/existing-crate-documentation/just-in-time-admin-access-crate.md)
    * Safely ignore misnamed Traveling Employee CA policies to prevent job failures
    * Fixed hardcoded user reference; now uses form submitter
    * Better handling of Temporary Access Pass lifetime policy limits
    * Correctly capture Temporary Access Pass value after creation
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added customizable approval confirmation email templates - title, subject, logo, styles, button, footer
    * Hardened license lookup publishes; surface missing license as `purchase_error`
    * Optional device\_id input to override default domain controller for on‑prem actions
    * Added Azure and SuperOps integration overrides to Users: List users template
    * Added retry logic to Purchase Licenses for concurrent runs
    * Updated affected workflows to latest M365 License Lookup template
    * Added conditional `m365_user_to_copy` for Hybrid No Sync; require both when visible
  * [Sync AzureAD Account Information with ConnectWise PSA Contacts (v3)](../../documentation/crates/existing-crate-documentation/sync-azuread-account-information-with-connectwise-psa-contacts-v3-crate.md)
    * Added extension param and improved phone-number format handling in Jinja (95430)
    * Fixed mobile number mapping; pass correct data
  * [Compromised User Response](../../documentation/crates/existing-crate-documentation/compromised-user-response-crate.md)
    * Fixed notification wrapper/subworkflow - flatten targets, populate body, gate impersonation, set mail fields
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Fallback to on\_prem\_user.userPrincipalName when azure\_user.id is empty for Exchange offboarding
    * Accept on\_prem\_user in validate\_vars and include remove\_mobile\_devices action
    * Correctly save/use Offboarding Ticket SubType org variable
  * [Report on Disabled M365 Users with Licenses](../../documentation/crates/existing-crate-documentation/report-on-disabled-m365-users-with-licenses-crate.md)
    * Fixed first-run webhook link creation; include webhook trigger ID
  * [Google: User Offboarding](../../documentation/crates/existing-crate-documentation/google-user-offboarding-crate.md)
    * Existing Ticket field displays consistently across organizations
  * [Alert on Expiring App Reg Certificates](../../documentation/crates/existing-crate-documentation/alert-on-expiring-app-reg-certificates-crate.md)
    * Implemented pagination so all registrations are evaluated
  * [AI Ticket Categorization](../../documentation/crates/existing-crate-documentation/openai-ticket-categorisation-setup.md)
    * Striped markdown/code fences before JSON parsing to avoid JSONDecodeError
  * \[Deprecated] Rewst: User Onboarding
    * Removed whitespace generated by `CTX.contact_email`

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Early Access](https://rewst.io/earlyaccess)
* Engine Improvements Beta

</details>
{% endupdate %}

{% update date="2026-06-19" %}
## 💻 June 19, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Check back next week!**

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Restored the ability to delete components when editing cloned apps in App Builder.
* **RoboRewsty**
  * Improved RoboRewsty performance for large requests to prevent long delays and failed responses.
  * Preserved manually deleted workflow connections when making additional RoboRewsty updates.
  * Fixed an issue that could cause RoboRewsty conversations to become unusable after compacting long conversations.
  * Prevented RoboRewsty from overwriting existing workflow configuration when adding or updating variables and parameters.
  * Improved RoboRewsty workflow generation to correctly configure with items task inputs and iteration settings.
* **Workflow Builder**
  * Restored automatic propagation of default sub-workflow input values to existing parent workflow actions in the new canvas.
* **Crates**
  * [Rewst's AI PSA Analyzer](../../documentation/crates/existing-crate-documentation/rewsts-ai-psa-analyzer-crate.md)
    * Persist AI-recommended crate suggestions to org var psa\_analysis\_results for downstream use (96032)
    * Fix NinjaOne logic to correctly list filtered tickets (98806)
    * Use ID (not UID) for NinjaOne board values in option generation (98807)
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Show send\_sms\_to\_user checkbox based on org var and password section; removed phone\_number dependency (95628)

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [FLOW](https://www.mspflow.events/)!

</details>
{% endupdate %}

{% update date="2026-06-12" %}
## 💻 June 12, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **General**
  * Improved workflow execution query performance by reducing redundant trigger lookups.
  * Improved workflow execution performance to deliver faster loading times for large execution histories.
* **Onboarding**
  * Added an optional onboarding step that helps PSA-connected customers analyze historical tickets and identify automation opportunities.
* **Workflow builder**
  * Made the new workflow canvas the default experience for workflow building.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Enabled App Builder template components to correctly render shared parent-organization templates for child-organization users.
  * Improved workflow output security while maintaining App Builder support for shared workflows across managed organizations.
* **Integrations**
  * Strengthened integration export permissions to prevent unauthorized cross-org access to pack YAML and documentation.
  * Hardened GraphQL query permissions to prevent unauthorized access to integration action options, unlisted trigger types, and runner data.
  * Fixed Proofpoint user listing to return each organization user only once when handling paginated results.
* **Organization Variables**
  * Fixed org variable updates to encrypt secret values correctly and prevent unauthorized or unsafe category changes.
* **RoboRewsty**
  * Fixed an issue where RoboRewsty could fail when removing workflow transitions between tasks connected by multiple paths.
* **Workflow Builder**
  * Restored selection highlighting on the new workflow canvas so the currently selected task or transition is always clearly indicated.
  * Fixed an issue where saving cron triggers in the new workflow canvas could prevent scheduled workflows from running.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Show "Send SMS to user" checkbox without requiring CTX.phone\_number; visibility now based on org variable and password section
    * Updated PowerShell workflows to use CW ASIO Run PowerShell with dynamic ConnectWise ASIO script ID lookup
    * Fixed JSON syntax, which was missing trailing commas, in Ingram Micro → Microsoft License Lookup template for Teams Enterprise and Microsoft 365 Copilot entries
  * [Just-In-Time Admin Access](../../documentation/crates/existing-crate-documentation/just-in-time-admin-access-crate.md)
    * Added Microsoft Entra Temporary Access Pass generation after Just-In-Time admin user creation and Global Admin assignment
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Save Offboarding Ticket SubType to the correct variable used by Microsoft User Offboarding, with fallback to legacy variable name
  * [Google: User Offboarding](../../documentation/crates/existing-crate-documentation/google-user-offboarding-crate.md)
    * Existing Ticket field now appears for all organizations using the Crate
  * [CIPP: Alert Triage](../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md)
    * Support for an additional payload format and normalize alerts to surface key details in PSA ticket notes
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [FLOW](https://www.mspflow.events/)!

</details>
{% endupdate %}

{% update date="2026-06-05" %}
## 💻 June 5, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Crate Marketplace**
  * Improved Crate Unpack by making Direct Form URLs easier to find.
* **General**
  * Enhanced the Rewst Status Page with regional status views, region-specific alerts, and improved workflow performance monitoring.
* **Organizations**
  * Improved PSA customer imports by loading customers only after users configure filters and start a search.
* **RoboRewsty**
  * Added RoboRewsty support for configuring task transition criteria sensitivity when creating or updating workflow tasks.
* **Workflow builder**
  * Restored trigger health visibility in the new Workflow Builder by adding External Status monitoring and error reporting to supported triggers.
  * Restored support for selecting any pack configuration in trigger integration overrides on the new Workflow Builder.
  * Added one-click access to workflow execution history from the new Workflow Builder while preserving the in-canvas execution viewer.
  * Added click-to-create trigger filters from incoming event data in the new Workflow Builder, making trigger configuration faster and easier.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Improved App Builder live page reliability by preventing transient authorization service errors from appearing as false “Not Authorized” failures.
* **General**
  * Strengthened cross-org security controls for user metadata lookups and rate limit subscriptions.
* **Integrations**
  * Improved NinjaRMM authentication handling to prevent intermittent workflow failures during token refresh.
* **RoboRewsty**
  * Fixed RoboRewsty-created workflow input variables so they now appear immediately and persist on the new Workflow Builder canvas.
  * Aligned RoboRewsty with the active draft workflow state so follow-up edits and workflow reads reflect the latest canvas changes.
  * Improved RoboRewsty conversation compaction to prevent token-limit errors in long-running chats.
  * Improved RoboRewsty’s Jinja rendering guidance to reduce template failures and help users recover faster while building.
* **Triggers**
  * Fixed trigger and CRON Critical Timing toggles so they immediately reflect their saved state without reverting in the UI.
* **Workflow Builder**
  * Fixed trigger criteria deletion in the new Workflow Builder canvas so removed criteria stay deleted after refresh.
  * Improved auto-arrange in the Workflow Builder so starting tasks stay positioned correctly even in workflows with loops.
* **Workflows**
  * Fixed completion handler timestamps so started and completed times now accurately reflect workflow duration.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added missing M365 Business Premium and Copilot Business license mappings to the M365 License Lookup template
    * Ensured Office field is applied for new Azure AD users during onboarding
    * Fixed Pax8 nonprofit donation licensing lookup to correctly identify Donation SKU
    * Prevented false "User Exists - Amend Username" on Secure Cloud IDP path by improving subworkflow error detection and defaults
    * Prevented false "User Exists - Amend Username" on on-prem path by detecting subworkflow failures earlier
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Replaced hardcoded BMS priority ID with runtime lookup; preserved existing fallbacks
  * [Sync AzureAD Account Information with ConnectWise PSA Contacts (v3)](../../documentation/crates/existing-crate-documentation/sync-azuread-account-information-with-connectwise-psa-contacts-v3-crate.md)
    * Fixed phone number sync when M365 and ConnectWise email casing differs
  * [Billing Count Report](../../documentation/crates/existing-crate-documentation/billing-count-report-crate.md)
    * Corrected logic to list Dropsuite counts accurately
  * [Rotate Account Passwords](../../documentation/crates/existing-crate-documentation/rotate-account-passwords-crate.md)
    * Added org-level PWPush link expiration settings (days/views) and updated delivery messages
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Added cloudmore and secure\_cloud options for ms\_licensing\_distributor org variable
  * [Add Client to Rewst](../../documentation/crates/existing-crate-documentation/add-client-to-rewst-setup.md)
    * Added "no AD sync" form option; included `onprem_no_adsync` in organization variable sets
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New workflow canvas as default view

</details>
{% endupdate %}

{% update date="2026-05-29" %}
## 💻 May 29, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **RoboRewsty**
  * Added support for RoboRewsty to build scripts, expanding AI-assisted workflow creation beyond templates.
* **Workflow Builder**
  * Improved the new Workflow Builder canvas zoom-out range so users can view and navigate larger workflows more easily.
  * Renamed the "New Actions" section to "Next Actions" in the workflow execution viewer to provide clearer action flow terminology.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **General**
  * Strengthened Graph API security controls to address findings from a vulnerability assessment and improve platform resilience.
* **Workflow Builder**
  * Fixed an issue where the workflow header disappeared when clicking tasks in execution history for large workflows, keeping navigation and controls consistently visible.
  * Fixed an issue that prevented workflows with invalid or deleted form trigger references from being saved, synced, or published successfully.
  * Fixed Library search in the new Workflow Builder to return only actions matching the user’s search term.
  * Fixed an issue where saving Advanced settings on SQL Custom Query actions caused the new workflow canvas to render blank.
* **Crates**
  * [Bulk Create Client from PSA](../../documentation/crates/existing-crate-documentation/bulk-create-client-from-psa-crate.md)
    * Made `account_types` and a`ccount_statuses` optional for Datto PSA; when empty, return all customers
      * Made `account_types` and `account_statuses` optional for Halo PSA; updated `halo_list_psa_clients` to return all when types empty, else filter
  * [Alert on Unused M365 Licenses](../../documentation/crates/existing-crate-documentation/alert-on-unused-m365-licenses-crate.md)
    * Prevented duplicate removals when Remediate is clicked multiple times during commitment; daily scan no longer creates repeat tickets for queued removals
  * [Organizational Setup Report](../../documentation/crates/existing-crate-documentation/organizational-setup-report-crate.md)
    * Added on-demand email form trigger; default email pulled from org variable and updated on submit; submitting generates and emails the report
  * [Report on Disabled M365 Users with Licenses](../../documentation/crates/existing-crate-documentation/report-on-disabled-m365-users-with-licenses-crate.md)
    * `get_webhook_trigger` now matches trigger type names containing `webhook` instead of filtering by a specific ID
  * [Add Client to Rewst](../../documentation/crates/existing-crate-documentation/add-client-to-rewst-setup.md)
    * Renamed Azure Active Directory to Microsoft Entra (AAD); added field for ConnectWise ASIO integration mapping
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Fixed device matching across multiple sites by flattening endpoints before filtering in `list_computers` On Success
      * Added sanitized\_zip to zero‑pad 4‑digit ZIPs; `cw_update_contact` and `cw_create_contact` now use it
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Check back soon

</details>
{% endupdate %}

{% update date="2026-05-22" %}
## 💻 May 22, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Standardized Microsoft bundle logo sizing and appearance across light and dark mode in the integration setup wizard.
* **Onboarding**
  * Added guided customer import options during onboarding based on the customer’s PSA platform and configuration status.
  * Displayed detailed per-row CSV import errors in the bulk organization import modal so customers can quickly identify and fix failed imports.
  * Made CSP Licensing and Documentation integrations optional during onboarding so customers can skip these steps and continue setup at their own pace.
* **RoboRewsty**
  * Improved RoboRewsty task updates so workflows with multi-line Jinja templates can be created and edited successfully.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Crate Marketplace**
  * Secured Crate unpacking argument access so customers can only retrieve unpacking configurations for organizations they manage.
* **Integrations**
  * Allowed customers to recreate deleted or hidden integrations without being blocked by invisible name conflicts.
* **Roborewsty**
  * Fixed RoboRewsty trigger creation and updates so users can successfully add and modify workflow triggers through AI assistance.
  * Fixed RoboRewsty HTTP request generation so headers and parameters are saved as proper key-value fields instead of broken character-indexed values.
* **Workflow Builder**
  * Fixed an issue in the new workflow canvas where editing object-list fields could unintentionally clear existing parameter values.
  * Secured workflow configuration access so users can only view input and output schemas for workflows in organizations they manage.
  * Restored shift+click multi-selection in the new Workflow Builder so users can select, move, and manage multiple nodes more precisely.
  * Fixed Action Options dropdowns in the new workflow builder so saved values display correctly immediately when opening action settings.
  * Improved workflow completion reliability by preventing intermittent database connection and Jinja timeout failures.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Updated onboarding form to make force\_password\_change and password\_never\_expires mutually exclusive
    * Added | json filter to pax8\_sku\_mapping alias in \[REWST TASK] Licenses: Update Quantity
    * Updated \[REWST - TASK] CW ASIO: Run PowerShell list\_shell\_scripts failure transition to use input script\_id or default ID
    * Added CW, SX, and BQ to ISO 3166 country code options generator (90206)
    * Added object in script at correct sequence
    * Reordered FAILURE transition for core\_await\_webhook\_request and set webhook expiration to 85800
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Added default\_sla to Create or Update Org Variable
  * [Google: User Onboarding](../../documentation/crates/existing-crate-documentation/google-user-onboarding-crate.md)
    * Updated check\_copy\_user to use manager's email address instead of ID
  * [Rewst Microsoft GDAP Assistant](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
    * Fixed Jinja failure in Create GDAP Relationship sub-workflow that stopped execution
    * Corrected msp\_created\_relationships filter to use customer.tenantId and de-duplicated customer\_name\_history
  * [Compromised User Response](../../documentation/crates/existing-crate-documentation/compromised-user-response-crate.md)
    * Updated Jinja in external\_forward\_rules to return only external emails
  * [Reset Locked Accounts](../../documentation/crates/existing-crate-documentation/reset-locked-accounts-crate.md)
    * list\_locked\_accounts now runs as org using CTX.org\_id in \[REWST - OPT GEN] List Locked-Out Accounts
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Updated Rewst login page

</details>
{% endupdate %}

{% update date="2026-05-15" %}
## 💻 May 15, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Crate Marketplace**
  * Added an “Attention Needed” integration state to crate details pages when health checks detect broken configurations.
* **Onboarding**
  * Sorted onboarding checklist crates by use case complexity to guide MSPs toward easier early wins.
* **RoboRewsty**
  * Added context compacting to avoid max context errors.
* **Workflow Builder**
  * Closed the Action Settings pane automatically when deleting tasks in the new workflow canvas.
* **New Crates**
  * [Rewst's AI PSA Analyzer](../../documentation/crates/existing-crate-documentation/rewsts-ai-psa-analyzer-crate.md) - This Crate uses Rewst’s internal AI or your integrated Anthropic or OpenAI provider to analyze ticket data and recommend the most effective automations for your customers' needs. The workflow pulls filtered ticket data from a specific number of days. Using AI to evaluate that data, it identifies the most relevant existing Rewst Crates and recommends custom automations if needed. Runtime may vary depending on the PSA platform and ticket volume.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed Microsoft Graph user actions to stop defaulting blank usage locations to US.
  * Normalized crate category casing so the marketplace shows a single Financial Management category.
  * Fixed ConnectWise ASIO paginated requests to return all available results instead of stopping at 100 items.
  * Fixed OAuth authorization popups in custom integrations.
* **Workflow Builder**
  * Fixed workflow version history crashes by correctly displaying “Deleted User” for changes made by removed users in the new canvas view.
  * Fixed array input fields to show and allow editing of Jinja values in the new canvas.
  * Fixed target workflow autocomplete to filter matching workflows immediately while typing in trigger settings.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Fixed false failure logs being reported during valid retry attempts
    * Onboarding New User Ticket Summary will reference requestor now if username is empty
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * The field nable\_device\_filter\_id is now hidden if customer does not have n\_able as their default RMM
  * AI Ticket Categorization Crates - Added Hatz AI implementation to the 3 AI Crates:
    * [Use AI to Suggest Responses to Tickets](../../documentation/crates/existing-crate-documentation/use-ai-to-suggest-responses-to-new-tickets-crate.md)
    * [AI Ticket Categorization](../../documentation/crates/existing-crate-documentation/openai-ticket-categorisation-setup.md)
    * [AI Ticket Sentiment Analysis Crate](../../documentation/crates/existing-crate-documentation/openai-ticket-sentiment-setup.md)
  * [CIPP: Alert Triage](../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md)
    * Updated the Has Valid Tenants Jinja to handle different payloads and updated the template to handle varying alert shapes
  * [Amend Mailbox Permissions](../../documentation/crates/existing-crate-documentation/amend-mailbox-permissions-crate.md)
    * Updated the Jinja to include shared mailboxes and enabled pagination if more than 1000 users are returned
  * [Amend Calendar Permission on User](../../documentation/crates/existing-crate-documentation/amend-calendar-permission-on-user-crate.md)
    * Changed the ID from Identity to ExternalDirectoryObjectId
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Empty files are now moved to the offboarding folder
    * Offboarding folder email notifications are now delivered to target recipients
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Check back soon!

</details>
{% endupdate %}

{% update date="2026-05-08" %}
## 💻 May 8, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * [Action version history](https://docs.rewst.help/documentation/automations/actions-in-rewst#action-version-updates) - When an integration action used in your workflows has been updated or has a breaking change, Rewst will now alert you directly in the platform so you can take action before anything breaks.
* **Onboarding**
  * [Client Import to Rewst organization](../../documentation/settings/organizations.md) - Added the ability to import customer organizations directly into Rewst via CSV import or PSA import (Autotask PSA, HaloPSA, or ConnectWise PSA)
* **Workflow Builder**
  * Added Follow First transition tooltips and right-click navigation to edit transition order directly from the workflow canvas.
* **Crates**
  * No new Crates were released this week.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Improved Addigy API requests to handle pagination correctly across v1 and v2 endpoints.
  * Restored Addigy mapping refreshes so policy and organization options can be selected after reinstalling the integration.
  * Added Australia and Europe environment support to the 1Stream integration for region-specific API connectivity.
  * Improved CW ASIO access token errors to show the API response details when credential exchange fails.
  * Fixed Ubiquiti org mapping to display nested site names correctly and save the mapped site IDs.
* **Workflow Builder**
  * Improved workflow save validation to prevent false version-conflict errors caused by browser and server clock drift.
  * Restored Jinja viewing and editing for action inputs in the new workflow canvas.
  * Fixed workflow version diffing to prevent notes from appearing as changed when no actual workflow changes were made.
  * Stabilized Integration Overrides in the new canvas so affected actions remain visible and settings render correctly.
* **RoboRewsty**
  * Improved RoboRewsty conversation handling to prevent token-limit crashes and retry transient model errors automatically.
* **Crates**
  * [Agent Smith: Service Provisioning \[Install Second\]](../../documentation/agent-smith/agent-smith-configuration-overview.md)
    * Updated form descriptions to specify which org variables to use
    * Removed the **Remove Control Device** form the action dropdown
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Show group display names in onboarding ticket notes instead of GUIDs
    * Enhanced user validation: detect existing users by email, UPN, and proxyAddresses; on-prem AD checks proxyAddresses to prevent duplicates
    * Fixed conditional for get\_all\_security\_groups in "List On-Prem Groups — Not Tenant Specific— subworkflow
    * Fixed false positives in User: Check Exists; improved on-prem error detection; standardized failure handling; added task logs
    * Debugged/validated BYOD SQL integration; fixed user\_exists false positive; confirmed db\_override gate and skipCache wiring; updated docs and workflow lists
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Refactored OneDrive grant: create Offboarding\_Transfer, move root items, share with recipient
  * [Triage SentinelOne Tickets](../../documentation/crates/existing-crate-documentation/triage-sentinelone-tickets-crate.md)
    * Tightened trigger criteria: run only when Entity.summary contains `sentinelone`, `machine`, and `threat`
  * [CIPP: Alert Triage](../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md)
    * Rewrote Build Ticket Variables as template to support both drift and flat payloads; dedupes and routes standards alerts correctly
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* **Crates**
  * Rewst's AI PSA Analyzer - This Crate uses Rewst’s internal AI or your integrated Anthropic or OpenAI provider to analyze ticket data and recommend the most effective automations for your customers' needs.

</details>
{% endupdate %}

{% update date="2026-05-01" %}
## 💻 May 1, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflow Builder**
  * The new [Workflow Builder](/broken/pages/6cIR2bnP5Js8cytxzRfO) is now enabled for all customers. A redesigned experience bringing a more intuitive way to build and manage your workflows.
  * We added a Compact Auto Layout toggle that reduces node spacing, making it easier to view and manage larger workflows.
  * We added the ability to navigate workflows using the Data Aliases tab, making it quicker to find and reference your data aliases while building.
* **Crates**
  * [CIPP Microsoft Desired State/Standards Compliance Crate](../../documentation/crates/existing-crate-documentation/cipp-microsoft-desired-state-standards-compliance-crate.md) - Our CIPP: Microsoft Desired State/Standards Compliance Crate monitors Microsoft 365 tenant configurations against a desired state baseline using the CIPP (CyberDrain Improved Partner Portal) integration.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * An issue has been fixed in the Liongard integration where the Create User action was missing the Environment and Environment Group fields required when assigning Manager or Reader roles.
  * We fixed an issue in the Lexful integration where refresh option dropdowns only returned the first \~40 values due to a pagination bug.
  * The `platform.agent.read` scope has been added to the default permission set for the ASIO integration.
* **Crates**
  * The Crate details page now correctly surfaces whether a primary workflow is synced or unsynced, giving better visibility into the state of your installed Crates.
* **Onboarding**
  * Child level Crate executions now count towards Crate execution tracking, giving a more accurate picture of overall Crate usage.
* **Engine**
  * We fixed an issue where integration overrides were not accepting Jinja expressions when using Name Search mode.
  * An issue where `sites.id` was not being typed as a Universally Unique Identifier during site existence checks, which could cause unexpected errors, was resolved.
  * We improved the efficiency of workflow dehydration by reusing a singleton S3 client rather than creating a new one each time.
  * We added a `tenantFilter` query parameter to the CIPP List MFA Users action, allowing results to be filtered by tenant.
  * A policy mapping error in the Addigy integration that was causing actions to fail has been resolved.
* **Workflow Builder**
  * We removed an unused patch field from workflow history queries, reducing unnecessary data being fetched in the background.
* **RoboRewsty**
  * We removed distracting hover animations in the RoboRewsty chat window that were causing a jarring jump effect when moving the mouse over conversation elements.
  * An issue where RoboRewsty was setting workflow timeouts too low, which could cause workflows to terminate before completing, has been fixed.
* **Crates**
  * [PSA: Update Ticket with User Offboard Links](../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-offboard-links-crate.md)
    * Corrected the Halo transition condition from "Halo PSA" to "HaloPSA"
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Added missing `log_ data` aliases
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Updated the Jinja to strip out zero-width Unicode characters in `ms_sku_to_friendly_name`
    * Added a filter to only return enabled users
    * Updated AD On Prem: Copy Existing User script to use the Manager property for HomeDrive and HomeDirectory
    * Added missing SKU `M365_F1_COMM`
  * [Run Powershell Script on Selected Devices](../../documentation/crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md)
    * Updated CW ASIO: Run PowerShell to use v2 API endpoints for `list_computers` and `run_powershell`
    * Added cw\_asio evaluation in `rewst_get_organization_variable`
  * [Find Inactive Computers in RMM](../../documentation/crates/existing-crate-documentation/find-inactive-computers-in-rmm-crate.md)
    * Updated List Computers to use the v2 API endpoint and include last-contact and online status data
  * [Microsoft Subscription Renewal Alerts](../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
    * Workflow will not return tickets for all mapped organizations
  * [Agent Smith: Device Provisioning \[Install First\]](../../documentation/agent-smith/agent-smith-configuration-overview.md)
    * Changed query approach to handle case-insensitivity in device names
  * [Add or Remove Group Membership](../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
    * Fields now appear based on identity provider
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* RoboRewsty - editing of scripts and templates
* Action Version History

</details>
{% endupdate %}

{% update date="2026-04-24" %}
## 💻 April 24, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Standardized error messages across all integrations so failed actions return consistent, structured error details including status code, error type, and response body for easier troubleshooting.
* **Onboarding**
  * Added vendor pre-requisite setup as a dedicated informational step in the onboarding checklist, making it clearer what needs to be configured in third-party systems before installing an integration in Rewst.
* **RoboRewsty**
  * Added transparency when users share external URLs — RoboRewsty now informs users it cannot read external links and suggests pasting the relevant content directly into the chat.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **General**
  * Fixed org variable queries that threw errors when filtering by ID or pack config without specifying an org ID, which prevented workflows and UI views from loading org variables correctly.
* **Integrations**
  * Corrected the Lexful integration dashboard link to point to the correct URL.
  * Fixed the SentinelOne integration so actions that accept multiple IDs (like List Threats) correctly process all values in the array instead of only the first, and resolved a pagination error on generic API requests.
  * Fixed the SQL Database "List Database Configurations" action so it correctly returns results when run from a sub-organization that inherits the integration from its parent.
  * Updated the ServiceNow integration test action to use an endpoint that does not require a paid plugin, so connectivity tests now succeed on standard ServiceNow instances.
* **RoboRewsty**
  * Fixed an issue where RoboRewsty-generated input variables could have non-boolean values for the "Required" checkbox, preventing users from toggling it on or off.
  * Fixed code block copy so the clipboard no longer includes the language identifier (e.g., "jinja") as the first line when copying code examples from RoboRewsty.
* **Workflows**
  * Fixed workflow execution results and context layers failing to load with a server error, which blocked users from viewing task logs and context data on completed workflow runs.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Use Manager property for HomeDrive/HomeDirectory in AD On Prem: Copy Existing User script
    * Added missing SKU `M365_F1_COMM`
  * [Run Powershell Script on Selected Devices](../../documentation/crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md)
    * Added `cw_asio` evaluation in `rewst_get_organization_variable`
  * [Microsoft Subscription Renewal Alerts](../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
    * Added do not return tickets for mapped organizations
  * [Agent Smith: Device Provisioning \[Install First\]](../../documentation/agent-smith/agent-smith-configuration-overview.md)
    * Handle case-insensitivity in device name queries
  * [Add or Remove Group Membership](../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
    * Fields now appear based on identity provider
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Added `valid_idp` alias so `idp_config` evaluates properly
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Added cw\_asio option for `default_rmm`
  * [CIPP Alert Triage](../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md)
    * Added condition to default to parent organization when not running for child organization
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-04-17" %}
## 💻 April 17, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Ubiquity Integration - docs found [here](../../documentation/integrations/integration-guides/ubiquiti-integration.md)
  * Added new Microsoft Teams messaging actions (Send Teams Message and Send Inquiry Message) to the Microsoft Graph integration using Power Automate webhooks and Adaptive Cards while deprecating legacy connector-based actions.
  * Updated the Lexful integration setup experience by refining setup instructions and hiding UAT configuration options in production.
* **Workflows**
  * Persisted the Context Viewer open/closed state across reloads and editor sessions.
  * Fixed task deletion on the new workflow canvas to properly remove associated transitions and prevent orphaned nodes.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Forms**
  * Fixed an issue where form field changes could unexpectedly revert or clear during editing.
* **Integrations**
  * Fixed Google Workspace Admin SDK pagination so paginated API requests handle Google’s token-based response format correctly.
  * Fixed the Bitdefender Delete Endpoint action to successfully delete endpoints without API errors.
  * Re-enabled the ConnectWise ASIO List Groups action so device groups can be retrieved successfully.
* **Triggers**
  * Fixed the triggers list so enabling or disabling synchronized clone triggers persists correctly and is no longer overwritten by crate sync.
* **Workflows**
  * Fixed Jinja filter documentation lookup so valid parameterless filters return successfully instead of showing a false “not found” error.
  * Fixed org variable queries to correctly handle filters without orgId and prevent SQL errors for non-staff users.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Use Domain Controllers filter in List Devices API to narrow search for large orgs.
    * Fixed Send Supervisor Password field: option Gen now sets value to identity; previously EXO GUID caused Send Mail failure.
  * [AI Ticket Sentiment Analysis](../../documentation/crates/existing-crate-documentation/openai-ticket-sentiment-setup.md)
    * Added SuperOps support.
  * [AI Ticket Categorization](../../documentation/crates/existing-crate-documentation/openai-ticket-categorisation-setup.md)
    * Added caching for issue types/subtypes to reduce task usage.
  * [Rotate Local Workstation Passwords](../../documentation/crates/existing-crate-documentation/rotate-local-workstation-passwords-crate.md)
    * Script now retrieves all MAC addresses.
    * Updated compiled\_assets data alias (Hudu/IT Glue) to update all matched assets by MAC address.
  * [Agent Smith: Service Provisioning \[Install Second\]](../../documentation/agent-smith/agent-smith-configuration-overview.md)
    * rewst\_engine\_url alias now uses APP.engine\_url instead of hardcoded value.
  * [Cork: Compliance Event to PSA Ticket](../../documentation/crates/existing-crate-documentation/cork-compliance-event-to-psa-ticket-crate.md)
    * Updated SuperOps tickets alias Jinja to filter by superops\_client\_id org variable.
  * [Microsoft Subscription Renewal Alerts](../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
    * company\_id for create\_service\_ticket now resolves dynamically by default\_psa across supported PSAs (CW Manage, Datto, Halo, Freshdesk, ServiceNow, Kaseya BMS, SuperOps, NinjaOne).
  * [PSA: Update Ticket with New User Onboard Links](../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-offboard-links-crate.md)
    * Added org variable setup to both Onboard and Offboard link update crates.
  * [Use AI to Suggest Responses to New Tickets](../../documentation/crates/existing-crate-documentation/use-ai-to-suggest-responses-to-new-tickets-crate.md)
    * Datto New Ticket trigger now sends Title, Description, and Queue.
  * [Sync AzureAD Account Information with ConnectWise PSA Contacts (v3)](../../documentation/crates/existing-crate-documentation/sync-azuread-account-information-with-connectwise-psa-contacts-v3-crate.md)
    * Removed inline comment causing an error.
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-04-10" %}
## 💻 April 10, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Dashboard**
  * Optimized hourly task count queries to improve dashboard performance while preserving complete 24-hour reporting, including zero-count hours.
* **Integrations**
  * Added support for token-based authentication in the Cove integration, enabling new API users to connect using API tokens.
* **Onboarding**
  * Self-guided onboarding
  * Auto-closed the onboarding checklist panel on navigation to ensure destination pages are fully visible and accessible.
  * Made onboarding checklist section headers clickable to allow users to easily navigate back to the corresponding tab listing.
* **RoboRewsty**
  * Form builder - Open RoboRewsty from the Form Builder, describe the form you need, and he will build it for you. No more dragging and dropping fields one by one.
  * Custom Instructions - Set persistent guidelines that shape how RoboRewsty responds to you. Find "RoboRewsty Custom Instructions" in your preferences menu (top right). Applies to all future interactions, configured per user.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **App Builder**
  * Fixed App Builder dropdowns to correctly pre-select default options from options generators, matching the behavior in standard Rewst forms.
* **Crate Marketplace**
  * Fixed crate integration requirement checks to correctly evaluate OAuth integrations using health checks, ensuring accurate “installed and configured” statuses and improved tooltip readability.
* **Forms**
  * Fixed an issue where dynamic option filters were not loading in the form editor, ensuring saved filter configurations are visible and editable.
* **Integrations**
  * Updated the Hatz AI “Upload File” action to support required `scope_type` and `scope_id` fields, ensuring file uploads succeed with the new API contract.
  * Fixed Cloud Bundle tenant lookup so workflows correctly resolve the customer’s Microsoft tenant ID in edge cases without requiring a prior cached run or manual workaround.
  * Corrected the Lexful integration production base URL to use the proper endpoint, ensuring API calls succeed against the correct service.
  * Fixed issues with the Rewst Export Object action causing failures across object types, ensuring objects can be successfully retrieved and exported.
  * Fixed an issue where Autotask PSA ticket trigger dropdown fields were not loading, restoring expected options during trigger configuration.
* **Onboarding**
  * Updated the onboarding checklist “Done” indicator to remove misleading interactivity, ensuring it no longer appears clickable without an associated action.
* **RoboRewsty**
  * Added workflow build validation to ensure RoboRewsty-created workflows finished with required transitions on non-terminal tasks, preventing incomplete or unrunnable workflow paths.
  * Fixed an issue where RoboRewsty chat state persisted across sessions by scoping stored state to the current user and clearing it on logout.
  * Fixed RoboRewsty workflow note tools on the new canvas by restoring note handling support, enabling notes to be added and updated correctly.
* **Workflows**
  * Masked secret organization variable values in execution results to prevent sensitive data from being exposed in plain text.
* **Crates**
  * [Reset Locked Accounts](../../documentation/crates/existing-crate-documentation/reset-locked-accounts-crate.md)
    * Added `runAsOrg` so the subworkflow executes in the suborganization's context and carries the override.
  * [Rotate Local Workstation Passwords](../../documentation/crates/existing-crate-documentation/rotate-local-workstation-passwords-crate.md)
    * Added Agent Smith actions to display workstations.
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Updated the PAX8 product name for `Microsoft_Teams_Audio_Conferencing_select_dial_out`.
  * [Add or Remove Group Membership](../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
    * Removed the `get_user` action from the workflow.
    * Updated the script template to use objectGUID directly instead of retrieving `userOnpremUPN` via the `get_user` Graph action.
    * Updated the script template to properly handle multiple values for `onprem_groups_to_remove`.
  * [CW PSA: Pod Technician Toolbox v2](../../documentation/crates/existing-crate-documentation/cwm-technician-toolbox-via-pod-1.md)
    * Reduced the number of tasks run before the first pod shows up in ConnectWise.
    * Added new logic for how the link is checked or created.
    * Added a new action to get the tenant ID.
  * [Rewst Microsoft GDAP Assistant](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
    * Updated the first two form field descriptions to clarify they are not required but recommended to fully set up the Microsoft integration.
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.
* Ubiquity integration
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-04-03" %}
## 💻 April 3, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Onboarding**
  * Added Crate guidance to the onboarding checklist.
* **RoboRewsty**
  * RoboRewsty's underlying instructions were restructured to follow AI best practices, resulting in clearer and more accurate guidance when building workflows, especially around variable creation, Jinja expressions, and error handling patterns.
* **Special UI bonus**
  * We've hidden a little holiday surprise in the app, but you'll have to wait for the right day to find it.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Dashboard**
  * Fixed inconsistent historical task stats.
* **Engine**
  * Fixed an issue where stat buffers were not fully flushed during batching, which could result in incomplete data being processed.
  * Fixed an issue where workflow sequences could enter an unrecognized status, causing unexpected errors during execution.
  * Fixed bundle packs not being included in pack discovery.
* **Integrations**
  * Fixed a crash caused by a TypeError when using 'Suggest Customer Mappings' for Microsoft Cloud Bundle integration.
  * Fixed unsaved packs defaulting to all permissions selected on CPV consent in Microsoft Cloud Bundle integration.
  * Added a contacts field to the 'Create Company' action in Pax8 integration.
* **RoboRewsty**
  * Improved task positioning for tasks added by RoboRewsty.
* **Workflow Builder**
  * Preserved large numeric strings that exceed JavaScript precision in object field parsing.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Return only a single valid session ID
    * Use officeLocation when listing Entra offices
    * Use Markdown-only new\_user\_approval\_email template
    * Restrict device list to customer devices in PS sub-workflow
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Add missing Organization ID entry to Ninja Severity org variable
  * [Amend Calendar Permission on User](../../documentation/crates/existing-crate-documentation/amend-calendar-permission-on-user-crate.md)
    * Remove unassociated form from Crate
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Correct SKU to proper product name
  * [REWST CA Policy Assistant](../../documentation/crates/existing-crate-documentation/rewst-ca-policy-assistant-crate.md)
    * Default CTX.user\_id in list\_all\_customers\_ca\_policies
  * [AI Ticket Sentiment Analysis](../../documentation/crates/existing-crate-documentation/openai-ticket-sentiment-setup.md)
    * Handle empty string in select\_psa task transition condition
  * [Notify on Conditional Access Policy Changes](../../documentation/crates/existing-crate-documentation/notify-on-conditional-access-policy-changes-crate.md)
    * Fix transition order and condition in get\_user\_auth\_reg\_details
  * [Just-In-Time Admin Access](../../documentation/crates/existing-crate-documentation/just-in-time-admin-access-crate.md)
    * Treat check\_script\_was\_provided as boolean in CW ASIO: Run Powershell
  * [Run Powershell Script on Selected Devices](../../documentation/crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md)
    * Prefer matching "PowerShell script" from List Shell Scripts before script\_id input
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-03-27" %}
## 💻 March 27, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Hatz AI integration - documentation found [here](../../documentation/integrations/integration-guides/hatz-integration.md)
  * Expanded the Microsoft Cloud Bundle to expose all supported permissions, added recommended permission selection, and improved guidance and validation around Microsoft permission limit errors.
  * Added Huntress POST and DELETE actions to support creating and managing accounts, organizations, incident resolutions, remediations, and memberships.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Dashboard**
  * Preserved historical dashboard task and time-saved metrics when sub-organizations are deleted or moved.
* **Forms**
  * Fixed an issue where stale form name filters persisted in browser storage, causing the Forms page to display incomplete results without an active filter.
* **Integrations**
  * Fixed an issue where the SentinelOne "List Threats" action returned only a single threat when multiple threat IDs were provided.
  * Fixed an issue where the SuperOps New Ticket Record trigger did not activate when new tickets were created.
* **RoboRewsty**
  * Fixed an issue where RoboRewsty created triggers without saving trigger criteria in a valid format, ensuring criteria now appear and work correctly.
* **Triggers**
  * Fixed an error preventing users from sorting triggers by type in the Trigger View.
* **Workflows**
  * Ensured parent workflows were reliably notified of sub-workflow completion, preventing workflows from getting stuck due to transient notification failures.
* **Crates**
  * [Alert on Low Disk Space](../../documentation/crates/existing-crate-documentation/alert-on-low-disk-space-crate.md)
    * Added CW ASIO Get Computer subworkflow and retry logic to handle API rate limits
  * [Document M365 Environment](../../documentation/crates/existing-crate-documentation/document-m365-environment-setup.md)
    * Added INFO\_PROTECTION\_GOVERNANCE to the M365 License Lookup template
  * [Remove Malicious Email and Block Sender](../../documentation/crates/existing-crate-documentation/remove-malicious-email-and-block-sender-crate.md)
    * Show "no messages/mailboxes" alert only when fewer than 500 items due to PSA limits
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Conditional ticket update when granting OneDrive sharing; checks for org variable offboarding\_suppress\_onedrive\_email
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Added TD Synnex Stellr to License Group subworkflow
    * Updated ticket description for Pax8 license purchase failure
    * Added integration override to trigger for TD Synnex Stellr
    * Published final\_upn from creation steps so it can be used for Azure AD user lookup
    * Clarified wording that form attributes (except domain) override copied user attributes
    * Built conditional OtherAttributes (c/co/countryCode) before New-ADUser to avoid empty-field failures
    * Added ticket completion logic, mark\_complete input (default true), and org variable auto\_complete\_onboarding\_ticket
    * Removed assigned\_user\_id from Assigned App User ID to resolve error
    * Updated filter\_product Jinja to include Nonprofit Staff Pricing (NCE) check
  * [Agent Smith: Service Provisioning \[Install Second\]](../../documentation/agent-smith/agent-smith-configuration-overview.md)
    * Removed duplicate "Agent Smith: IoT Hub Actions" subworkflows from parent/sub/opt gens
  * [Traveling Employee CA Policy](../../documentation/crates/existing-crate-documentation/traveling-employee-ca-policy-crate.md)
    * Set default selection for Destination Countries in MSP and Self-Service forms
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Workflow canvas redesign beta

</details>
{% endupdate %}

{% update date="2026-03-20" %}
## 💻 March 20, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Jinja context viewer - documentation found [here](../../documentation/jinja/context-viewer.md)
* **Onboarding**
  * Enabled manual override to mark the org mapping onboarding sub-step as complete when 80% mapping cannot be reached due to integration org count differences.
* **Triggers**
  * Added access to the form usages dialog directly from the Trigger View Forms tab to quickly view form URLs without navigating away.
* **Crates**
  * [CIPP Alert Triage Crate](../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md) - This new Crate automates processing CIPP alerts with tenant/message exclusions, auto creates/updates PSA tickets, and provides a configuration form for per-org mappings and rules.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed Connectw PSA - Manage board queries to continue paginating Type–Subtype–Item associations beyond 20 pages so all available board items are returned.
  * Added missing CW ASIO scopes for platform.devices.write, platform.suspension.read, and security.vulnerability.read.
  * Changed Dropsuite org mapping to use the organization name instead of the mapped email address so org associations are displayed and matched more accurately.
  * Removed deprecated SQL DB integration fields from the integration config page.
* **Workflows**
  * Fixed an issue where items processed later in a With Items batch could be passed to subworkflows as empty objects when concurrency was enabled.
* **RoboRewsty**
  * Fixed RoboRewsty workflow context handling so it correctly recognized the active workflow after users switched editors and properly distinguished workflow IDs from action IDs.
  * Improved RoboRewsty’s workflow transition editing to prevent duplicate links and make updates to transition criteria and data aliases apply more reliably.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Updated the Jinja in filter\_product to check for Nonprofit Staff Pricing - New Commerce Experience.
  * [Alert On Users Without MFA Enforced](../../documentation/crates/existing-crate-documentation/alert-on-users-without-mfa-enforced-crate.md)
    * Updated `check_trigger_type` to detect webhooks based on the ref attribute.
  * [Microsoft Subscription Renewal Alerts](../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
    * Updated Jinja for `expiring_subscription` to exclude suspended status.
    * PSA: Check if Existing Ticket now checks in NinjaOne.
    * Freshdesk and ServiceNow now retrieve existing tickets using closedFlag and Ticket Summary.
  * [Rewst Microsoft GDAP Assistant](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
    * Added CTX.active\_relationships check before withitems to avoid errors when no active relationships exist.
  * [Alert on AV/EDR Coverage Gaps](../../documentation/crates/existing-crate-documentation/alert-on-av-edr-coverage-gaps-crate.md)
    * Fixed newline comment handling and typo; enhanced Create Ticket
      * fallback to initial\_description, support assignee\_id; added cc\_emails, tags, initial\_description\_html; use contact\_id, parent\_ticket\_id); removed unnecessary set\_variables and moved company\_id->ORG.VARIABLES.ninja\_org\_id fallback into create\_ticket.
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Added conditional: if input has @ use -Filter against UserPrincipalName; else use -Identity for SAMAccountName.
  * [Amend Mailbox Permissions](../../documentation/crates/existing-crate-documentation/amend-mailbox-permissions-crate.md)
    * Disabled custom trigger in \[Rewst] EXO: Manage Mailbox Permissions using \[ROC] Crate and kept the trigger synced from crate-dev.
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Hatz AI integration

</details>
{% endupdate %}

{% update date="2026-03-13" %}
## 💻 March 13, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Triggers view - dedicated page to view all triggers
* **Integrations**
  * Lexful integration - Enables the automation of IT documentation management in Lexful. Documentation found [here](../../documentation/integrations/integration-guides/lexful-integration.md).
  * Updated branding from ConnectWise Control to ConnectWise ScreenConnect across the platform and website to align with ConnectWise’s current brand standards.
  * Added a v2 ConnectWise ASIO endpoint action for listing computers to improve compatibility where the legacy list endpoint could fail.
* **General**
  * Navigation redesign
  * RoboRewsty AI generated workflows

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed an issue where Google Workspace Admin actions could not clear recoveryPhone and recoveryEmail fields when left blank.
  * Fixed an issue where OpenAI Create Response requests in background mode could fail when empty optional objects were sent to the API.
  * Improved Azure OpenAI error handling by showing clear guidance for unsupported model actions instead of raw Azure errors.
* **Onboarding**
  * Fixed an issue where onboarding questionnaire submissions could fail validation due to a null priority value when switching between custom “Other” responses and standard options.
* **RoboRewsty**
  * Enabled transitions, including conditions and data aliases, to be created by RoboRewsty on terminal workflow tasks without requiring a downstream target.
  * Prevented duplicate approval submissions by disabling approval bubble actions immediately when clicked.
* **App Builder**
  * Fixed an issue where the AppBuilder Theme Settings panel could fail to load for apps with missing theme data by restoring the default theme instead of showing an error.
* **General**
  * Fixed an issue where consumers did not restart after a RabbitMQ reconnection, which could cause message processing to stop until the service was restarted.
  * Fixed an issue where the Admin View (Staff Only) section could appear but could not be navigated to in the side navigation for non-staff users when Support Access was enabled.
* **Crates**
  * [AI Ticket Sentiment Analysis](../../documentation/crates/existing-crate-documentation/openai-ticket-sentiment-setup.md)
    * Fixed ticket\_body data alias Jinja in get\_ticket\_variables
    * Set get\_escalation\_member found match condition to >= 1 to set first escalation\_email
  * [Windows Patch Deployer](../../documentation/crates/existing-crate-documentation/windows-patch-deployer-crate.md)
    * Convert computer.id to string in generate\_options Jinja
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Enabled force\_all\_users; added input param and updated generate\_options Jinja to return all users
    * Added SuperOps and NinjaOne PSA support with new/updated workflows
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Set success transition status code to 1000 in halo\_psa\_list\_users
  * [Run Powershell Script on Selected Devices](../../documentation/crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md)
    * Updated ASIO task transition condition in RMM selection action
  * [Rewst Microsoft GDAP Assistant](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
    * Added get\_delegated\_admin\_relationships to Get GDAP Settings; merged with CSP results
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Hatz AI integration
* CIPP Alert Triage Crate
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-03-06" %}
## 💻 March 6, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Optimized webhook trigger performance by replacing synchronous GraphQL calls with direct database queries and Redis-based trigger caching.
  * Updated the Core Webhook trigger Secret Key field description to clarify that it is recommended—not required—for Wait for Results functionality.
* **General**
  * Fixed org picker breadcrumbs so they consistently displayed the correct full organization path across navigation and search states.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Resolved an issue where the hard delete cron job failed to remove workflows and orphaned subworkflow actions, causing engine crashes when deleting soft-deleted organizations.
* **Integrations**
  * Restored N-able N-sight option refreshing so client mappings loaded correctly for integrations using XML-based API responses.
  * Fixed Google domain-wide delegation token exchange failures that prevented non-admin users from accessing supported Google Workspace APIs like Gmail and Drive.
  * Fixed an issue where MySQL connections using SSL failed, preventing successful queries through the SQL integration.
  * Fixed an issue where the List Integrations for Organization action failed when run at the parent organization level.
  * Updated ImmyBot actions to include newly required API parameters, resolving workflow failures caused by recent ImmyBot API changes.
  * Updated the OpenAI action to use the `v1/responses` endpoint, restoring compatibility with current OpenAI models.
* **Jinja**
  * Fixed `parse_csv` so provided `fieldnames` are correctly applied when parsing lists of string lists, instead of treating the first row as headers.
* **App Builder**
  * Improved custom domain validation by removing the “Unknown Error” message and displaying clearer feedback when reserved domains are used.
* **General**
  * Added analytics tracking for guided onboarding
*   **Crates**

    * [Amend Mailbox Permissions](../../documentation/crates/existing-crate-documentation/amend-mailbox-permissions-crate.md)
      * Updated to use \[REWST - OPT GEN] Get Mailbox Folder Permissions instead of \[ROC] version
      * Microsoft Exchange actions now run as org
      * Disabled template trigger using \[ROC] Amend Mailbox Permissions form
    * [Google: User Offboarding](../../documentation/crates/existing-crate-documentation/google-user-offboarding-crate.md)
      * Reordered tasks: run check\_mailbox\_access and grant\_mailbox\_access before disabling user attributes
    * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
      * Added check to ensure user has a mailbox before adding shared mailboxes
      * Added mail\_only\_user input to User: List; when true, route to m365\_list\_users
      * Added SuperOps and NinjaOne PSA support; new List Company Locations/Upsert Contact workflows; updated PSA tasks Upsert Contact, List Company Locations, and List Contact Types

    **Kits**

    * There were no updates to kits this week.

    **Subworkflows**

    * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* RoboRewsty AI Workflow Builder
* Side navigation update
* Lexful Integration
* CIPP Alert Triage Crate
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-02-20" %}
## 💻 February 20, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Senteon - [Documentation](../../documentation/integrations/integration-guides/senteon-integration.md)
  * Moved the Ingram Micro Cloud Marketplace integration from the AI category to CSP Licensing to improve discoverability and correct categorization on the integrations page.
  * Enhanced CW ASIO scope management by adding support for custom scopes while preserving default behavior to prevent authentication failures when new scopes are introduced.
* **Onboarding**
  * Updated onboarding button labels and supporting copy for improved clarity, including revised resume, setup, and completion CTAs and expanded organization variable messaging.
* **General**
  * [Webhook trigger rate limiting](https://docs.rewst.help/security/webhook-trigger-rate-limits)

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Blocked exposure of secret organization variables by preventing user-supplied Jinja in workflow inputs and outputs from unredacting sensitive values.
  * Added exception handling and telemetry for unexpected publish failures so task publishing errors were logged with workflow and task context instead of failing silently.
  * Fixed workflow version history to properly retain and restore previous data alias values when only the alias value is changed and saved.
  * Ensured background workflow actions continue processing even if one post-save step fails, improving overall workflow reliability.
* **Forms**
  * Restored organization list loading for Forms role users when using the Rewst integration in form dropdowns.
* **Crate Marketplace**
  * Improved marketplace crate description parsing to prevent blank descriptions and ensure the correct summary displays across legacy and new templates.
* **Integrations**
  * Fixed an issue with the IT Glue integration where applying filters caused errors and prevented clients from refreshing or loading correctly.
  * Corrected Microsoft CSP customer lookups so List/Get actions returned full customer details even when customers were not mapped to a Rewst organization.
  * Extended Addigy device search pagination so workflows could return more than 500 devices when larger inventories were present.
* **Onboarding**
  * Updated Microsoft GDAP Assistant crate visibility to always display when CSP is selected and enable only after required prerequisites are completed, with real-time progress indicators and checklist tracking.
* **App Builder**
  * Fixed an issue preventing App Builder apps from fully cloning or importing, ensuring all pages and workflows transfer successfully within the same tenant and across environments.
* **General**
  * Fixed an issue where restoring an organization did not properly re-associate it with its parent and could result in unexpected logout behavior.
*   **Crates**

    * [Assign Autotask Configuration Contact Based on Last Logged In User](../../documentation/crates/existing-crate-documentation/assign-autotask-configuration-contact-based-on-last-logged-in-user-crate.md)
      * Created sub-workflow for item failures; added condition to pull active configurations and contacts with email addresses
    * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
      * Added correct options generator for Exchange Server dropdown
      * Added ticket-handling tasks and gating to avoid updates to non-existent tickets; creates/branches appropriately
      * Added employee\_id support to form and workflows
      * Product name for `CPC_E_4C_16GB_128GB` in Pax8 license lookup template corrected
      * Made device lookups case-insensitive
      * Fixed creation/linking of new contacts to correct company in ConnectWise
    * [Traveling Employee CA Policy](../../documentation/crates/existing-crate-documentation/traveling-employee-ca-policy-crate.md)
      * Added update/delete in Self-Serve; improved location detection; support updating country/assigned users; added Time Entry org variable; allow policy deletion
    * [Add or Remove Group Membership](../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
      * Added pagination to `list_user_group_membership` action
    * [Reset Locked Accounts](../../documentation/crates/existing-crate-documentation/reset-locked-accounts-crate.md)
      * Ensured workflow completes cleanly and reports "No locked accounts found" on empty results
      * Implemented revised PowerShell logic to return locked-out users
    * [Alert on Unused M365 Licenses](../../documentation/crates/existing-crate-documentation/alert-on-unused-m365-licenses-crate.md)
      * Adjusted Jinja to complete successfully or fail with clear notification
    * [Billing Count Report](../../documentation/crates/existing-crate-documentation/billing-count-report-crate.md)
      * Adjusted Jinja to correctly aggregate Pax8 license quantities
    * \[Deprecated] M365 CSP/GDAP Permission Checker - update to old version of Crate still in use with some customers
      * Add option to set org var gdap\_list\_all\_tenants=true to include tenants with expired admin relationships

    **Kits**

    * There were no updates to kits this week.

    **Subworkflows**

    * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* RoboRewsty AI Workflow Builder beta
* CIPP Alert Triage Crate
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-02-13" %}
## 💻 February 13, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Organizations**
  * Improved auto-generation of organization slugs to automatically handle reserved words and prevent creation errors.
* **General**
  * Improved authentication performance by adding a database index on `users.sub` to eliminate sequential scans on every request.
* **Crates**
  * [Rewst CA Policy Assistant Crate](../../documentation/crates/existing-crate-documentation/rewst-ca-policy-assistant-crate.md) - This Crate contains a form that retrieves parent tenant sign-in error logs from the last 14 days and emails a list of all enabled Conditional Access policies, with a link to each for easy navigation to the policy in Microsoft Entra.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Fixed a canvas crash by resolving a missing `onDeleteTrigger` reference so Workflow Settings open correctly from the gear icon.
  * Fixed an issue where action boolean dropdown selections in workflows reverted to False, ensuring selected values (including None) persist correctly.
* **App Builder**
  * Fixed custom domain provisioning to properly handle Caddy API failures, ensuring errors are logged and retried instead of silently failing.
* **Forms**
  * Fixed an issue where fields removed from a Form Org Instance were incorrectly re-enabled after saving changes to the parent form.
  * Fixed number input fields so manually typed values correctly trigger Jinja-based form conditions without requiring arrow button interaction.
* **RoboRewsty**
  * Fixed document indexing of Rewst docs to improve RoboRewsty knowledge base.
* **General**
  * Fixed engine restart republishing to avoid looping on the same unacknowledged database notification, reducing noise and improving notification recovery.
  * Expanded custom event tracking for improved behavioral metrics.
*   **Crates**

    * [Reset Locked Accounts](../../documentation/crates/existing-crate-documentation/reset-locked-accounts-crate.md)
      * Ensures workflow completes and outputs "No locked accounts found" for empty result sets
      * Implemented revised PowerShell logic to return locked-out users
    * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
      * Device lookups are now case-insensitive
      * Resolved issue creating contacts and linking to the correct company in ConnectWise
      * Updated Raw JSON for create contact; added int to company and fixed firstName typo
      * Added Kaseya VSA X integration override
    * [Alert on Unused M365 Licenses](../../documentation/crates/existing-crate-documentation/alert-on-unused-m365-licenses-crate.md)
      * Adjusted Jinja to ensure clear success/failure and user notification
    * [Billing Count Report](../../documentation/crates/existing-crate-documentation/billing-count-report-crate.md)
      * Adjusted Jinja to correctly aggregate Pax8 license quantities
    * [Alert on Expiring App Reg Certificates](../../documentation/crates/existing-crate-documentation/alert-on-expiring-app-reg-certificates-crate.md)
      * Edited Jinja to build objects for each app–cert pair and those with expiring certs
    * [Google: User Onboarding](../../documentation/crates/existing-crate-documentation/google-user-onboarding-crate.md)
      * Added loop\_current variable and incremented it each iteration
    * [Document BitLocker Information](../../documentation/crates/existing-crate-documentation/document-bitlocker-information-crate.md)
      * Changed online agent check to != 0 to include non-offline statuses
    * [Use AI to Suggest Responses to New Tickets](../../documentation/crates/existing-crate-documentation/use-ai-to-suggest-responses-to-new-tickets-crate.md)
      * Updated Jinja for setting the Anthropic model in set\_model
    * [PSA: Update Ticket with New User Onboard Links](../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-onboard-links-crate.md)
      * Added check\_form\_name\_input to subworkflow; main workflow handles subworkflow failure with custom note; added static form name defaulting to Rewst Onboarding and Offboarding names
    * [Upload File to PSA Ticket](../../documentation/crates/existing-crate-documentation/upload-file-to-psa-ticket-crate.md)
      * Changed Jinja for publish field default to CTX.publish\_type|d("1", true)
    * [Update User Attributes (On-Prem/Azure) v2](../../documentation/crates/existing-crate-documentation/update-user-attributes-on-prem-azure-v2-crate.md)
      * Added success alias for the success output variable
    * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
      * Added minutes-worked timing from automation\_task\_offboard\_user\_time for final ticket notes
      * For AD-synced environments, restore shared mailbox if disabled user is moved to an unsynced OU
      * Revised Jinja to filter agreements by name and company ID
    * [Rewst Microsoft GDAP Assistant](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
      * Set Force Delegated Admin to True for create\_admin\_relationship and activate\_invite actions

    **Kits**

    * There were no updates to kits this week.

    **Subworkflows**

    * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* [Webhook trigger rate limiting](https://docs.rewst.help/security/webhook-trigger-rate-limits) - February 17th
* RoboRewsty AI Workflow Builder beta
* CIPP Alert Triage Crate
* CIPP Microsoft Desired State Standards Compliance Crate

</details>
{% endupdate %}

{% update date="2026-02-06" %}
## 💻 February 6, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Re-enabled safety check that stops the system from creating triggers for organizations that are disabled or deleted.
* **General**
  * Piloting - Guided Onboarding

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Prevented saving triggers with empty or whitespace-only names when using the Test Trigger Criteria dialog.
* **App Builder**
  * Fixed DomainAppSession cookies to expire correctly, reducing the risk of unauthorized access from stale sessions.
  * Removed AppSession and cookie tokens from App Builder page props to prevent exposing JWTs in client-side HTML.
* **Integrations**
  * Ensured headers and body parameters were persisted when reopening the Microsoft Graph Batch Beta Graph API Request action.
* **General**
  * Enhanced performance metric observability.
  * Added metric tracking for RoboRewsty.
  * Updated app dependencies.
* **Crates**
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Only AD sync when IDP is `on_prem` with ADSync; otherwise skip
    * Fix OneDrive Owner permission grant errors - objectNotSupported/400
    * Ticket Number options: `psa_company_id` now populated from PSA Child Company form field
  * [Clean up Global Address List from Disabled Users](../../documentation/crates/existing-crate-documentation/clean-up-global-address-list-from-disabled-users-crate.md)
    * Exclude shared mailboxes from GAL removal
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Check for existing license before purchasing; sequence M365 licensing steps
    * Add CW ASIO to Run PowerShell via RMM; create ConnectWise ASIO: Run PowerShell workflow
    * Add ArrowSphere licensing logic and subworkflows
    * Fix check\_time logic in PSA Update Ticket subworkflows: Halo, ConnectWise PSA, Autotask, Kaseya, ServiceNow based on `no_ticket_time` flags
    * Remove divide-by-60 in `calculate_ticket_time`
    * Update `determine_provider` to honor PSA `mail_only` flag; used across crates
  * [Amend Calendar Permission on User](../../documentation/crates/existing-crate-documentation/amend-calendar-permission-on-user-crate.md)
    * Align structure with updated workflow; correct permission checks
  * [Run Powershell Script on Selected Devices](../../documentation/crates/existing-crate-documentation/run-powershell-script-on-selected-devices-crate.md)
    * Add ConnectWise ASIO to On-Prem Run PowerShell on Org Domain Controller
  * [Billing Count Report](../../documentation/crates/existing-crate-documentation/billing-count-report-crate.md)
    * Add ConnectWise ASIO
  * [CW PSA: Pod Technician Toolbox V2](../../documentation/crates/existing-crate-documentation/cwm-technician-toolbox-via-pod-1.md)
    * Add ConnectWise ASIO to RMM: Get Computer
  * [Rotate Local Workstation Passwords](../../documentation/crates/existing-crate-documentation/rotate-local-workstation-passwords-crate.md)
    * Add ConnectWise ASIO to RMM: List Workstation
  * [Automation Toolkit](../../documentation/crates/existing-crate-documentation/automation-toolkit-crate.md)
    * Add ConnectWise ASIO to RMM: List Child Sites
  * [Install Acronis Backup Agent on Devices](../../documentation/crates/existing-crate-documentation/install-acronis-backup-agent-on-devices-crate.md)
    * Add ConnectWise ASIO to RMM: List Installed Softwares
  * [Document Group Details V2](../../documentation/crates/existing-crate-documentation/document-m365-groups-setup.md)
    * Check `group_members` before match\_hudu\_contact
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Update M365: Get License Groups to include assignedLicenses, filter groups with assigned licenses
  * [Traveling Employee CA Policy](../../documentation/crates/existing-crate-documentation/traveling-employee-ca-policy-crate.md)
    * Add trigger overrides to all four triggers in the Crate
  * Add Rewst Form Link to Offboarding Request Tickets - deprecated Crate
    * Update custom Jinja transition to include Autotask PSA; rename transition
* **Kits**
  * [\[Kit\] Billing Count Reporting](../../documentation/automations/kits/billing-count-kit.md)
    * Add ConnectWise ASIO integration
  * [\[Kit\]: HaloPSA Integration](../../documentation/automations/kits/halo-psa-integration-kit.md)
    * Modify ticket type ID assignment to require psa\_alert\_ticket\_type; subworkflow used in multiple Crates
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Webhook trigger rate limiting
* Rewst CA Policy Assistant Crate

</details>
{% endupdate %}

{% update date="2026-01-30" %}
## 💻 January 30, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Marketplace**
  * Added functionality to display integrations for crates, improving marketplace filtering and prerequisite visibility.
* **General**
  * Displayed current Rewst version in profile menu
  * Removed notification bell from navigation
* **Integrations**
  * Standardized the Datto Autotask integration name to **Autotask PSA** across the platform to reduce confusion and improve consistency.
* **RoboRewsty**
  * Added Extended Thinking streaming for RoboRewsty on Claude (Anthropic API and AWS Bedrock), enabling a toggleable reasoning view without persisting it to the database.
* **Workflows**
  * Added tracking for workflow creation events across all creation methods to improve visibility into automation adoption.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Authentication**
  * Fixed Google SSO logins in the Asia region that could fail with “Not Authorized – User not found” after successful authentication.
* **Marketplace**
  * Fixed an issue where crates failed to unpack for organizations with previously deleted sub-orgs by correctly resolving organization references during trigger creation.
  * Fixed clone syncing failures for workflows with large numbers of clones, preventing interrupted syncs and ensuring updates complete across all organizations.
* **Workflows**
  * Fixed an error that prevented saving or enabling cloned/unpacked triggers (“filterValidOrganizations is not a function”).
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Align license\_subscription variable naming with form and subworkflow
    * Uncheck `create_contact_in_psa` by default when Advanced PSA Options is hidden
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Rename Datto PSA references and workflow names to Autotask to match branding update
  * [Time Savings Report](../../documentation/crates/existing-crate-documentation/time-savings-report-crate.md)
    * Rename variable configs and set cron defaults to avoid overriding form inputs
  * [Configure Out Of Office on Mailbox](../../documentation/crates/existing-crate-documentation/configure-out-of-office-on-mailbox-crate.md)
    * Update run-as org Jinja for `create_ticket` action
  * [Alert on Low Disk Space](../../documentation/crates/existing-crate-documentation/alert-on-low-disk-space-crate.md)
    * Add pre-check so `generate_tickets` runs only when `drives_low_freespace` is not empty
  * [Alert on Login from Non-Native Country](../../documentation/crates/existing-crate-documentation/alert-on-login-from-non-native-country-crate.md)
    * Fix description to correctly reference the crate in docs
  * [Amend Calendar Permission on User](../../documentation/crates/existing-crate-documentation/amend-calendar-permission-on-user-crate.md)
    * Add default board ID to M365 Set Calendar Permissions create ticket action
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Onboarding indicators
* Webhook trigger rate limiting
* Rewst CA Policy Assistant Crate

</details>
{% endupdate %}

{% update date="2026-01-23" %}
## 💻 January 23, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Updated Connectwise Asio setup instructions
  * Updated the ServiceNow integration to allow access to all relevant tables and API endpoints, removing the previous limitation to a single customer table.
* **Crates**
  * [Traveling Employee CA Policy Crate](../../documentation/crates/existing-crate-documentation/traveling-employee-ca-policy-crate.md)
  * [Rewst Microsoft GDAP Assistant Crate](../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Resolved an issue where searching for actions in the workflow editor was taking much longer than expected, restoring fast and responsive search results.
  * Fixed an issue where unpublished workflow canvas changes could be lost when updating inputs or outputs before publishing.
* **Integrations**
  * Improved security for the Microsoft Cloud bundle by ensuring the initial refresh token is no longer exposed unencrypted during setup.
  * Fixed an issue where custom integration actions could disappear from the integration editor while still appearing in workflows, ensuring all actions are consistently visible and editable.
  * Resolved an issue where the CIPP integration connectivity test could return a false 403 error during setup, even though the integration worked correctly in workflows.
  * Fixed an issue in Custom Integrations where integrations with working pagination did not appear as available for org mapping, allowing pagination and org mapping to be used together correctly.
  * Enhanced OAuth2 support for Custom Integrations with expiration-aware token refresh, automatic retry on auth failures, and a manual “Clear Token Cache” option to prevent workflow disruptions.
  * Fixed an issue where selecting an alternate IT Glue configuration in the integration settings did not persist, allowing users to switch between multiple IT Glue instances correctly.
  * Fixed an issue where creating a Kaseya VSA agent install package could fail or cause workflows to hang, ensuring the Machine Group ID is handled correctly and workflows complete as expected.
* **RoboRewsty**
  * Fixed a Redis cache key collision between Jinja filter documentation endpoints by isolating cache keys and applying consistent TTLs, preventing GraphQL “Expected iterable” errors.
  * Fixed an issue where RoboRewsty chat messages could appear more than once in a conversation.
* **App Builder**
  * Fixed an issue where the App Builder logout button did not properly sign users out
  * Fixed an issue where cloned App Builder apps loaded the wrong scripts in templates, causing pages to render incorrect code after cloning or syncing.
  * Fixed an issue where App Builder buttons with “Refresh on Click” enabled could cancel workflow execution, ensuring workflows now start before the page refreshes.
  * Fixed a crash in App Builder Theme Settings when clearing or entering an invalid hex color, ensuring the color picker now handles bad input gracefully.
  * Updated the default App Builder sign-in page to use Microsoft’s official “Sign in with Microsoft” wording and icon, improving branding consistency and user clarity for new apps.
* **Triggers**
  * Fixed an issue where soft-deleted or disabled organizations could block trigger operations (including tag-based triggers and crate unpacking) by ensuring trigger instances are only created for active organizations.
* **General**
  * Fixed an issue where dropdown fields on the tables could truncate text at 1920×1080 resolution, ensuring options remain fully visible and readable.
  * Improved first-time login error handling so users without an invite are routed to a clearer “No Invite” page (showing the attempted email) instead of the generic fallback error.
  * Added dual-project Amplitude tracking with dynamic config so new custom events can be safely tested in a sandbox project and promoted to production analytics only when approved.
* **Crates**
  * [Document M365 Environment](../../documentation/crates/existing-crate-documentation/document-m365-environment-setup.md)
    * Replaced deprecated Microsoft licensing download endpoint with a template; removed endpoint tasks and updated all references
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Expanded ISO 3166 country code data; added workflow to look up ISO codes; added usage\_location input and updated AD user tasks to reference new ISO values
    * Updated Device Name field logic in \[REWST - PROC] User: Change Password to include primary/preferred domain controller org variables
    * Added validation to ensure SQL integration is installed and db\_override is enabled before proceeding
  * Rewst: User Onboarding - deprecated Crate updated to support customers using legacy versions
    * Updated Get Subscribed Products sub-workflow to use a SKU template instead of pulling from Microsoft; affects older onboarding forms
* **Kits**
  * There were no updates to kits this week.
* **Subworkflows**
  * \[REWST - TASK] CW Control: Run Powershell - used by every Crate that works with RMM integrations
    * Added logging to check\_if\_device\_name\_id noop and old\_find\_session\_groups

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Onboarding indicators
* Webhook trigger rate limiting
* Traveling Employee CA Policy Form Crate
* GDAP Crate Improvements for easier setup of the Microsoft Cloud Integration Bundle

</details>
{% endupdate %}

{% update date="2026-01-16" %}
## 💻 January 16, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * New integration - Connectwise Asio
  * Added Generic action for Twilio
  * Added new OpenText Secure Cloud actions to let you view and manage customer services and subscriptions directly in Rewst.
  * Added the Microsoft category back to integrations, making Microsoft-related integrations easier to find and organize.
  * Improved OAuth2 handling for custom integrations by refreshing tokens based on their actual expiration and adding a way to clear cached tokens to prevent workflow failures.
  * Updated the NinjaRMM integration branding to NinjaOne and added PSA categorization, with no impact to existing workflows.
* **RoboRewsty**
  * Added approval flow when querying services.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Workflows**
  * Fixed an issue where cloned workflow transitions could incorrectly reconnect to the same action after reopening a workflow.
  * Fixed an issue where large organizations could hit database limits when loading action options, improving reliability for high-volume accounts.
* **Integrations**
  * Fixed an issue where the Datto PSA “suggest matches” feature could fail with service errors for large accounts, restoring reliable matching.
  * Fixed an issue where custom integration refreshes did not respect paging settings, ensuring all records are correctly retrieved.
  * Fixed an issue where GraphQL user invite actions failed when passing valid boolean values.
  * Fixed an issue where pagination settings prevented org mapping from being available in CIv2 integrations.
  * Fixed an issue where the ConnectWise Manage integration could show errors when saving configuration, even with valid credentials.
  * Fixed an issue where the N-able N-sight integration could fail when refreshing options or listing clients.
  * Fixed an issue where Microsoft Exchange pagination could stop early, ensuring all results are returned consistently.
  * Fixed an issue where older Dropsuite integration configurations could stop working unexpectedly, preventing unnecessary re-authentication.
  * Fixed an issue where the Microsoft Cloud integration could show an incorrect or missing app registration link in the setup page.
  * Fixed Microsoft CSP customer actions so they return complete and correct customer data, including customers not yet mapped to Rewst organizations.
  * Fixed the Proofpoint statistics action to use the correct API parameters so it returns accurate and complete reporting data.
* **RoboRewsty**
  * Fixed an issue where RoboRewsty conversations could fail to start due to a Redis error, improving reliability during conversation setup.
  * Improved RoboRewsty startup performance by caching prompt data, reducing repeated API calls during agent initialization.
* **App Builder**
  * Fixed an issue where App Builder custom components could lose link URLs and icons when reused on new pages.
* **Triggers**
  * Reduced unnecessary system notifications by only sending trigger update events when meaningful changes occur, improving performance and stability.
* **Forms**
  * Removed technical data-type labels from form input fields to make Forms clearer and easier to use for non-technical users.
* **Crate Marketplace**
  * Fixed an issue in the Crate Marketplace where Microsoft integration links now correctly point to the Microsoft bundle instead of individual integrations.
* **General**
  * Fixed the Profile menu Settings link so it correctly opens Settings for the active organization instead of an error page.
  * Improved browser support and build reliability by updating supported browser targets and resolving outdated dependency warnings.
  * Improved icon button visibility across administrative pages and modal components by fixing color contrast issues in the theme.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Altered Device Name field Jinja to use org primary/preferred domain controller
    * Added validation for SQL integration installed and db\_override enabled
    * Renamed "Azure AD" to "Entra ID"; add/align input labels; require last name, username, and email domain
    * Added complete automation log as final PSA ticket note for audit trail
  * [Automation Toolkit](../../documentation/crates/existing-crate-documentation/automation-toolkit-crate.md)
    * Changed crate visibility from private to public
  * [Export Org Vars to CSV for Import](../../documentation/crates/existing-crate-documentation/export-org-vars-to-csv-for-import-crate.md)
    * Switched transition condition to email in check\_documentation\_type; set END criteria to 1
  * [Remove Malicious Email and Block Sender](../../documentation/crates/existing-crate-documentation/remove-malicious-email-and-block-sender-crate.md)
    * Added email\_list defined check and graceful failure path; set End sensitivity to 1
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Fixed anchor mailbox issue; no longer a required input
  * [Just-In-Time Admin Access](../../documentation/crates/existing-crate-documentation/just-in-time-admin-access-crate.md)
    * Set Temporary Password to Always Skip Cached to prevent reuse
  * [Document Group Details v2](../../documentation/crates/existing-crate-documentation/document-m365-groups-setup.md)
    * Added check for group members to avoid failure when none matched
* **Subworkflows**
  * [Halo PSA: Update Ticket](../../documentation/automations/subworkflows/rewst-task-halo-psa-update-ticket.md)
    * Linked add\_public\_note success to complete workflow noop
  * [Halo PSA: Create Ticket](../../documentation/automations/subworkflows/rewst-task-halo-psa-create-ticket.md)
    * Added tech\_id input; default Agent ID from ORG.VARIABLES.psa\_default\_tech\_id when null
* **Kits**
  * There were no updates to kits this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Onboarding indicators
* Traveling Employee CA Policy Form Crate
* GDAP Crate Improvements for easier setup of the Microsoft Cloud Integration Bundle

</details>
{% endupdate %}

{% update date="2026-01-09" %}
## 💻 January 9, 2026 - Dev update

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Added a generic Huntress API request action to allow calling endpoints not covered by existing integration actions.
  * Implemented organization mappings for the Cloudmore integration to enable proper organization configuration.
  * Added support for the new Datto Autotask Australia 3 (ww29) data center option so customers can select the correct endpoint.
  * Improved ConnectWise PSA opportunity creation to safely handle empty or optional nested fields and prevent API errors during workflow execution.
  * Updated the SQL Database integration to support standard multi-tenancy, secure encrypted credentials, proper transaction handling, and modern async database drivers.
* **Database**
  * Implemented locking and caching improvements to reduce Postgres lock durations and improve workflow and dashboard throughput.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

* **Integrations**
  * Fixed action param type casting for nested objects within arrays to ensure values are converted according to their defined schema.
  * Fixed the HaloPSA “Add or Update Assets” action to include support for asset fields, aligning it with API capabilities.
  * Fixed Microsoft CSP customer dynamic dropdown options to prevent errors when loading mapped customers in forms.
  * Fixed Arrowsphere order creation by cleaning up empty nested product objects and correcting YAML schema types to prevent API errors and documentation failures.
  * Fixed the SuperOps “New Ticket Record” trigger to include ticket context data so workflows can reference and act on the triggering ticket.
  * Fixed the Bitdefender “List Endpoint” action to return endpoints for the specified client organization when a parentId is provided.
  * Fixed the GraphQL updatePage mutation to include the site reference during permission checks, allowing existing pages to be updated successfully.
  * Preserved certificate newlines in the SQL integration to ensure valid PEM formatting.
  * Fixed Kaseya BMS API retries by capping Retry-After delays to prevent long-running sleep loops and unresponsive workflows.
* **RoboRewsty**
  * Fixed RoboRewsty message looping and added request resume functionality to improve chat persistence and reconnection across refreshes and tab changes.
  * Improved RoboRewsty chat bubble styling in light mode to increase contrast, readability, and overall visual clarity.
  * Fixed RoboRewsty chat scrolling so mouse wheel actions no longer scroll the background page.
* **Triggers**
  * Fixed workflow triggers so disabled organizations are no longer selected or executed when using “All current and future orgs."
  * Fixed the Trigger Version Control dialog so trigger version history opens correctly without errors.
* **Jinja**
  * Fixed inconsistent Jinja evaluation for action transition data aliases so results match regardless of whether aliases are set on the action or a separate noop.
* **Forms**
  * Fixed multi-select form default behavior so previous selections are cleared when dynamic options return no default values.
* **General**
  * Updated Statsig dynamic config retrieval to run asynchronously in an executor, preventing event loop blocking and improving performance.
* **Crates**
  * [Microsoft: User Onboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
    * Use email as UPN to prevent incorrect user assignment
    * Enable mail\_nickname input on the form for on‑prem environments
    * Use specified\_share\_server as device\_name when provided; fix variable typo
    * Update ticket with correct password info during onboarding
    * Add transition to set description to external\_note when internal\_note task runs
    * Re-sync Create User task to apply run\_ad\_sync logging fix
    * Add transition for override list in set\_output\_var
    * Change work\_minutes filter type from int to float in final ticket updates
    * Updated datto\_ticket\_number input description to "Datto Ticket Number"
    * Added ability to post private/internal notes to existing SuperOps and NinjaOne tickets
    * Implemented updating of an existing NinjaOne ticket
    * Added ability to create new NinjaOne tickets with org default values
  * [Add or Remove Group Membership](../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
    * Fix empty user list by updating the form
    * Add 'groups-aad' option to manage\_users\_or\_groups
  * [PSA: Update Ticket with User Offboard Links](../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-offboard-links-crate.md)
    * Update trigger to support orgs using items or not
  * [Configure Organizational Variables](../../documentation/crates/existing-crate-documentation/configure-organization-variables.md)
    * Add "Created Offboarding Ticket" form item; update Options Gen/ORG variable logic for psa\_offboarding\_user\_ticket\_item
    * Add FR and NZ to M365 Usage Locations options
    * Added field for requester ID for SuperOps to the \[ROC] Rewst: Simple Organizational Variable Form for Child Accounts form
  * [PSA: Update Ticket with New User Onboard Links](../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-onboard-links-crate.md)
    * Update trigger to support with/without items
  * [Enterprise Application Creation Alert](../../documentation/crates/existing-crate-documentation/enterprise-application-creation-alert-crate.md)
    * Add input mapping to ticket\_type\_id in create\_psa\_service\_ticket action
  * [Document Rewst Org Variables](../../documentation/crates/existing-crate-documentation/document-rewst-org-variables-crate.md)
    * Add Getting Started tag to this crate; remove it from Rewst: User Onboarding
  * [Report on Disabled M365 Users with Licenses](../../documentation/crates/existing-crate-documentation/report-on-disabled-m365-users-with-licenses-crate.md)
    * Use trigger type name "Webhook" instead of ID in condition
  * [Microsoft: User Offboarding](../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
    * Use user\_filter input instead of hardcoded asterisk (\*)
  * [Billing Count Report](../../documentation/crates/existing-crate-documentation/billing-count-report-crate.md)
    * Wrap CTX.id in array for auvik\_list\_devices\_info/details input handling
  * [Bulk Create Client from PSA](../../documentation/crates/existing-crate-documentation/bulk-create-client-from-psa-crate.md)
    * Add SuperOps support in Stage 2: Create Organisations
  * [Reset Microsoft MFA](../../documentation/crates/existing-crate-documentation/reset-microsoft-mfa-crate.md)
    * Made Ticket ID a dynamic dropdown; added "Skip Ticket Creation" checkbox to guide correct workflow path
  * [Cork: Compliance Event to PSA Ticket](../../documentation/crates/existing-crate-documentation/cork-compliance-event-to-psa-ticket-crate.md)
    * Updated filter to include only tickets with a resolved date and status not 1–4
  * [M365: Disable Inactive User Accounts](../../documentation/crates/existing-crate-documentation/m365-disable-inactive-user-accounts-crate.md)
    * Added required PSAs and RMMs as associated packages
  * [Change a User's Password](../../documentation/crates/existing-crate-documentation/change-a-users-password-crate.md)
    * Added PSAs and RMMs as associated integrations on the crate details page
* **Workflows**
  * \[REWST - TASK] Agent Smith: Run Powershell
    * Move output data alias from query\_device 404 to retry max-retries transition
  * \[REWST - TASK] SuperOps: Create Ticket
    * Default technician and requester to None in create\_ticket action for this subworkflow in our ticket creation subworkflow, used whenever we create a ticket in any Crate

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Connectwise ASIO integration
* Enhanced logging for the user onboarding workflow
* Various DropSuite Additions
* Traveling Employee CA Policy Form
* GDAP Crate Improvements

</details>
{% endupdate %}
{% endupdates %}
