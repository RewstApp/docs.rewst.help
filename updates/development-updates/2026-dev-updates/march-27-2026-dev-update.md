# March 27, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Hatz AI integration - documentation found [here](../../../documentation/integrations/integration-guides/hatz-integration.md)
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

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* Workflow canvas redesign beta

</details>
