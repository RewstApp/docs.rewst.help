---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 102 - Building a Basic Workflow

## Introduction

Hello and welcome! In this tutorial, we'll guide you through the process of creating automated workflows using Rewst. Our focus will be on creating a form, building an MVP workflow, and connecting the two with a trigger. Follow these steps to build the Add or Remove Users from AD workflow!&#x20;

When you've completed this training, [don't forget to get credit!](https://app.rewst.io/form/38c7d9ca-1606-4a61-872e-884466850287)

## Watch the video and follow along with the steps below

{% embed url="https://youtu.be/MuOTYGS56l4" %}

## Get Credit

{% hint style="success" %}
To get credit for completing this session offline, please [submit this form](https://app.rewst.io/form/38c7d9ca-1606-4a61-872e-884466850287).
{% endhint %}

## Follow Along

### Part 1: Build a Form to Add or Remove Users in AD

We'll start by creating a form to collect the necessary information to pass to the workflow. First, we'll go to the Forms section in Rewst. Next, we'll design the form with fields, and configure the fields to dynamically show us a list of users and groups. And finally, we'll define which variables can be accessed from the workflow for each field. Follow these steps:

<details>

<summary>Steps: Building a Form</summary>

**Add a Form**

1. **Go to** _Automations_ → _Forms_ in the menu.
2. **Click** _Add_ at the top right to add a new Form.
3. **Type** _Add or Remove from AzureAD Group_ for the name.
4. **Click** Submit.

**Add a Dropdown field to Choose a User**

1. **Drag and Drop** a _Dropdown_ field.
2. **Click** on the field to open the field settings.
3. **Type** "user\_id" for the _Field Name_.
4. **Replace** the default _Field Label_ text with "User".
5. **Type** "Choose a User" for the _Field Description_ text.
6. **Click** the _Required_ checkbox.
7. **Click** on the _Dynamic Options_ slider.
8. **Choose** _Microsoft Graph_ for the _Integration_ dropdown.
9. **Choose** _Users_ for the _Resource_ dropdown.

**Add a Dropdown field to Choose a Group**

1. **Drag and Drop** a _Dropdown_ field.
2. **Click** on the field to open the field settings.
3. **Type** "group\_id" for the _Field Name_.
4. **Replace** the default _Field Label_ text with "Group".
5. **Type** "Select a Group" for the _Field Description_ text.
6. **Click** the _Required_ checkbox.
7. **Click** on the _Dynamic Options_ slider.
8. **Choose** _Microsoft Graph_ for the _Integration_ dropdown.
9. **Choose** _Groups_ for the _Resource_ dropdown.

**Add Radio Buttons to identify whether to add or remove users**

1. **Drag and Drop** a _Radio Buttons_ field.
2. **Click** on the field to open the field settings.
3. **Type** "action" for the _Field Name_.
4. **Replace** the default _Field Label_ text with "Add or Remove".
5. **Click** the _Required_ checkbox.
6. **Type** "Add" for the first _Option Label_.
7. **Type** "Remove" for the second _Option Label_.
8. **Click** on the minus (-) button to remove the third option.
9. **Type** "add" for the first _Option Value_.
10. **Type** "remove" for the second _Option Value_.

**Save the form**

1. **Click** the _Save_ button at the top right of the form builder.
2. **Click** _Submit_ on the pop-up to confirm.

</details>

***

### Part 2: Build a Workflow to Add or Remove Users in AD

Next, let's design a workflow that responds to the form submissions. We'll start by going to the Workflow section in Rewst and adding a new workflow. Then, we'll add the actions, including MS Graph actions, to the workflow. Finally, we'll implement transitions based on whether a user is added or removed from a group.

<details>

<summary>Steps: Creating a Workflow</summary>

**Create a New Workflow**

1. **Go to** _Automations_ → _Workflows_ in the menu.
2. **Click** _Create_ at the top right to add a new Workflow.
3. **Type** _Add or Remove User from AzureAD Group_ for the name.
4. **Click** Submit.

**Add the Initial Workflow Actions**

1. **Open** the _Core_ section in the left Actions menu.
2. **Drag and Drop** the _noop_ action to the Workflow Canvas.
3. **Open** the _Microsoft Graph_ section in the left Actions menu.
4. **Drag and Drop** the _Add Group Member_ action to the Workflow Canvas.
5. **Click and Drag** the transition from the _noop_ action to the _Add Group Member_ action.
   * To do this, you will need to hover over the gray circle under the _On Success_ section of the _noop_ action.

**Configure the Noop**

1. **Click** on the _noop_ Action to open the properties.
2. **Click** the edit icon next to the _noop_ name.
3. **Type** "add\_or\_remove" for the name.
4. **Type** "Checks the action variable to determine if we are adding or removing a user from a group" for the _Description_.

**Configure the Transition**

1. **Click** on the transition on the _noop_ Action.
2. **Type** "Add" in the _Custom Label_ field.
3. **Click** on the _Custom Condition_ option under _Condition_.
4. **Click** on the Jinja editor button next to the _Custom Condition_ field.
5. **Type** the following to add a custom condition where the action is performed on "add".

```django
{{ CTX.action == "add" }}
```

6. **Close** the editor.

**Configure the Workflow Variable Inputs with the Form Variables**

1. **Click** on the _Configure Workflow Variable_ button in the top right menu.
   * This is the pencil icon.
2. **Type** "300" in the _Time Saved (seconds)_ field.
3. **Click** the plus (+) button next to _Input Configuration_ to add the user variable.
4. **Type** "user\_id" in the _name_ field.
5. **Click** the _Required_ checkbox.
6. **Click** the plus (+) button next to _Input Configuration_ again to add the group variable.
7. **Type** "group\_id" in the _name_ field.
8. **Click** the _Required_ checkbox.
9. **Click** the plus (+) button next to _Input Configuration_ again to add the action variable.
10. **Type** "action" in the _name_ field.
11. **Click** the _Required_ checkbox.
12. **Click** _Submit_.

</details>

***

### Part 3: Triggering the Workflow with the Form

Next, we'll add a Form trigger to the workflow to ensure that the information that comes through the form can kick off the workflow process.&#x20;

<details>

<summary>Steps: Triggering the Workflow with the Form</summary>

**Add a Form Trigger**

1. **Click** the _Add Trigger_ button at the top menu.
2. **Type** "Form Trigger" in the _Name_ field.
3. **Click** the _Enabled_ slider.
4. **Choose** _Core - Form Submission_ for the _Trigger Type_.
5. **Choose** _Microsoft Graph_ for _Integration Overrides_.
6. **Choose** the _Add or Remove User from AzureAD Group_ form under _Trigger Parameters_ → _Form_.
7. **Click** Submit.
8. **Click** _Publish_ to save the Workflow with the new Trigger.

</details>

***

### Part 4: Configuring the Add and Remove Graph Actions

We jumped ahead to show how to trigger a workflow with a form. We now are going back to set the parameters needed for the actions to add or remove a user from a group.

<details>

<summary>Steps: Finishing the Workflow</summary>

**Add a Second Transition**

1. **Click** the _Add_ (+) button on the _noop_ action to add a new transition.

**Configure the Remove Transition**

1. **Click** on the right transition on the _noop_ Action.
2. **Type** "Remove" in the _Custom Label_ field.
3. **Click** on the _Custom Condition_ option under _Condition_.
4. **Click** on the Jinja editor button next to the _Custom Condition_ field.
5. **Type** the following to add a custom condition.

```django
{{ CTX.action == "remove" }}
```

6. **Close** the editor.

**Set the Transitions to Follow First**

1. **Click** the _noop_ Action, now named "add\_or\_remove".
2. **Click** on the _Advanced_ section at the bottom.
3. **Click** _Follow First_ under _Transition Mode_.
4. **Click** _Publish_ to save the Workflow.

**Add and Configure the Remove Group Member Action**

1. **Open** the _Microsoft Graph_ section in the left Actions menu.
2. **Drag and Drop** the _Remove Group Member_ action to the Workflow Canvas.
3. **Click** the _Remove Group Member_ Action.
4. **Type** "Removing user from Group" in the _Description_ field.
5. **Click** on the Jinja editor button next to the _Group_ field.
6. **Type** the following to to reference the `group_id` input variable with Jinja:

```django
{{ CTX.group_id }}
```

7. **Close** the editor.
8. **Click** on the Jinja editor button next to the _User ID_ field.
9. **Type** the following to to reference the `user_id` input variable with Jinja:

```django
{{ CTX.user_id }}
```

10. **Close** the editor.
11. **Click and Drag** the transition from the _noop_ action to the _Remove Group Member_ action.
   * To do this, you will need to hover over the gray circle under the new _Remove_ section you added.

**Configure Add Group Member Action**

1. **Click** the _Add Group Member_ Action.
2. **Type** "Adding user to Group" in the _Description_ field.
3. **Click** on the Jinja editor button next to the _Group_ field.
4. **Type** the following to to reference the `group_id` input variable with Jinja:

```django
{{ CTX.group_id }}
```

5. **Click** on the Jinja editor button next to the _User ID_ field.
6. **Type** the following to to reference the `user_id` input variable with Jinja:

```django
{{ CTX.user_id }}
```

</details>

### Part 5: Check the Results

Finally, let's test out the workflow by filling out the form and checking the workflow results!

<details>

<summary>Steps: Testing the Workflow</summary>

<mark style="color:red;">⚠️ This will only work with live data If you are using Microsoft Graph, make sure you keep in mind that this will work with live data so you can add or remove users appropriately. It's best to have pretend data to work with.</mark>

**View the Form URL**

1. **Click** _Edit Trigger_ at the top menu next to our Form Trigger
2. **Click** the _View Direct URLs_ button next to _Dynamic Form URL_.
3. **Click** on the link.

**Test the Form**

1. **Choose** a User.
2. **Choose** a Group.
3. **Click** Add or Remove.

**View the Results of the Workflow**

1. **Go to** _view results for workflow_.
   * This can be found next to the name of the workflow in the top menu.
2. **Click** on _Succeeded_ under Status to see the full results.

<mark style="color:blue;">📝 If the user or group aren't valid, you may see failure. To troubleshoot, you can open the</mark> _<mark style="color:blue;">Context</mark>_<mark style="color:blue;">,</mark> _<mark style="color:blue;">Logs</mark>_<mark style="color:blue;">, or</mark> _<mark style="color:blue;">Input</mark>_ <mark style="color:blue;">sections to dig into more detail and see what happened.</mark>

</details>

***

## Conclusion

Congratulations! You have successfully created a form, designed a workflow, and connected the two with a trigger to automate Azure AD group management. In Rewst 103, we'll take a step back and look at using Jinja in our workflows. If you have any questions, don't hesitate to reach out. Happy automating!



## Additional Resources

{% hint style="info" %}
For more information on using Forms, Workflows, and Triggers, check out our documentation:

* [Building Workflows](../../documentation/workflows/)
* [Using Forms](../../documentation/forms/)
* [Introduction to Triggers](../../documentation/triggers/intro-to-triggers.md)
{% endhint %}

## Need more guidance?&#x20;

{% hint style="success" %}
Sign up for our **LIVE** training sessions below!
{% endhint %}

<table data-card-size="large" data-column-title-hidden data-view="cards" data-full-width="false"><thead><tr><th align="center"></th><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center"><mark style="color:blue;"><strong>Rewst 102</strong></mark></td><td align="center">Building A Basic Workflow</td><td><a href="https://calendly.com/cluck-u/rewst-102">https://calendly.com/cluck-u/rewst-102</a></td></tr><tr><td align="center"><mark style="color:blue;"><strong>Cluck U Office Hours</strong></mark></td><td align="center">Come and Get Help!</td><td><a href="https://calendly.com/cluck-u/office-hours">https://calendly.com/cluck-u/office-hours</a></td></tr></tbody></table>
