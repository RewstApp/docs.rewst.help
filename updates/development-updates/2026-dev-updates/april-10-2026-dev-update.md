# April 10, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

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

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.
* Ubiquity integration

</details>
