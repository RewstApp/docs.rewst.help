# April 10, 2026 - Marketplace update

<details>

<summary><strong>New Crates</strong></summary>

No new Crates were released this week.

</details>

<details>

<summary><strong>Bug fixes and chores</strong></summary>

### Crates

* [Reset Locked Accounts](../../../documentation/crates/existing-crate-documentation/reset-locked-accounts-crate.md)
  * Added `runAsOrg` so the subworkflow executes in the suborganization's context and carries the override.&#x20;
* [Rotate Local Workstation Passwords](../../../documentation/crates/existing-crate-documentation/rotate-local-workstation-passwords-crate.md)
  * Added Agent Smith actions to display workstations.
* [Microsoft: User Onboarding](../../../documentation/crates/existing-crate-documentation/microsoft-user-onboarding-crate-v2/)
  * Updated the PAX8 product name for `Microsoft_Teams_Audio_Conferencing_select_dial_out`.&#x20;
* [Add or Remove Group Membership](../../../documentation/crates/existing-crate-documentation/add-or-remove-group-membership-crate.md)
  * Removed the `get_user` action from the workflow.&#x20;
  * Updated the script template to use objectGUID directly instead of retrieving `userOnpremUPN` via the `get_user` Graph action.&#x20;
  * Updated the script template to properly handle multiple values for `onprem_groups_to_remove`.&#x20;
* [CW PSA: Pod Technician Toolbox v2](../../../documentation/crates/existing-crate-documentation/cwm-technician-toolbox-via-pod-1.md)
  * Reduced the number of tasks run before the first pod shows up in ConnectWise.
  * Added new logic for how the link is checked or created.
  * Added a new action to get the tenant ID.&#x20;
* [Rewst Microsoft GDAP Assistant](../../../documentation/crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md)
  * Updated the first two form field descriptions to clarify they are not required but recommended to fully set up the Microsoft integration.

### Kits

There were no updates to kits this week.

### Subworkflows

There were no updates to subworkflows this week.

</details>

<details>

<summary><strong>Coming soon</strong></summary>

CIPP Microsoft Desired State Standards Compliance Crate

</details>

