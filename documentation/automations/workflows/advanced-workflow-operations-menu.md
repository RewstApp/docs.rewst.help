# Advanced workflow operations menu

{% hint style="info" %}
This document assumes that you've mastered earlier workflow building concepts from Cluck University and our introduction to the workflow builder [here](workflow-builder-how-to-set-up-a-workflow.md). If you haven't yet completed that reading, come back to this page later.
{% endhint %}

These operations can be found inside each task's **Advanced** tab.

## Integration overrides

For more on integration overrides and how to use them, see our documentation [here](https://docs.rewst.help/documentation/automations/intro-to-triggers#integration-overrides).

Add an integration override to the task by clicking  ![](<../../../.gitbook/assets/Screenshot 2025-03-26 at 11.10.58 AM.png>). This will expose a new submenu for **Configuration Selection Mode**.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.11.30 AM.png" alt=""><figcaption></figcaption></figure>

## Transition modes

_Transition modes_ in Rewst are responsible for determining how transitions attached to a workflow action are followed. There are two primary modes:

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-07 at 4.15.49 PM.png" alt=""><figcaption><p>Note the two different colored transitions arrows</p></figcaption></figure>

* **Follow All**: This is the default mode. If your task has multiple conditions attached, the Follow All mode attempts to follow all of the specified transitions. In the workflow visualization, this mode is represented by the standard color blue.
* **Follow First**: In this mode, conditions are evaluated from left to right and as soon as the first condition is satisfied, the remaining conditions are disregarded. To differentiate these transitions in the workflow visualization, they are color-coded orange.

## Task transition criteria sensitivity

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.20.10 AM.png" alt=""><figcaption></figcaption></figure>

This setting is used to indicate how many parent tasks need to be satisfied. For example, `0` would indicate all tasks. If the workflow has two tasks with arrows pointing to a third task, that sensitivity is the number of tasks above it which need to be complete before it runs. This is particularly important when building workflows that contain [subworkflows](./#subworkflows).&#x20;

## Run as org

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.20.31 AM.png" alt=""><figcaption></figcaption></figure>

The _Run as Org_ option allows the workflow action to run in the context of another organization.

{% hint style="warning" %}
You can only run as org going from a parent organization to child organization. The workflow will fail when attempting to run as the parent organization, when the workflow is running in the child organization context.
{% endhint %}

The purpose of `Run as Org` is to temporarily pass the execution of a workflow task into the context of another organization. This is something you may see done when you have a task— be it an individual action or a subworkflow— that needs to be executed as if it were for a different org than the one the workflow is running for.&#x20;

For example, if you wanted to have something run once for the parent organization that needed to also reference items for a child organization, a Run as Org option would solve this issue. Start by listing all organizations. Then, using `Run as Org` on a subworkflow, do things within that subworkflow for one or many of your managed organizations.

Or, when a form has an organization picker on it, where the organization ID is passed into the workflow from the form, `Run as Org` is used to have the actions in the workflow run as if they were for the selected organization, instead of the organization for which the form was loaded.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-10 at 5.51.50 PM.png" alt=""><figcaption></figcaption></figure>

## With items

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.19.37 AM.png" alt=""><figcaption></figcaption></figure>

_With Items_ is the equivalent to a `foreach` statement in other languages.

With this, you can pass a number of objects into a certain action and collect the results from each and then do something.

{% hint style="warning" %}
When using with items in Rewst, it's important that you make the name of the task unique, and different from any other task name in that workflow.&#x20;
{% endhint %}

In the example below, you're going to list every user that is enabled in the child organization, and create or update a contact for each one.

List all enabled users, then output this to a data alias called

```django
{{ CTX.all_users }}
```

The data alias has the following Jinja:

{% code overflow="wrap" %}
```django
{{
  [
    user
    for user in TASKS.m365_list_users.result.result.data.value
    if user.enabled
  ]
}}
```
{% endcode %}

You then have a subworkflow that creates or updates a contact. As per the best practice, use a subworkflow with your **With Items**.

In the **Advanced** tab, set the **With Items** field with this data alias.

The action now has the additional icon indicating that it has a `With Items` set on it.

During testing, or for example if creating tickets from an alert, you may sometimes want to limit the amount of alerts you get during this phase. Test the workflow on a subset of your total users initially to make sure it works as expected.

To achieve this, you could create an input variable on the workflow called `max_tickets_to_create_per_action`and set it to the maximum number of times you want that **With Items** to run.

If set to 1, it will only run on a single object within CTX.all\_users.

The below code is what you would use in the **With Items** field in the **Advanced** tab.

```django
{{ CTX.all_users[:CTX.max_tickets_to_create_per_action | int] }}
```

### Use inputs after creating With Items&#x20;

Iterating through CTX.all\_users on the action means you can't use \{{ CTX.all\_users.X \}} as the property for the input.

Instead, you must use `{{ item() }}`

Say you want to get the first name of each user as an input. On your **`With Items`** action you would execute:

```django
{{ item().firstName }}
```

## Items concurrency

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.23.21 AM.png" alt=""><figcaption></figcaption></figure>

If you're running a workflow task using With Items, this allows you to set how many of these processes run at the same time. It's recommended that no more than 10 concurrent actions be performed at a time to guarantee performance.

## Task timeout

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-26 at 11.23.53 AM.png" alt=""><figcaption></figcaption></figure>

This allows you to adjust the number of seconds to wait for a task to complete. The default value is 10 minutes.

## Shallow clone a workflow

_Shallow cloning_ is a feature of the Rewst platform that allows you to create a copy of an existing workflow or form. This is useful if you have a workflow that is very similar to another workflow, but which requires a few small changes.

Standard cloning copies the entire resource _pack—_ workflow, forms, templates, triggers, etc— and when cloning into your own org, you end up with multiple duplicates of the same resource. Shallow cloning copies that single selected resource, but re-uses all of the dependencies that it has. If you have a sub-workflow that's part of a main workflow, and you shallow clone that sub-workflow, you will end up with a copy of the sub-workflow. This lets you make changes to the sub-workflow without affecting the original workflow.

There is no difference between the steps to clone or shallow clone a resource. Rewst will automatically detect if you are cloning something into your own org. If so, the platform will shallow clone it instead. Note that this removes the **Synchronize** button on the dialog, and instead shows a text to explain.
