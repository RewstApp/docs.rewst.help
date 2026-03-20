# Context Viewer

{% hint style="info" %}
For more on The Context, take our [Jinja coursework in Cluck University](https://learn.rewst.io/path/automation-basics), or read our docs [here](jinja-essentials.md#what-is-the-context).&#x20;
{% endhint %}

## What is the Context Viewer?

Prior to the release of our Context Viewer, you'd have to remember all the variables, structures and data aliases you create in [The Context](jinja-essentials.md#what-is-the-context) of your workflows on your own. Now, by default, the Context Viewer will recall these for you in any task that has an output schema, without having to run the workflow first.

{% hint style="info" %}
An _output schema_ is a structured display of what is returned by the API of the integration called by your task. It's what we expect back from the API call for that task. Some of Rewst's older tasks don't have output schemas.&#x20;

Remember, _actions_ are dragged from the left side action menu of your Workflow Builder, and once placed on the Workflow Builder canvas become _tasks_.
{% endhint %}

Click ![](<../../.gitbook/assets/Screenshot 2025-11-26 at 1.57.10 PM (1).png>)next to any field in your task's right side menu to open the Monaco Editor. Now, the Context Viewer will automatically appear to the left of the Monaco Editor whenever your task has an output schema.

<figure><img src="../../.gitbook/assets/Screenshot 2025-11-26 at 2.45.56 PM.png" alt=""><figcaption></figcaption></figure>

The Context Viewer has five tabs:

* **Current** - This tab shows the output schema for the task you are currently editing, expressed using `result.` syntax.
* **Tasks** - This tab lists out all output variables from the tasks that execute before the current task.
* **Published** - This tab lists out all published data alias values from earlier transitions, as well as workflow inputs.
* **Workflow** - This contains your workflow inputs. When new inputs are added, they immediately become available in this tab for use throughout the workflow.
* **Organization** - This tab lists out all available organization variables.

Click on any of the items listed in these tabs to immediately add them to the Monaco Editor. Once added, you can edit the code as needed.

The Context is location-aware - inside a task with output schema, it shows relevant result data with the appropriate syntax - `result.domain_aliases` vs `tasks.domain_aliases` - depending on where in the workflow you're editing.

## Current limitations to the Context Viewer

* Currently, not all tasks have output schemas. Future improvements will allow pulling in workflow execution information to show what happened at specific points in previous workflow runs, providing predictive capabilities based on past executions.
* The Context Viewer won't show completed workflow variables.&#x20;
* Trigger information may not be set up under its own category.
* If a task doesn't have an output schema, the Context Viewer won't appear to the left of the Monaco Editor when you open it in your task's right side menu.&#x20;



