# 104 - Options Generators & Generic API Requests

## Introduction

In Rewst 104, we will delve into the intricacies of option generators and generic API requests. Specifically, we will learn how option generators enhance forms, building upon the knowledge acquired in our Rewst 102 course. Additionally, we will explore generic API requests by integrating Microsoft Graph API, demonstrating its functionality within the Rewst platform. We will also implement list comprehension techniques, building upon the concepts introduced in Rewst 103.

When you've completed this training, [don't forget to get credit](104-options-generators-and-generic-api-requests.md#get-credit)[!](https://app.rewst.io/form/cdeabeb5-7fcb-4695-8534-94af2bcb10f0)

{% hint style="danger" %}
These steps assume you have completed the full steps from Rewst 102 You can find the instructions to make this form on the [<mark style="color:blue;">Rewst 102 Page</mark>](102-building-a-basic-workflow.md)<mark style="color:blue;">.</mark>
{% endhint %}

## Watch the video and follow along with the steps below

{% embed url="https://youtu.be/pkKRidcAHWA" %}

## Get Credit

{% hint style="success" %}
To get credit for completing this session offline, please [submit this form](https://app.rewst.io/form/cdeabeb5-7fcb-4695-8534-94af2bcb10f0).
{% endhint %}

## Follow Along

### Understanding Option Generators

In this course, we will filter groups based on user membership status. When adding a user to a group, only groups the user is a member of will be displayed. Conversely, when removing a user from a group, only groups the user is a member of will be shown. To achieve this, we will utilize option generators, specialized workflows that curate form field options dynamically.

### Part 1: Modifying the Form

We'll start by modifying our existing form from Rewst 102. The group field and add/remove field positions will be switched. When users select a user and the add/remove radio button, these values will be passed to our option generator workflow.

<details>

<summary>Step 1: Modify the Form Created in Rewst 102</summary>

**Open the Form**

1. **Go to** _Automations_ → _Forms_ in the menu.
2. **Search** for the _Add or Remove from AzureAD Group_ Form.
3. **Click** on the Form to Open it.

**Re-order the Form**

1. **Drag and Drop** the _Add or Remove Field_ above _Group_.
2. **Click** the _Save_ button at the top right of the form builder.
3. **Click** _Submit_ on the pop-up to confirm.

</details>

***

### Part 2: Creating the Option Generator

In our next steps, we'll go to the Workflow section. Here, we'll craft a new workflow called "Demo Option Generator for Groups Based on User Membership." This workflow will be configured as an option generator, with specified inputs including user ID and action (add or remove). Moreover, we'll set the output configuration variable as "options" for our subsequent tasks.

<details>

<summary>Step 2: Create a New Option Generator Workflow</summary>

**Create a New Workflow**

1. **Go to** _Automations_ → _Workflows_ in the menu.
   * You can open this in a new tab to make it easier.
2. **Click** _Create_ at the top right to add a new Workflow.
3. **Type** _Option Generator for Groups based on User Membership_ for the name.
4. **Click** Submit.

**Add Output Configuration in Workflow Variables**

1. **Click** on _Configure Workflow Variables_ (The Pencil icon) at the top right of the Menu.
2. **Choose** _Option Generator_ for the _Workflow Type_ dropdown.
3. **Click** on the Add (+) button next to _Output Configuration_ at the bottom.
4. **Type** _options_ for the _Field Name_.
5. **Click** Submit.

**Add Input Configuration Variables**

1. **Click** on the Add (+) button next to _Input Configuration_.
2. **Type** _action_ for the _name_.
3. **Click** _Required_.
4. **Click** on the Add (+) button next to _Input Configuration_ again.
5. **Type** _user\_id_ for the _name_.
6. **Click** _Required_.
7. **Click** Submit.

</details>

<details>

<summary>Step 3: Add the List Member Actions to Option Generator Workflow</summary>

**Add a Core Noop Action to the Canvas**

1. **Drag and Drop** the _noop_ action to the Workflow Canvas.
   * You can find this in the Core section or by searching.
2. **Click** on the _noop_ to open the Details menu.
3. **Click** the edit button next to _core\_noop_.
4. **Rename** the action to _add\_or\_remove_.
5. **Click** _Advanced_.
6. **Choose** the _Follow First_ Transition Mode.

**Create a Transition for Adding a User**

1. **Click** on the default _On Success_ transition on the _add\_or\_remove_ noop.
2. **Type** _Add_ for the _Custom Label_.
3. **Click** the _Custom Condition_ button from the Condition options.
4. **Click** the Source button next to the _Custom Condition_ field.
5. **Type** `{{ CTX.action == "add" }}` in the editor.
6. **Close** the editor.

**Create a Transition for Removing a User**

1. **Click** the Add (+) button next to the _Add_ transition.
2. **Type** _Remove_ for the _Custom Label_.
3. **Click** the _Custom Condition_ button from the Condition options.
4. **Click** the Source button next to the _Custom Condition_ field.
5. **Type** `{{ CTX.action == "remove" }}` in the editor.

**Add a Graph API Request action to List Member Groups**

1. **Drag and Drop** the _Graph API Request_ action to the Workflow Canvas.
   * You can find this in the Microsoft Graph section or by searching.
2. **Click** on the new action to open the Details menu.
3. **Click** the edit button next to the name.
4. **Rename** the action to _list\_user\_groups_.

**Add API Information to the List User Groups Action**

<mark style="color:blue;">It is recommended that you reference the API Docs</mark> [<mark style="color:blue;">These docs are references in this portion of the training</mark>](https://learn.microsoft.com/en-us/graph/api/user-list-memberof?view=graph-rest-1.0\&tabs=http)

1. **Click** the Source button next to the _Endpoint_ field.
2. **Add** `/users/{id | userPrincipalName}/memberOf` from the API docs to the editor.
3.  **Replace** `{id | userPrincipalName}` with `{{ CTX.user_id }}` so it looks like the following:

    ```django
    /users/{{ CTX.user_id }}/memberOf
    ```
4. **Close** the editor.
5. **Click and Drag** the transition from the _add\_or\_remove_ action to the _list\_user\_groups_ action.
   * To do this, you will need to hover over the circle under the _Remove_ section of the action.

**Add a Graph List Groups action to List All Groups**

1. **Drag and Drop** the _List Groups_ action to the Workflow Canvas.
   * You can find this in the Microsoft Graph section or by searching.
2. **Click** on the action to open the Details menu.
3. **Click** the edit button next to name.
4. **Rename** the action to _list\_all\_groups_.

**Add a Data Alias to the List All Groups action**

1. **Click** on the _On Success_ transition.
2. **Click** on the Add (+) button next to _Data Aliases_.
3. **Type** _all\_groups_ as the _key_.
4. **Open** the Source editor.
5. **Add** the following to the editor:

```django
{{ RESULT.result.data.value }}
```

6. **Close** the editor.
7. **Click and Drag** the transition from the _add\_or\_remove_ action to the _list\_all\_groups_ action.
   * To do this, you will need to hover over the circle under the _Add_ section of the action.

**Add a Data Alias to the List User Groups action**

1. **Click** on the _On Success_ transition of _list\_user\_groups_.
2. **Click** on the Add (+) button next to _Data Aliases_.
3. **Type** _group\_list_ as the _key_.
4. **Open** the Source editor.
5.  **Add** the following to the editor:

    ```django
    {{ RESULT.result.data.value }}
    ```
6. **Close** the editor.

**Copy the List User Groups Action**

1. **Click** on the options menu next to the _list\_user\_groups_ action.
2. **Click** _Create Copy_.
3. **Move** it on the Canvas under the _list\_all\_groups_ action.
4. **Drag** the Transition from _list\_all\_groups_ to the _list\_user\_groups_ copy.
5. **Click** on the _On Success_ Transition for the new copy.
6. **Change** the Data Alias from _group\_list_ to _user\_groups_.

**Add a Final Noop to Build the Group List**

1. **Add** a _core\_noop_ action under the _list\_user\_groups_ copy.
2. **Click** on the action to open the Details menu.
3. **Change** the name to _build\_group\_list_.
4. **Click** the _On Success_ Transition.
5. **Click** on the Add (+) button next to _Data Aliases_.
6. **Type** _group\_list_ as the _key_.
7. **Open** the Source editor.
8.  **Add** the following Jinja to the editor:

    ```django
    {{
        [
            group
            for group in CTX.all_groups
            if group.id not in [
                user_group.id
                for user_group in CTX.user_groups
            ]
        ]
    }}
    ```
9. **Close** the editor.

**Add the Final Transition**

1. **Drag** the Transition from _list\_user\_groups_ copy to _build\_group\_list_.
2. **Click** _Publish_.
3. **Click** _Submit_.

</details>

***

### Part 3: Trigger and Integration

Next, we'll first add a trigger, configured to always pass, guaranteeing the workflow's execution when necessary inputs are supplied. Following that, we'll integrate the option generator into the group field within the form. To ensure clarity, we'll specify the display name attribute for the label field, ensuring that the options appear as group names for user selection.

<details>

<summary>Step 4: Update the options Config and add the Trigger</summary>

**Open the Workflow Variables**

1. **Click** on _Configure Workflow Variables_ (The Pencil icon) at the top right of the Menu.
2. **Open** the source editor next to the options _Output Configuration_.
3.  **Type** the following:

    ```django
    {{ CTX.group_list }}
    ```
4. **Click** Submit.

**Add and Configure the Trigger**

1. **Click** _Add Trigger_ in the top menu.
2. **Type** _Option Generator_ for the Name.
3. **Click** the slider next to _Enabled_.
4. **Choose** _Core - Always Pass_ Trigger Type.
5. **Click** the Add (+) button next to _Integration Overrides_.
6. **Choose** _Microsoft Graph_ for the _Integration_ dropdown.
7. **Click** the slider next to _All current and future managed organizations_.
8. **Click** _Submit_.
   * You may need to Click _Cancel_ after to close it.
9. **Click** _Publish_ at the top right of the workflow.
10. **Click** _Submit_.

</details>

<details>

<summary>Step 5: Update the Form to be a Workflow Generated Form</summary>

**Change the Group field to Workflow Generated**

1. **Go to** _Automations_ → _Forms_ in the menu.
   * If you already have another tab open, go back to your form.
2. **Open** the _Add or Remove from AzureAD Group_ Form.
3. **Click** on the _Group_ field.
4. **Click** the slider under _Workflow Generated_.

**Configure the Details of the Workflow Generated Field**

1. **Select** the _Option Generator for Groups based on User Membership_ Workflow from the dropdown.
   1. Refresh the page if the workflow does not appear.
2. **Replace** the _Label Field_ default with _displayName_.
3. **Choose** _Option Generator_ for the Trigger.
4. **Click** _Populate from form field_ under the `action` field.
5. **Choose** `action` from the dropdown.
6. **Click** _Populate from form field_ under the `user_id` field.
7. **Choose** `user_id` from the dropdown.
8. **Click** _Save_.
9. **Click** _Submit_.

**Run the Form to Pull the Options Generator**

1. **Click** on _View Usages_ at the top right.
2. **Click** on the _View Direct URLs_.
3. **Click** on the link.

<mark style="color:red;">⚠️ You will not see the link if you haven't completed Rewst 102 The link shows up because the Workflow built in 102 has the Form set as a trigger. You can find the instructions to make this workflow on the Rewst 102 Page</mark>

</details>

<details>

<summary>Step 6: Test it!</summary>

**Try it for yourself!**

1. **Choose** a User.
2. **Click** Add or Remove.
3. **Check** to see if the groups show correctly!

</details>

***

## Conclusion

Congratulations! You've successfully configured an option generator and implemented logic using generic API requests and list comprehension techniques. With this knowledge, you can enhance your forms and streamline group management.

## Additional Resources

{% hint style="info" %}
For more information on using Options Generators, Generic API Requests, List Comprehension, and more, check out our documentation:

* [Option Generators](../../documentation/workflows/workflow-generated-options.md)
* [Generic API Requests](../../documentation/integrations/cloud/microsoft-cloud-integration-bundle/microsoft-graph/microsoft-graph-integration-setup.md#graph-api-request)
* [List Comprehension](../../documentation/jinja/use-cases-and-best-practices/jinja-lists.md)
* [Diff Lists](../../documentation/workflows/actions-in-rewst/transform-actions/diff-lists.md)
* [Microsoft Graph API](https://learn.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0)
{% endhint %}

## Need more guidance?&#x20;

{% hint style="success" %}
Sign up for our **LIVE** training sessions below!
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><mark style="color:blue;"><strong>Rewst 104</strong></mark></td><td align="center">Options Generators &#x26; Generic API Requests</td><td><a href="https://calendly.com/cluck-u/rewst-104">https://calendly.com/cluck-u/rewst-104</a></td></tr><tr><td align="center"><mark style="color:blue;"><strong>Cluck U Office Hours</strong></mark></td><td align="center">Come and Get Help!</td><td><a href="https://calendly.com/cluck-u/office-hours">https://calendly.com/cluck-u/office-hours</a></td></tr></tbody></table>
