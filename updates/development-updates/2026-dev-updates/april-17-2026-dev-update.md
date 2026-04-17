# April 17, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

<details>

<summary><strong>New features and items</strong></summary>

* **Integrations**
  * Ubiquity Integration - docs found [here](../../../documentation/integrations/integration-guides/ubiquiti-integration.md)
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

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.

</details>
