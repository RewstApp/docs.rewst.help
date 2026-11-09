---
hidden: true
noIndex: true
---

# Rewst workflow Engine Next upgrade: Beta guide

{% hint style="info" %}
Shhh, this page is a secret!

For betas within the Rewst product, our related documentation is link access-only. This means that you won't be able to find it in search or ask RoboRewsty questions about the content of this page. For questions, reach out in your dedicated support Discord channel.
{% endhint %}

## What is the Next Engine upgrade?

We’re upgrading the core engine that executes your workflows in Rewst. It's designed to make workflows faster, more reliable, and better able to handle complex and long-running automation. For you, nothing about how you build or manage workflows changes. The same Crates, actions, triggers, and integrations all work identically.

Right now, this upgrade is in beta. The old and new workflow engines are running side-by-side with a per-workflow toggle that you control to determine which engine to use. This allows you full control and immediate rollback to the old engine at any time if you encounter any issues. Both engines use the same database.

### How much faster is the Next Engine?

This depends heavily on the workflow, but in testing we've seen everything from modest\
gains to order-of-magnitude improvements. Real examples from beta runs:

* 33 seconds → 14 seconds
* 2 minutes → 13 seconds
* \~28 minutes → under 2 minutes per sub-run
* 27 minutes → 5 minutes
* 9 minutes → 2 minutes

The larger and more complex the workflow, the more dramatic the improvement

## Your role as a beta user

Run your normal workflows and let us know if anything looks different from what you’d expect. If you see something unexpected, post it in the Beta Discord channel, or open a normal support ticket with the workflow execution ID. The engine is designed to drive every workflow to a completed state and to eliminate hung and stuck executions. If you do see something stuck in running for an unusually long time on Engine Next, please report it — reducing that to zero is an explicit goal of the beta. We also love hearing about your wins! Send us your before and after run times, too.

{% hint style="info" %}
You’re joining a private Discord channel with other beta participants and Rewst team members. It’s the place to share findings, ask questions, and give us feedback. [Click here to activate your channel invite.](https://discord.gg/XW2nkvDPF)
{% endhint %}

Start with workflows that are not ultra business-critical, and favor larger, more\
complex ones. Those are the best stress tests, and where you'll see the biggest wins. When you enable a workflow, compare its results and run time against previous runs and confirm nothing unexpected changed. Newly built workflows are also a good place to try Engine Next.

## **How it works**

#### How do you turn it on?

* Once your organization is enabled as a beta tester, you'll find the per-workflow toggle as a column in the workflow list view labeled **Engine Next**. The default off setting uses the old engine, and the on setting uses the new engine.

<figure><img src="../.gitbook/assets/Screenshot 2026-07-23 at 3.45.37 PM.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
The toggle value is cached, so it takes roughly 15 seconds to propagate before\
new runs of that workflow pick up the change.
{% endhint %}

* Once you're comfortable and ready to take on the changes, you can also flip an org-wide **Enable** setting under **Settings > Feature Preview** in the left side menu of your Rewst platfor&#x6D;**.**

<figure><img src="../.gitbook/assets/Screenshot 2026-07-23 at 3.46.41 PM.png" alt=""><figcaption></figcaption></figure>

* Once a workflow starts on an engine, it completes fully on that engine, including\
  all of its subworkflows. It will never switch back and forth mid-execution.

#### How do you know a workflow actually ran on Engine Next?

* At the top of the workflow results page, an **Engine Next** tag will show if the workflow execution used the new engine.
* Execution history remains visible for 30 days, the same as today.

#### If you rerun a previous execution, which engine does it use?

* Execution will follow whatever the toggle is currently set to. If Engine Next is on for that workflow, the rerun uses Engine Next, even if the original execution ran on the old engine.
* If you toggle off while a workflow is already running, that run finishes on whatever engine it started with. Your change applies to the next run.

#### How are subworkflows handled?

* Subworkflows automatically inherit the engine of the workflow that started them. On the execution and results page, you'll see an Engine Next chip near the workflow name and run time. If a run used the old engine, the chip won't be there.
* Once a workflow starts on an engine, it completes fully on that engine — including\
  all of its subworkflows. It will never switch back and forth mid-execution.
* If your subworkflow is shared by two parent workflows, the workflow execution follows whichever parent kicked off that particular run. The same shared sub workflow can run on the old engine when called by an old-engine parent and on Engine Next when called by an Engine Next parent. It doesn't propagate back up to change the parent.

#### Will Rewst deployments interrupt your running workflows?

* No. Engine Next pins each in-flight workflow to the engine version it started on.
* When we deploy a new version, existing runs finish on their original version and only newly\
  started workflows use the new one, so rolling deploys don't break workflows that are\
  mid-flight, including long-running ones.

#### Can you turn it off if you go all-in and change your mind?

* If you enable Engine Next for your whole org and want to back out, turning it off\
  reverts to the per-workflow selections you had before. You won't lose your prior\
  configuration.

#### Why do in-progress results sometimes look a little different?

* Engine Next doesn't write to the database continuously the way the old engine did. Instead, it\
  records an initial in progress record when the run kicks off and then writes the full\
  results at the end of the run. While a run is in flight, live progress is streamed to the results page instead of being read from the database.
* As a result you may notice minor in-flight display quirks. For example, a running subworkflow not appearing until it completes, or a subworkflow name showing where a task name used to. Several of these have already been fixed and more fixes are rolling out. The final saved result matches the old engine's view.

#### What happens if Engine Next, or the underlying infrastructure, goes down?

* Engine Next has robust fault tolerance built in. If there's a backend outage, the engine doesn't lose the workflows it's holding. They stay queued, and as soon as infrastructure is back online they resume right where they left off and run through to completion. You shouldn't need\
  to manually recover or rerun workflows that were caught in an outage.
* However, Engine Next is not shielded from every possible platform issue, and\
  it does not provide full tenant isolation. Because it dramatically reduces database\
  reads and writes and the locking and blocking that came with them, it's far more resilient than\
  the old engine and reduces the noisy neighbor class of problems.

## November 2026 workflow execution beta

{% hint style="info" %}
The updated Results page is currently in beta and only viewable for users who particpate in our Engine Next upgrade beta.&#x20;
{% endhint %}

The Results page acts as the record of all your automations. Every time a workflow runs in your organization — whether it was triggered automatically, by a form submission, or manually — a record of that run appears here. It's where you go to see what happened, what succeeded, what failed, and why.

{% hint style="success" %}
If you want to see results for just one specific workflow rather than everything, the best path is to navigate to [**Automations > Workflows**](automations/workflows/#view-specific-workflow-results), find the workflow you need, and click the results icon on that row. This will take you to a filtered view showing only that workflow's history.
{% endhint %}

Each row in the results list represents one workflow executio&#x6E;**,** a single run of a single workflow. It contains the following information:

* Status - Color-coded message
  * Succeeded - Everything ran as expected, no issues
  * Failed - Something went wrong during the run, and it should be investigated
  * Running - The workflow is still in progress right now
  * Cancelled - The execution was stopped before it finished
* Workflow name - Which automation ran
* Organization - Which org the workflow ran for
* Engine - Which engine was used to run the workflow, Rewst's legacy engine or newer Temporal engine
* Successful tasks - The number of actions in the workflow that executed successfully, even if the entire run failed
* Started - The date and time that the execution began
* Finished - The date and time that the execution finished
* Duration - The total amount of time for the execution
* Time saved - Rewst tracks estimated time saved per execution
* Click **⋮** to the right of any row to expose options to copy the result link or delete the result.&#x20;
* Click ![](<../.gitbook/assets/Screenshot 2026-11-03 at 4.42.44 PM.png>) to see other executions of that workflow.&#x20;
* Click **>** to view the Execution Detail page for that workflow.&#x20;

## **Filter results**

Click on any of the statuses at the top of the list to filter results down to just that type of status. Click **All** to reset previous filtering selections and display the entire available list.

<figure><img src="../.gitbook/assets/Screenshot 2026-11-03 at 4.44.38 PM.png" alt=""><figcaption></figcaption></figure>

Use the filter drop-down selectors at the top of the list to filter results by date range up to 30 days previous and within your time zone, or by failure type. Enter a workflow name into the **Search by workflow name** bar to narrow down your list to specific characters.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2026-11-03 at 4.40.52 PM.png" alt=""><figcaption></figcaption></figure>

Toggle **Include sub-orgs** and **Include sub-workflows** on or off to filter out child organizations or subworkflows from your total results list.

<figure><img src="../.gitbook/assets/Screenshot 2026-11-03 at 4.40.42 PM.png" alt=""><figcaption></figcaption></figure>

## Execution detail view

Click **>** on any row to open that run's Execution Detail page. You'll see a step-by-step log of every action the workflow took, in order. If something failed, the failed step will be highlighted, and you can click on it to see the error message. This is the information you'd share with Rewst support if you needed help. Copy the URL from your browser while viewing an execution and paste it directly into a support ticket.

* Click **Other Runs** to view all other available execution results for that workflow.
* Click **Visualize** to launch the execution in the Workflow Builder Canvas and display the run visually.
* Click **Analyze** to open RoboRewsty and have him analyze and give feedback on your execution results.
* Click **Re-Run** to manually push an immediate run of the workflow.
* Click **⋮** to expose clickable options to **Copy results link** and **Copy workflow link**.&#x20;
*   When the run contains at least one failure, that failure is listed in the failures panel. Click on each failure to expand and view its information. The panel contains a breakdown for child workflow, each linking to its own error.\
    <br>

    <figure><img src="../.gitbook/assets/image (105).png" alt="" width="375"><figcaption></figcaption></figure>
* A banner will display across the page when a run repeatedly fails in a way it may not recover from on its own.

#### How to read a failed execution

* At the top of the execution page, note the summary header. It shows which workflow ran, what its status is, when it ran, and how many tasks succeeded. The progress bar beneath the numbers displays the waiting time, for inquiry or delay, versus working execution time for the run.

<figure><img src="../.gitbook/assets/image (104).png" alt="" width="375"><figcaption></figcaption></figure>

*   The Task outcomes and Successful Tasks tiles display the breakdown of what happened to all tasks in the workflow.<br>

    <figure><img src="../.gitbook/assets/Screenshot 2026-11-03 at 5.09.39 PM.png" alt=""><figcaption></figcaption></figure>
* The most important thing to look at when an execution fails is the Errors section. This is the plain-English explanation of what went wrong. Ask RoboRewsty for help decoding your error message.

<figure><img src="../.gitbook/assets/Screenshot 2026-11-03 at 4.21.25 PM.png" alt=""><figcaption></figcaption></figure>

* Click on any task to open its expanded detailed result.
  * The Input section holds the data that was sent into the task when it was triggered. The input is useful for troubleshooting because it tells you exactly what data the workflow received, so you can verify it was triggered correctly even if the workflow itself failed.
  * The Result section shows what the action produced as a result.&#x20;

{% hint style="success" %}
When you land on a failed execution, always read it in this order: \
1\. Errors first \
2\. Input \
3\. The task list to determine which step failed.
{% endhint %}

## Delete results

You can delete individual execution records from this page. Note that deletion is permanent. The record will be gone from your view, though Rewst's backend keeps it in database backups for a short retention window. Deleting a result doesn't affect your time saved stats, which are tracked separately.
