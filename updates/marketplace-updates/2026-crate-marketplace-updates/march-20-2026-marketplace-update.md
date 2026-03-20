# March 20, 2026 - Marketplace update

<details>

<summary><strong>New Crates</strong></summary>

[CIPP Alert Triage Crate](../../../documentation/crates/existing-crate-documentation/cipp-alert-triage-crate.md) - This new Crate automates processing CIPP alerts with tenant/message exclusions, auto creates/updates PSA tickets, and provides a configuration form for per-org mappings and rules.&#x20;

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

### Crates

* [Microsoft: User Onboarding](../../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
  * Updated the Jinja in filter\_product to check for Nonprofit Staff Pricing - New Commerce Experience.&#x20;
* [Alert On Users Without MFA Enforced](../../../documentation/crates/existing-crate-documentation/alert-on-users-without-mfa-enforced-crate.md)
  * Updated `check_trigger_type` to detect webhooks based on the ref attribute.
* [Microsoft Subscription Renewal Alerts](../../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
  * Updated Jinja for `expiring_subscription` to exclude suspended status.&#x20;
  * PSA: Check if Existing Ticket now checks in NinjaOne.
  * Freshdesk and ServiceNow now retrieve existing tickets using closedFlag and Ticket Summary.&#x20;
* [Rewst Microsoft GDAP Assistant](../../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
  * Added CTX.active\_relationships check before withitems to avoid errors when no active relationships exist.
* [Alert on AV/EDR Coverage Gaps](../../../documentation/crates/existing-crate-documentation/alert-on-av-edr-coverage-gaps-crate.md)
  * Fixed newline comment handling and typo; enhanced Create Ticket&#x20;
    * fallback to initial\_description, support assignee\_id; added cc\_emails, tags, initial\_description\_html; use contact\_id, parent\_ticket\_id); removed unnecessary set\_variables and moved company\_id->ORG.VARIABLES.ninja\_org\_id fallback into create\_ticket.&#x20;
* [Microsoft: User Offboarding](../../../documentation/crates/existing-crate-documentation/microsoft-user-offboarding-crate.md)
  * Added conditional: if input has @ use -Filter against UserPrincipalName; else use -Identity for SAMAccountName.
* [Amend Mailbox Permissions](../../../documentation/crates/existing-crate-documentation/amend-mailbox-permissions-crate.md)
  * Disabled custom trigger in \[Rewst] EXO: Manage Mailbox Permissions using \[ROC] Crate and kept the trigger synced from crate-dev.

### Kits

There were no updates to kits this week.

### Subworkflows

There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

CIPP Microsoft Desired State Standards Compliance Crate

</details>

