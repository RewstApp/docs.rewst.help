# Templates and scripts

{% hint style="info" %}
Templates and scripts are similar features in Rewst, though each is intended for a different purpose. Once created, they're separated by type into two sections in the platform for ease of organization and sorting. Both can be referenced in workflows.
{% endhint %}

## What is a template?

_Templates_ are used to create a standardized set of text used in several places in Rewst. For example, if you want to create a ticket and always use the same HTML for the ticket description, you would create a template. In the input, you would reference the template instead of having to type that same text each time.

To access templates, navigate to **Automations > Assets > Templates** in the left side menu of your Rewst platform.

Write templates in either Markdown or HTML language. Common examples of templates include:

Jinja templates

* Data transformations - Manipulating and formatting data between workflow tasks
* Dynamic field values - Creating dynamic inputs for action parameters
* Conditional logic - Building expressions for transitions and decision-making
* Text/message generation - Formatting emails, tickets, notifications, etc.
* List/dictionary comprehensions - Processing collections of data

Workflow templates

* Task configurations and parameters
* Transition logic between tasks
* Error handling patterns
* Sub-workflow integration
* With-items (loop) configurations

Trigger configuration templates

* Webhook triggers
* Scheduled/cron triggers
* Integration-specific triggers - e.g., ticket creation, form submission

App Builder templates

* Component configurations
* Data binding expressions
* Workflow integrations for apps

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-05 at 4.08.04 PM.png" alt="Screenshot of the Templates list view in the Rewst Automations section, showing a dark-themed interface with a left navigation menu, a top search bar and Create Template button, and a table of templates with names, descriptions, dates, attributes, and action icons."><figcaption></figcaption></figure>

Write templates in either Markdown or HTML language.

### Create a template

1. Click **+ Create**.
2. Fill in the relevant fields with the information for your template.
   1. **Name**
   2. **Description**
   3. **Tags**
3. Select the language you want to write your template in from the **Language** drop-down selector.
4. Click into your **Editor** panel on the left side of the screen to begin writing. View your progress in the **Preview** panel.
5. Scroll down and click **Submit** when finished.

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 at 10.53.50 AM.png" alt=""><figcaption><p>An example of an in-progress template, written in Markdown</p></figcaption></figure>

## What is a script?

_Scripts_ in Rewst enable you to write scripts in a straightforward and accessible manner compared to traditional programming languages. Scripting tasks can range from batch processes on a local computer to generating dynamic web pages on a web server. Scripts can be written, edited, and executed more quickly and easily than software programs.

To access scripts, navigate to **Automations > Scripts** in the left side menu of your Rewst platform.

Write Rewst scripts in any of the following languages: PowerShell, Python, YAML, Jinja. All scripts are assigned a unique URL (GUID).

<figure><img src="../../.gitbook/assets/Screenshot 2026-03-05 at 4.09.19 PM.png" alt="Screenshot of the Scripts list view in the Rewst Automations section, showing a dark-themed interface with a left navigation menu, a top search bar and Create Template button, and a table of scripts with names, descriptions, dates, attributes, and action icons."><figcaption></figcaption></figure>

Write Rewst scripts in any of the following languages: PowerShell, Python, YALM, Jinja.

### Create a script

1. Click **+ Create**.
2. Fill in the relevant fields with the information for your script.
   1. **Name**
   2. **Description**
   3. **Tags**
3. Select the language you want to write your script in from the **Language** drop-down selector.
4. Click into your **Text** panel to begin writing.
5. Scroll down and click **Submit** when finished.

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 at 2.40.44 PM.png" alt=""><figcaption></figcaption></figure>

## Jinja: Use templates and scripts within workflows

While templates and scripts are written in HTML or Markdown, they can accept small elements of Jinja to set up their elsewhere in Rewst. They allow for context variables to be set within them, which can then be referenced in workflows to allow the eventual sent message to populate with dynamic information.

In the example below, you're sending an e-mail to a new user that has been created.

```django
Hi {{ CTX.first_name }},

Welcome to Rewst!

Your email account has been provisioned and you should be able to access it at:
https://outlook.office.com/mail/

username: {{ CTX.email }}
password: {{ CTX.password }}

We're excited to have you on the team!
```

In the input for the `Send Mail` action, you would enter `{{ template("<template-id>")}}` into the action's **Message** field instead of typing out the intended message manually. This would pull your pre-written template into the body of the email when it is sent.

<figure><img src="../../.gitbook/assets/Screenshot 2025-03-21 at 2.34.55 PM.png" alt=""><figcaption></figcaption></figure>

The template ID or script ID can be taken from the URL, when editing. As an example, let's look at the URL below.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-03 at 9.21.15 AM.png" alt=""><figcaption></figcaption></figure>

The part of the URL underlined in yellow is the template ID. For this particular ID, your Jinja would read as `{{ template("768f5d45-5fe7-4c1f-b2c1-932dcbdcb1d7") }}`.

## Export and import templates and scripts

You can export a template or script to share with other Rewst customers, or create your own hard copies of template and script backups. To export a template or script as a JSON bundle, ![](<../../.gitbook/assets/Screenshot 2025-10-21 at 4.50.38 PM.png>)next to your relevant template or script in its total list.

To import a template or script bundled as a JSON file, click ![](<../../.gitbook/assets/Screenshot 2025-10-21 at 4.48.45 PM.png>) in the top right navigation bar of the list page. Then, drag and drop your file into the upload dialog that appears.
