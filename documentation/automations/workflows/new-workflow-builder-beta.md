---
hidden: true
noIndex: true
---

# New Workflow Builder - Beta

{% hint style="info" %}
Our new version of Rewst's Workflow Builder is officially in Beta! For the near future, you'll have the option to use the old Workflow Builder or switch to our new experience via the <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 12.37.47 PM.png" alt="" data-size="line"> in the top tool bar.&#x20;

Submit feedback on our updated Builder here in our dedicated Discord feedback channel.&#x20;
{% endhint %}

Rewst's new Workflow Builder combines everything you loved about our original Builder with clearer menus, enhanced capabilities, and better visualization. The location of buttons and fields may have been moved around, but everything that was present in the old Workflow Builder is still present in the new version. Like before, access workflows in the Rewst platform by navigating to **Automations > Workflows** in the left side menu. Create a new workflow from scratch by clicking **Create Workflow**.

## The Workflow Builder toolbar <a href="#the-workflow-settings-toolbar" id="the-workflow-settings-toolbar"></a>

{% columns fullWidth="false" %}
{% column %}
### ![](<../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.37 PM.png>)  <a href="#the-workflow-settings-toolbar" id="the-workflow-settings-toolbar"></a>


{% endcolumn %}

{% column %}


Use the top left toolbar to open, view, and use the features of the workflow builder.
{% endcolumn %}
{% endcolumns %}

* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.41 PM.png" alt="" data-size="line"> to expand or collapse the general left side menu of the Rewst platform.
* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.45 PM.png" alt="" data-size="line"> to reveal the **Library**, where all your actions, triggers, subworkflows and favorites can be found. Read more about it in the [**Library**](new-workflow-builder-beta.md#library) section of this document.
* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.49 PM.png" alt="" data-size="line"> or <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.59 PM.png" alt="" data-size="line"> to undo or redo your last change.
* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.00.54 PM.png" alt="" data-size="line"> to open the **Settings** menu for your workflow. See more about this menu in the [**Settings**](new-workflow-builder-beta.md#settings) section of this document.
* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.01.03 PM.png" alt="" data-size="line">to open the additional **Canvas** controls menu. Zoom in, out, or to fit. Choose from vertical or horizontal layout for your canvas. Here you can also check the view on and off for **Snap to Grid**.
* Click <img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.01.10 PM.png" alt="" data-size="line">to **Show All Comments** or **Hide Comments**.

Center screen, the toolbar contains a drop-down selector for additional options for your workflow. This is also where you can toggle back to the legacy view of the Workflow Builder.

* Click **Rename** to change the name of your workflow.
* Click **Edit Workflow Attributes** to add a new tag or choose an existing tag from the drop-down **Tags** selector.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.38.20 PM.png" alt="" width="296"><figcaption></figcaption></figure>

* Click **Edit Workflow JSON** to open the JSON editor in the right of your screen.
* Click **Version History** to open a menu on the right side of your screen displaying the record of when the workflow was created and edited. You also have the option to revert back to a previous version of your workflow, or view previous versions to compare changes.
* Click **Execution History** to view the list of execution results for the workflow, including their success or failure status.&#x20;
* Click **Export** to [export a workflow](https://docs.rewst.help/documentation/automations/workflows#export-and-import-workflows).
*   Click **Clone** to create an exact copy of your workflow without changing the original.&#x20;

    The window that appears is the failsafe to confirm that you want to clone the workflow. In it, you can do the following:

    * Give your clone a different name from the original
    * Choose the organization where the workflow will be cloned to with the drop-down **Organization** selector
    * Choose to **Synchronize Changes** with the original workflow - any changes you make to the original workflow will be reflected in the clone if this is toggled on
* Click **Delete** to delete your workflow entirely.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.35.24 PM.png" alt=""><figcaption></figcaption></figure>

## Library

{% columns fullWidth="false" %}
{% column %}
<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.14.55 PM.png" alt=""><figcaption></figcaption></figure>
{% endcolumn %}

{% column %}
The **Library** menu contains three distinct tabs:

1. **Actions** holds a complete list all available actions and subworkflows. At the very bottom of the list is **+ Add Integrations**, which launches the option to add a new integration to Rewst. Note that this is intended to allow you to add an integration quickly and facilitate the completion of workflow design, not to replace the full integrations menu. Any integration added through the library that requires [organization mapping](../../integrations/#what-is-organization-mapping) will need to be mapped from its full integration page.\
   Integration actions are divided by categories, viewable after you click into the integration. If you search within an integration, results will be scoped to that integration only. This rule applies for custom integrations in addition to Rewst-native integrations.
2. **Flow Control** contains the option to add a new Trigger, as well as a list of all triggers already added to your workflow.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.15.03 PM.png" alt=""><figcaption></figcaption></figure>



3. **My Library** stores your bookmarked, favorite actions. Click the bookmark icon on any action to add it to the My Library list.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 2.15.10 PM.png" alt=""><figcaption></figcaption></figure>


{% endcolumn %}
{% endcolumns %}

At the very bottom of the menu you have the option to add a new custom integration.

1. Click **Add Integrations +**.
2. The dialog that appears contains many fields for information needed to set up the integration. Pull that relevant information from the partner app you wish to integrate.&#x20;
3. When finished,&#x20;

## Canvas view settings

{% columns %}
{% column %}
The canvas view menu is now on the left side of the Workflow Builder canvas. **+** and **-** zoom the view in or out. ![](<../../../.gitbook/assets/Screenshot 2026-03-20 at 1.21.54 PM.png>) snaps the view to fit the entire workflow into the center frame of your screen. ![](<../../../.gitbook/assets/Screenshot 2026-03-20 at 1.21.58 PM.png>)toggles the visualization interactivity of the workflow on or off. See more about this in the [#view-task-flow](new-workflow-builder-beta.md#view-task-flow "mention") and [#view-trigger-flow](new-workflow-builder-beta.md#view-trigger-flow "mention")sections of this document.
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-20 at 1.19.12 PM.png" alt=""><figcaption></figcaption></figure>


{% endcolumn %}
{% endcolumns %}

## Add transitions between actions

To add a transition, hover over your desired starting action. Note the circles on the right and bottom on the action. These represent the action’s outputs, and are where you can create transitions to following. The triangle on the top and left of the action are inputs into the action, and where you can connect a transition. Click on the circle under or to the right of the action, drag, and release on the top of the ending action where you would like the transition to conclude.&#x20;

<figure><img src="../../../.gitbook/assets/add transition.gif" alt=""><figcaption></figcaption></figure>

The diamond that appears between the two actions is the _transition indicator_. Click on it to open the transition settings menu.

{% columns fullWidth="false" %}
{% column %}
<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-18 at 3.18.17 PM.png" alt="" width="300"><figcaption></figcaption></figure>


{% endcolumn %}

{% column %}
\
From this menu you can:

* Optionally add a **Custom Transition Label.**
* Choose the **Condition** of your transition. - note the appearance and meaning of the condition statuses in the table below, the symbols of which will appear in your transition indicator once chosen.
* Add a data alias.

<figure><img src="../../../.gitbook/assets/condition statuses.gif" alt=""><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

| Transition indicator symbol | Label       | Meaning                                                               |
| --------------------------- | ----------- | --------------------------------------------------------------------- |
| ✓ - Check mark              | **Success** | The transition will only be followed if the preceding action succeeds |
| ✗ - X mark                  | **Failure** | The transition will only be followed if the preceding action fails    |
| ↻ - Circle/always           | **Always**  | The transition will be followed regardless of the action outcome      |
| { } - Braces/custom         | **Custom**  | The transition uses a custom Jinja condition                          |

## View action flow

View the relationship between actions via the animation depicted on their transitions. Note that the way the animation flows depicts the order of the actions in the workflow. You'll need to to run the workflow or pull up an execution histoy and select an execution for the animation to kick on. It automatically turns off when you return to the edit view in the Workflow Builder Canvas.

<figure><img src="../../../.gitbook/assets/task animation.gif" alt="" width="375"><figcaption></figcaption></figure>

## View trigger flow

Triggers now appear directly on the Workflow Builder Canvas, and have an arrow to visually indicates which action the workflow will start executing when that trigger fires.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-18 at 12.23.09 PM.png" alt="" width="289"><figcaption></figcaption></figure>

## General settings

The **Settings** menu has distinct tabs, each with its own configuration options.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 3.25.42 PM.png" alt=""><figcaption></figcaption></figure>

* **General** provides a field to view and edit the **Workflow Name**, as well as the **Workflow Timeout** in seconds, the **Time Saved** in seconds, and a drop-down selector for the **Workflow Type** - either  Standard, Option Generator, or Stream Output. Here you can also choose to **Delete Workflow** or **Download Workflow as JSON** file.
* **Data Aliases** displays a list of all defined [data aliases](data-aliases.md).
* **Input** displays existing input configuration, as well as options to **Add Schema** or **+ Add Input**.
* **Output** displays existing output configuration, as well as options to **Add Schema** or **+ Add Output**.
* **Variables** displays existing variables, as well as an option to **+ Add Variable**.
* **Triggers** displays existing [triggers](../intro-to-triggers/), as well as an option to **+ Add Trigger**.
  * Click **+ Add Trigger** to reveal the **Trigger Settings** menu. Each of the tabs contains the following options. Remember to click **Save Trigger** at the bottom of the menu when finished making your selections.
    * In the **General** tab:
      * Here you can update the fields for **Trigger Name**, **Trigger Mode**, and **Trigger Type**.&#x20;
      * Under the **Mock Results** and **Workflow Input Parameters** menus, the **Query Conditions** fields allow for the entering of string values only.
      * Any previously set trigger variables will appear here in the **Trigger Variable** section.
    * In the **Overrides** tab:
      * **+ Integration Override** reveals a list of all integrations and allows you to specify which integration configurations should be used. Otherwise, the default integration configuration for the triggering organization will be used.&#x20;
      * **+ Add All** will add integration overrides for all installed integrations in the organization.
    * In the **Criteria** tab, set up your [trigger criteria](../intro-to-triggers/trigger-criteria.md).
    *   In the **Run For** tab, choose your [Activate Triggers to Run For](../intro-to-triggers/#activate-trigger-to-run-for) settings.


* **Edit JSON** provides three separate code editors, including one each for **Trigger Outputs** and **Action Parameters**.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-17 at 3.42.26 PM.png" alt="" width="375"><figcaption></figcaption></figure>

## Action settings

Click into your action to open the **Action Settings** menu, which contains four tabs.

**General** - This includes your **Task Name** and **Description** fields, as well as **Output**, **Publish Result As**, and **Time Saved.** Click **Edit Task JSON** to open the action code editor.

**Parameters** - This contains all the specific parameter fields, which will vary depending on which action you're working with.

**Testing** - This tab provides the option to simulate the action's function with a user-defined result, useful for testing and debugging. Toggle **Mock this action** on or off. Click **Add Mock Result** to add additional guidelines for JSON content to be returned by this action to the **Mock Results** list.

**Advanced** - Here you'll find settings for several advanced action properties. The use and purpose of each is more fully documented [here](https://docs.rewst.help/documentation/automations/workflows/advanced-workflow-operations-menu#integration-overrides).

* [**Integration Overrides**](advanced-workflow-operations-menu.md#integration-overrides)
* [**Task Transition Criteria**](advanced-workflow-operations-menu.md#task-transition-criteria-sensitivity)
* [**Run as Org**](advanced-workflow-operations-menu.md#run-as-org)
* [**With Items**](advanced-workflow-operations-menu.md#with-items)
* [**Items Concurrency**](advanced-workflow-operations-menu.md#items-concurrency)
* [**Task Timeout**](advanced-workflow-operations-menu.md#task-timeout)
* [**Security Features**](https://docs.rewst.help/documentation/jinja/jsonpath-for-data-redaction-in-rewst)
  * **Redacted Input Parameters**
  * **Redacted Output Parameters**

## Trigger settings

Click and drag **Trigger** under the Flow Control tab of the Library to add a new trigger to your Workflow Builder Canvas. This will reveal a new menu to the right with your **Trigger Settings** that contains four tabs.

**General** - Set your **Trigger Name**, choose the **Trigger Mode** and **Trigger Type**, and toggle your trigger to **Enabled** or **Disabled**.

**Overrides** - Add [**Integration Overrides**](../intro-to-triggers/#integration-overrides) for the trigger.

**Criteria** - Add [trigger criteria](https://docs.rewst.help/documentation/automations/intro-to-triggers/trigger-criteria#save-trigger-criteria) to filter trigger events.

**Run For** - Choose which organization or organizations to activate the trigger to run for. Here you can also choose tags to select activation.

### Completion handlers

In the new Workflow Builder, [completion handlers](completion-handlers-and-workflow-wrappers.md) are treated as triggers. Find them in the trigger menu under the **Trigger Mode** drop-down selector.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-30 at 12.03.13 PM.png" alt="" width="242"><figcaption></figcaption></figure>

An **Inbound** selection will set the workflow to trigger by another workflow. An **Outbound** selection will trigger another workflow to run when this workflow completes.

## Testing

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-18 at 3.36.09 PM.png" alt=""><figcaption><p>In the dialog that appears after clicking <strong>Deploy</strong>, click <strong>Show Detailed Changes</strong> to expand the accordion and display a side-by-side comparison of your original workflow and all changes that would be published.</p></figcaption></figure>

Click **Run** to initiate your test, then click to confirm that you want to **Run Test** in the dialog that appears.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-18 at 4.35.53 PM.png" alt=""><figcaption></figcaption></figure>

After your test is complete, view the workflow execution results in the right side menu. Click on any of the events in the execution log to expand and view information. Click **View Results** to launch a new browser tab with the complete results, in the Rewst platform outside of the Workflow Builder. When satisfied with your workflow, then click **Deploy** and **Submit** to save your changes and implement them on all future runs.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-18 at 4.36.37 PM.png" alt=""><figcaption></figcaption></figure>

