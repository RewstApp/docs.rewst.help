# Workflow builder: How to set up a workflow

## Workflow Builder&#x20;

{% hint style="info" %}
Remember, the [Core](../actions-in-rewst/core-actions.md) actions accordion menu contains your base actions that apply for all integrations. The [Rewst](../actions-in-rewst/rewst-actions.md) actions accordion holds actions form the foundation of your interaction with the platform. The [workflows](../actions-in-rewst/workflows-actions.md) actions accordion contains any existing workflows in the workflow list for the related child organization. The other accordions contain actions that apply to that particular brand of integration.

Once an action has been dragged onto the canvas, we refer to that dragged action as a _task_.
{% endhint %}

<figure><img src="../../../.gitbook/assets/workflow canvas.png" alt=""><figcaption><p>A blank workflow builder canvas, as seen for a freshly created workflow</p></figcaption></figure>

## The workflow settings toolbar

At the top of the workflow builder, you'll find several settings buttons.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.38.03 PM.png" alt=""><figcaption></figcaption></figure>

**Edit Workflow Title** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.39.11 PM.png" alt="" data-size="line">**:** Click to open up a dialogue where you can change the name of your workflow.

**View results for workflow** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.40.07 PM.png" alt="" data-size="line">: This opens up a new tab in your browser with the entire recorded execution history of that workflow.

**History** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.40.33 PM.png" alt="" data-size="line">: Click to open a menu on the right side of your screen displaying the record of when the workflow was created and edited. You also have the option to revert back to a previous version of your workflow, or view previous versions to compare changes.

**Notes**  <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.41.06 PM.png" alt="" data-size="line">: Click to open the **Notes** menu, where you can view a record of all notes made on the workflow, and view instructions for how to add new notes. For more information on notes, see the [#add-edit-or-delete-workflow-notes](workflow-builder-how-to-set-up-a-workflow.md#add-edit-or-delete-workflow-notes "mention") section of this document.

**Execution History** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.41.52 PM.png" alt="" data-size="line">: This reveals the same information as History, but provides an easy way to view the data without leaving your workflow builder.

**Data Aliases** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.42.21 PM.png" alt="" data-size="line">: Click to view a list of all set [data aliases](data-aliases.md). Click on the data alias to take you directly to that action.

**Add Trigger** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.42.56 PM.png" alt="" data-size="line">: Click to open up the **Add Trigger** form, where you can set up your [trigger](../intro-to-triggers/)'s configuration, parameters, criteria, and activated organizations.

**Configure Workflow Settings** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.43.27 PM.png" alt="" data-size="line">: Click to open the menu that contains the settings for workflow type, workflow timeout, time saved, and variable, [input, and output configuration](data-input-and-output-input-variables-and-context-variables.md).

**Workflow Completion Handlers** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.43.57 PM.png" alt="" data-size="line">: Click to open a submenu where you can set [completion handlers](https://docs.rewst.help/documentation/workflows/completion-handlers). Click the button a second time to collapse the menu.

**Workflow Options** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.44.23 PM.png" alt="" data-size="line">: Click to open a submenu where you can export a workflow, clone a workflow, or delete your workflow, as well as edit the workflow's attributes.&#x20;

**Display Validation Errors** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.44.56 PM.png" alt="" data-size="line">: By default, this is set to off. When toggled on, Rewst will provide an error on required fields that aren't filled out, and add a message about the field being required beneath the field in red text. The text will be invisible until the user clicks on the field and then click out of it without entering a value.

<figure><img src="../../../.gitbook/assets/image (57).png" alt=""><figcaption><p>An example of the message, when the setting is toggled on</p></figcaption></figure>

**Test** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.45.18 PM.png" alt="" data-size="line">: Click to run a test of your workflow as it appears on your workflow builder canvas, and view the results of that test. Note that this also publishes and saves the workflow.

**Publish** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.45.49 PM.png" alt="" data-size="line">: Click to publish changes on your workflow without first running a test, which will push the updated version live for use. This also offers a dual screen code viewer, to compare your old workflow to your new one.

## Build a workflow

### Set up the trigger

{% hint style="success" %}
Recall that every workflow is kicked off by a trigger. Which trigger you choose will depend on the goals of your workflow. There's no right or wrong order to build your workflow as long as it contains all the correct parts at the time of publication. You could start with adding actions to your canvas first, then set up your trigger.

If your trigger is form, you'll need to create and set up that form first before pulling it into your workflow.
{% endhint %}

1. Click <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.42.56 PM (1).png" alt="" data-size="line">to add a new trigger.
2. Name your trigger with something simple but descriptive.
3. Toggle **Enabled** to on.
4. Search for your desired trigger in the **Trigger Type** drop down menu. Depending on your trigger, new **Trigger Parameters** will appear as a new section in the setup menu with additional selections to be made to set parameters for the trigger. For example, if your trigger is a [form](https://docs.rewst.help/documentation/forms), you would be asked to select the name of an existing form to use as the trigger.
5. If needed, add an [integration override](../intro-to-triggers/#create-a-trigger).
6. Set your trigger criteria, if required for your workflow.
7. Think about which organizations you want the trigger to run for.
   1. **Selected Organization (Org Name)** will be toggled on by default. Toggle to off if desired.
   2. If you want the automation to work for your main org as well as all child organizations, toggle **All current and future managed organizations** to on.&#x20;
   3. If you want the automation to apply only for certain organizations, select them manually in the **Organizations** selector field.
8. Click **Submit** to save the trigger.

{% hint style="info" %}
A workflow can be called by multiple forms through the use of triggers. All that is required is to open the workflow and create a new trigger with **Core - Form Submission** selected for the Trigger Type.
{% endhint %}

### Create the workflow

1. Click **Create**.&#x20;
2. Give your workflow a **Name**, and add any tags you would like via the **Tags** drop-down selector.
3. Click **Submit**. This will launch the workflow builder.

### Drag the action

1. Search for your desired action in the left side menu.&#x20;
2. Click on it, drag it, and drop it onto the canvas.
3. Repeat this process to add all needed actions to your workflow.

### Configure tasks

{% hint style="info" %}
Remember, once an action is placed on the canvas, we then call it a task.
{% endhint %}

1. Click on the placed task, which will open a configuration dialog featuring two sections:
   1. A set of basic details fields at the top:
      1. **Name**: A user-editable field for the task's identifier.&#x20;
      2. **Reference**: The integration pack and task description.&#x20;
      3. **Output**: Specifies where the task's output gets stored in the task logs.&#x20;
      4. **Task ID**: The unique ID for referencing this task.&#x20;
      5. **Description**: A user-fillable text box for additional task information.&#x20;
      6. **Publish Result As**: A friendly name you assign for the task's results that you can use as an a context variable for calling it's content in future tasks.
   2. Four distinct tabs beneath the basic details:&#x20;
      1. **Parameters**: Unique to each task, this tab houses options for defining the task's behavior during execution, including settings for endpoints, filters, conditions, and query parameters. Think of them like fill-in-the-blank options that make workflows adaptable.&#x20;
         1. Note the **Redact on Hover** setting for inputs that are set to **Password**. This can be toggled on or off via the ![](<../../../.gitbook/assets/Screenshot 2025-03-25 at 4.55.28 PM.png>).
      2. **Advanced**: In this tab, you'll set the rules for your task's path and behavior within the workflow. See more about this on the [Advanced Workflow Operations](advanced-workflow-operations-menu.md) page. Options include:
         1. [Integration Overrides](../intro-to-triggers/#integration-override-on-an-action)
         2. [Transition Mode](advanced-workflow-operations-menu.md#transition-modes)
         3. [Task Transition Criteria Sensitivity](advanced-workflow-operations-menu.md#task-transition-criteria-sensitivity)
         4. [Run as Org](advanced-workflow-operations-menu.md#run-as-org)
         5. [With Items](../../jinja/jinja-essentials.md#with-items)
         6. [Items Concurrency](advanced-workflow-operations-menu.md#items-concurrency)
         7. [Task Timeout](advanced-workflow-operations-menu.md#task-timeout)
      3. **Mocking**: This tab provides the option to simulate the task's function with a user-defined result, useful for testing and debugging.
      4. **Time Savings**: In this tab, specify your estimate of the time a human would need to complete the task. This is used for creating Time Entries in PSA platforms.
      5. **Security**: This tab allows for meticulous redaction of sensitive information within workflow tasks. This is especially vital when using generic HTTP actions for services without official integrations, where API tokens or other sensitive data in headers could be exposed in results.&#x20;
         1. In the **Redacted Input Parameters** and **Redacted Output Parameters** fields, mask sensitive data in the task's inputs or outputs. You also have the option to customize redaction with [JSONPath queries](https://jsonpath.com/).
         2. These queries can be entered manually in the editor, or chosen from the field's drop-down selector.
         3. When redaction is applied, sensitive fields will appear as `********` in task logs and results.
2. Remember to add [transitions](https://docs.rewst.help/documentation/workflows/configuring-your-workflow-tasks/navigating-between-tasks-with-transitions) between your tasks.
3. Click **Test** to see if your workflow executes as desired.&#x20;
4. Click **Publish** to save your changes and push them to the desired effect.

### Add time saved to a workflow

One of the key metrics you can use to understand the value added by your automations is time saved. You can configure this in Rewst by identifying how long it takes to manually work through your process before automating it and adding it into your workflow.

{% hint style="info" %}
**Considerations for time saved**

When determining how much time to set for any given process, it's a good practice to consider not only how much time it may take you or your most experienced tech to go through that process manually, but also how much time it takes to fix any human errors that may happen during this process.
{% endhint %}

1. Click on the workflow that you want to configure.
2. Click on **Configure Workflow Variables** <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.43.27 PM (1).png" alt="" data-size="line"> to edit the workflow.
3. Enter the amount of seconds it takes for the process in **Time Saved (seconds)**.
4. Click **Submit**.

### Add, edit, or delete workflow notes

{% hint style="info" %}
Rewst now also offers our [RoboRewsty](../../roborewsty/document-with-roborewsty.md) note taking feature, to automate your documentation. Choose to document manually, or with RoboRewsty. &#x20;
{% endhint %}

Notes are a great way to jot down your thinking behind workflow aspects, and an essential step to building workflows for any team that has multiple employees editing workflows. They save in the workflow itself, and can be viewed via the <img src="../../../.gitbook/assets/Screenshot 2025-03-05 at 2.41.06 PM (1).png" alt="" data-size="line"> notes button by anyone who has permissions to edit that workflow. These boxes provide a title and a markdown editor.

{% hint style="warning" %}
Adding notes is disabled for synced clone workflows.&#x20;
{% endhint %}

1. Right-click the canvas and select **Add Note**. Alternatively, press and hold the **control** key, then drag your mouse to create a note.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-03-06 at 3.01.41 PM.png>)
2. Click and drag it to the desired location on the canvas.
3.  Hover over the upper-right <img src="../../../.gitbook/assets/Screenshot 2025-03-06 at 3.02.37 PM.png" alt="" data-size="line"> icon and click **Edit Note** to edit a note's content in the right side menu.<br>

    <figure><img src="../../../.gitbook/assets/Screenshot 2025-03-06 at 3.03.18 PM.png" alt=""><figcaption></figcaption></figure>
4. To delete notes, right-click the note and click **Delete Note**_._

## Additional workflow builder features

### Select multiple elements on the canvas

Select multiple workflow tasks and notes simultaneously by drawing a selection box around them.

1. Hold shift and drag your mouse, or hold the middle-mouse button and drag your mouse.
2. Once you’ve selected multiple tasks or notes, move them by dragging the selection box to the desired location.
3. With multiple tasks or notes selected, you can perform the following actions:
   1. Delete Items: Press the delete key, or right-click the canvas and select **Delete Selected Tasks**.
   2. Duplicate Items: Press ctrl+d, or right-click the canvas and select **Duplicate Selected Tasks**.

<figure><img src="../../../.gitbook/assets/multiselect gif.gif" alt="" width="375"><figcaption><p>The duplication of tasks and transitions</p></figcaption></figure>

### Favorite actions

Commonly used actions can be favorited to easily find and add actions to workflows. When favorited, actions can be found in the **favorites** section and added on the workflow canvas by right-clicking.

1. Find the action you want to favorite.
2. Click the star icon next to the action.\
   \
   ![](<../../../.gitbook/assets/image (62).png>)
3. To add a favorited action to your workflow:
   1. Right-click on the workflow canvas.
   2. Add an action from the favorites section.

### Clone and synchronize a workflow

Custom-designed workflows can be cloned to create an exact copy without changing your original.&#x20;

1. Click **...** at the top right of the Workflow Builder Canvas.
2. Click **Clone**.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-02-06 at 5.18.24 PM.png>)
3. The window that appears is the failsafe to confirm that you want to clone the workflow. \
   In it, you can do the following:
   1. Give your clone a different name from the original
   2. Choose the organization where the workflow will be cloned to with the drop-down **Organization** selector
   3.  Choose to **Synchronize Changes** with the original workflow - any changes you make to the original workflow will be reflected in the clone if this is toggled on<br>

       <figure><img src="../../../.gitbook/assets/Screenshot 2026-02-06 at 5.17.03 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Creating a clone of your workflow is a great way to make a siloed test environment for your custom workflow. Make upgrades, fixes, or updates to your original workflow with synchronized changes toggled off.
{% endhint %}

## Retrieve the name of a workflow

Run the command `{{ WORKFLOW.name }}` .

Similarly, if you're searching for the name as it relates to completion handlers, run the command  \
`{{ COMPLETED_WORKFLOW.WORKFLOW.name }}` .

{% hint style="info" %}
Information for the **Advanced** tab of tasks and actions in a workflow can be found in our documentation for the [advanced workflow operations menu](advanced-workflow-operations-menu.md).
{% endhint %}
