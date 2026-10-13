# The Live Editor

## What is the Live Editor?

Rewst Classic's _Live Editor_ is an interactive environment in the Rewst Classic platform where you can test and debug workflows, Jinja, PowerShell, and variables in real time. Instead of building blindly and hoping it works later, check your code and see if it delivers your desired result.

* Run individual steps or entire branches of a workflow and see how things behave.
* Inspect the actual data moving through a workflow, including step outputs, parsed inputs, and runtime values.
* Test your Jinja expressions directly on real data without deploying the full workflow.

## Use the Live Editor in Rewst

Access the Live Editor by navigating to **Automations > Live Editor** in the left side menu of your Rewst  Classic platform.

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-05 at 4.10.41 PM.png" alt="Screenshot of the Templates list view in the Rewst Automations section, showing a dark-themed interface with a left navigation menu, a top search bar and Create Template button, and a table of templates with names, descriptions, dates, attributes, and action icons.  Alt text: Screenshot of the Live Editor in the Rewst Automations section, showing a dark-themed interface with a left navigation menu and three side-by-side panels for Context, Editor (with a “Hello World” example), and Result for testing and rendering code output."><figcaption></figcaption></figure>

The **Context** panel in the Live Editor is where you provide mock or sample data that your Jinja template can reference during rendering. Since the Live Editor runs outside of an actual workflow execution, there's no real `CTX`, `TASKS`, or other runtime data available. The Context panel lets you simulate that data so you can test your templates realistically. Variables you define in the Context panel are accessed in your template using the `CTX.` prefix. If you add `"username": "Alice"` in the context, your template should reference it as `{{ CTX.username }}`, not just `{{ username }}`.

Click the **switch** button in the top right of your **Editor** panel to switch between the two available languages in the editor. The name of the language currently in use for the editor will display in blue on the button.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-17 at 11.04.07 AM.png" alt=""><figcaption></figcaption></figure>

Click **Render** to display your code's result in the **Result** pane.

Click **Share** to create a link to share your context and code in the editor, to be opened by another individual later. This is particularly helpful for sending to coworkers or Rewst support staff.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-17 at 11.06.02 AM.png" alt=""><figcaption></figcaption></figure>

## Live Editor shortcuts

* Access the Live Editor in other menus in Rewst Classic, in any fields where you see the <img src="../../.gitbook/assets/jinja-burger.png" alt="" data-size="line">button.
* Press `F1` within the editor to see menu and shortcut options
* Press `Ctrl + Space` to get the initial root options
* Add `|` to the end of your variables to access [Jinja filters](https://docs.rewst.help/documentation/jinja/list-of-jinja-filters). e.g.: `{{ ORG.ATTRIBUTES.id|default('test default string') }}`

{% hint style="info" %}
For more on how to use Jinja in Rewst, see our [Jinja documentation here](https://docs.rewst.help/documentation/jinja), and sign up for courses in [Cluck University](https://learn.rewst.io/).
{% endhint %}
