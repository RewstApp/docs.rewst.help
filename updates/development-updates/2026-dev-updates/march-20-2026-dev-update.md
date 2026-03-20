# March 20, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

<details>

<summary><strong>New features and items</strong></summary>

* **Workflows**
  * Jinja context viewer - documentation found [here](../../../documentation/jinja/context-viewer.md)
* **Onboarding**
  * Enabled manual override to mark the org mapping onboarding sub-step as complete when 80% mapping cannot be reached due to integration org count differences.
* **Triggers**
  * Added access to the form usages dialog directly from the Trigger View Forms tab to quickly view form URLs without navigating away.

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

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Hatz AI integration

</details>
