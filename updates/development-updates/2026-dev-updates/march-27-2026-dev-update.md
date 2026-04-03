# April 3, 2026 - Dev update

Explore what new changes the Dev team has deployed in the last week.

This can be anything from new features, bug fixes, or QoL changes!

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
  * Fixed a crash caused by a TypeError when using 'Suggest Customer Mappings' for Microsoft Cloud Bundle integration.&#x20;
  * Fixed unsaved packs defaulting to all permissions selected on CPV consent in Microsoft Cloud Bundle integration.&#x20;
  * Added a contacts field to the 'Create Company' action in Pax8 integration.&#x20;
* **RoboRewsty**
  * Improved task positioning for tasks added by RoboRewsty.
* **Workflow Builder**&#x20;
  * Preserved large numeric strings that exceed JavaScript precision in object field parsing.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

* New Workflow Builder - currently in select customer beta.

</details>
