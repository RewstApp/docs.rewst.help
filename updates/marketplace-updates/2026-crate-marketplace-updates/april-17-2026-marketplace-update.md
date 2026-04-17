# April 17, 2026 - Marketplace update

<details>

<summary><strong>New Crates</strong></summary>

No new Crates were released this week.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

### Crates

* [Microsoft: User Onboarding](../../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
  * Use Domain Controllers filter in List Devices API to narrow search for large orgs.
  * Fixed Send Supervisor Password field: option Gen now sets value to identity; previously EXO GUID caused Send Mail failure.&#x20;
* [AI Ticket Sentiment Analysis](../../../documentation/crates/existing-crate-documentation/openai-ticket-sentiment-setup.md)
  * Added SuperOps support.
* [AI Ticket Categorization](../../../documentation/crates/existing-crate-documentation/openai-ticket-categorisation-setup.md)
  * Added caching for issue types/subtypes to reduce task usage.
* [Rotate Local Workstation Passwords](../../../documentation/crates/existing-crate-documentation/rotate-local-workstation-passwords-crate.md)
  * Script now retrieves all MAC addresses.&#x20;
  * Updated compiled\_assets data alias (Hudu/IT Glue) to update all matched assets by MAC address.&#x20;
* [Agent Smith: Service Provisioning \[Install Second\]](../../../documentation/agent-smith/agent-smith-configuration-overview.md)
  * rewst\_engine\_url alias now uses APP.engine\_url instead of hardcoded value.&#x20;
* [Cork: Compliance Event to PSA Ticket](../../../documentation/crates/existing-crate-documentation/cork-compliance-event-to-psa-ticket-crate.md)
  * Updated SuperOps tickets alias Jinja to filter by superops\_client\_id org variable.&#x20;
* [Microsoft Subscription Renewal Alerts](../../../documentation/crates/existing-crate-documentation/microsoft-subscription-renewal-alerts-crate.md)
  * company\_id for create\_service\_ticket now resolves dynamically by default\_psa across supported PSAs (CW Manage, Datto, Halo, Freshdesk, ServiceNow, Kaseya BMS, SuperOps, NinjaOne).&#x20;
* [PSA: Update Ticket with New User Onboard Links](../../../documentation/crates/existing-crate-documentation/psa-update-ticket-with-user-offboard-links-crate.md)
  * Added org variable setup to both Onboard and Offboard link update crates.&#x20;
* [Use AI to Suggest Responses to New Tickets](../../../documentation/crates/existing-crate-documentation/use-ai-to-suggest-responses-to-new-tickets-crate.md)
  * Datto New Ticket trigger now sends Title, Description, and Queue.&#x20;
* [Sync AzureAD Account Information with ConnectWise PSA Contacts (v3)](../../../documentation/crates/existing-crate-documentation/sync-azuread-account-information-with-connectwise-psa-contacts-v3-crate.md)
  * Removed inline comment causing an error.&#x20;

### Kits

There were no updates to kits this week.

### Subworkflows

There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

CIPP Microsoft Desired State Standards Compliance Crate

</details>

