---
description: >-
  Implement custom condition transitions in Task Transitions to enable dynamic
  decision-making in workflows, based on the properties of a Microsoft Group.
---

# Getting Object Properties for Microsoft Groups

## Module Overview

:bulb: Certain properties of Microsoft Group objects impact what integration (or what API) we'll use to add someone to that group or remove them from the group. Storing the Group object in a data alias enables custom conditions in transitions to guide the workflow toward the correct integration.

### Video (8:47 _Minutes)_

{% embed url="https://youtu.be/Z6IWP50i9zA" %}



<details>

<summary>Step 1: Adding the "Get Group" Action</summary>

1. **Add** the "get group" action from Microsoft Graph to the top of the workflow.
   * Turn on the "snap to grid" feature for easier alignment
2. **Rename** the action to delete "get\_group", deleting "microsoft\_graph"
3. **Select** the Jinja Editor for the Group ID field
   * Enter `{{ CTX.group_id }}` and close the Jinja Editor
4. **Add** a data alias to the "on success" transition
   * Key: `group`
   * Value: `{{ RESULT.result.data.value }}`

</details>

<details>

<summary>Step 2: Using a Noop for Decision-Making: What "Path" Do We Take From Here?</summary>

1. **Add** a noop below the "get\_group" action
2. **Rename** the noop "check\_group\_type"
3. **Add** 2 more transitions to "check\_group\_type"
4. **Label** the three transitions and place them in the follow order from left to right:
   * Dynamic
   * Graph
   * Exchange Online
5. **Select** the Dynamic transition and add the following custom condition: `{{ "DynamicMembership" in CTX.group.groupTypes }}`
6. **Select** the Graph transition and add the following custom condition: `{{ "Unified" in CTX.group.groupTypes or not CTX.group.mailEnabled }}`
7. **Connect** the Graph transition to the "add\_or\_remove" noop

</details>

### Action Item

* Store the group object in a data alias for easier data management.
* Implement a noop to control the workflow's flow, determining the appropriate action based on the group type.

## Navigation

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center">Go to the previous module:<br><a data-mention href="introduction-to-workflow-logic-microsoft-apis.md">introduction-to-workflow-logic-microsoft-apis.md</a></td><td align="center"></td><td></td></tr><tr><td align="center">Go to the next module:<br><a data-mention href="creating-a-microsoft-exchange-online-path-in-the-workflow.md">creating-a-microsoft-exchange-online-path-in-the-workflow.md</a></td><td align="center"></td><td></td></tr></tbody></table>
