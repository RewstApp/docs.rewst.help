# April 24, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

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

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.

</details>
