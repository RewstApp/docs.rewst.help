# Options filter: Filtering in forms

## What is options filter?

The _options filter_ makes customizing fields within forms straightforward for those who want to add filtering without updating an options generator workflow. It takes inputs, filters them, and produces an output agnostic of the data source.

Options filter works for the following form field types:

* [Dropdown](https://docs.rewst.help/documentation/automations/forms/intro-to-forms#drop-down)
* [Radio Button](https://docs.rewst.help/documentation/automations/forms/intro-to-forms#radio-buttons)
* [Multi-Select ](https://docs.rewst.help/documentation/automations/forms/intro-to-forms#multi-select)

Option generators are still a fantastic option for those who need a more powerful, in-depth, solution. We cover what these are and how to use them in Cluck University's [Rewst Foundations](https://learn.rewst.io/creating-an-option-generator) . If you’ve already taken our courses and want a refresher, see our documentation on option generators [here](https://docs.rewst.help/documentation/workflows/workflow-generated-options).

## Options filter guidance

* Modifying a form using the options filter will work for both parent and child organizations, as long as data formatting is set up the same way for both organizations.
* Add as many conditions as desired.
* Access the options filter feature in our standard form builder.&#x20;
* Options filter works in the context of the current organization.&#x20;

## Practical uses for options filter

* Say you offer 10 different types of licenses, but your users only ever use a single Business Premium type. Filtering down to just that license would simplify the list, and leave no room for error.
* Using a multi-select form field, present multiple licenses to a user to be filtered down to a specific set of licenses.
* Filter out admins from a total list of users, to create a cleaner list for copying into user onboarding.
* When offboarding a user, you may want to exclude a list of specific people to prevent accidental offboarding of key individuals, like the CEO.
* Hide on.microsoft email domains that are purely administrative, to provide a cleaner list.

### Detailed options filter example

You work at an MSP and are building a license request form for technicians. Your customer, XYZ Corp, only purchases Microsoft 365 Business Premium licenses, not E3, E1, or other license types. To prevent techs from accidentally selecting the wrong license type, which would lead to support tickets and billing issues, you want the drop-down in your form to only show Business Premium.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-05 at 4.03.54 PM.png" alt=""><figcaption><p>Building the form with the different license types</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-05 at 4.04.18 PM.png" alt=""><figcaption><p>What is seen after clicking <strong>filter options</strong></p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-05 at 4.04.49 PM.png" alt=""><figcaption><p>Filtering using the <strong>simple</strong>  logic option. The $.label equals Microsoft 365 Business Premium. Note that you haven't clicked <strong>apply filter</strong> on the bottom right, so there are still 4 filtered options shown under <strong>Dropdown Options</strong>.</p></figcaption></figure>



<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-05 at 4.06.14 PM.png" alt=""><figcaption><p>What you see after you click <strong>apply filter</strong>. Now, there's only 1 filtered option: Microsoft 365 Business Premium</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-05 at 4.05.51 PM.png" alt=""><figcaption><p>A preview of the form, or a preview of what the end user would see. Only one option would display.</p></figcaption></figure>

## Options filter dialog

Click **Filter Options** under the **Dynamic Options** submenu of the right side forms menu. This will open the **Create Option Filters** dialog. In the dialog, you’ll see two submenus: **Dropdown Options** and **Options Filter**.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-11-20 at 11.47.53 AM.png" alt=""><figcaption></figcaption></figure>



### All Options

The **All Options** drop-down selector holds all of the options which you’ve set in the standard form builder right side menu. Adding more options in that menu will populate those options into your drop-down selector.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-25 at 5.02.18 PM.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Screenshot 2025-06-03 at 1.06.45 PM.png" alt=""><figcaption></figcaption></figure>

The **Filtered Options** drop-down selector holds a list of your selected options after applying the filter. It acts as a preview for what to expect from your filtering.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-06-03 at 1.07.15 PM.png" alt=""><figcaption></figcaption></figure>

If your form field uses a custom options filter, there will be a badge indicator in the top right of the field.

<figure><img src="../../../.gitbook/assets/indicator.png" alt=""><figcaption></figcaption></figure>



#### The JSON interface

Toggle from the default **Simple** view to the **JSON** view. This will switch to show the code of the filter. You may have a scenario where your desired filter is more complex than just label and value, such as ID. Using this code editor, filter out custom objects from complex queries.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-25 at 4.36.39 PM.png" alt=""><figcaption></figcaption></figure>

#### Jinja for options filters

If you manage many organizations, use Jinja in options filters to scale filtering logic without manually configuring filters for every suborganization. When simple boolean logic operators feel limiting, go straight to Jinja for greater customization.&#x20;

{% hint style="info" %}
The CTX variable you want to reference will always be called `options`.
{% endhint %}

<figure><img src="../../../.gitbook/assets/Screenshot 2025-06-03 at 1.05.33 PM.png" alt=""><figcaption></figcaption></figure>

### AND and OR conditional options filtering

{% hint style="info" %}
Using the options filter for forms will require a basic understanding of Boolean. If you’re new to the topic, be sure to complete our Clean Automation course in Cluck University before trying out this feature.
{% endhint %}

The options filter works off of two boolean operators, which are used to build queries for a variety of filtering situations.

1. **AND** sets that all conditions must be true to be filtered into the returned result. E.g., Red AND white would count only items with both those characteristics.
2. **OR** sets that either of several conditions can be true to be filtered into the return result E.g., Red OR white would count items with either of those characteristics.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-06-03 at 1.11.33 PM.png" alt=""><figcaption></figcaption></figure>

Click **X** to the right of any added rule or group to delete it from your options filter list.

Click **+Rule** to add a filter field, which is customizable by a list of parameters. Choose from either **$.value** or **$.label**, then choose from the long drop-down list of conditions. E.g., **$.value equals `15`** would filter all results with a value of exactly 15.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-25 at 4.28.47 PM.png" alt=""><figcaption></figcaption></figure>

In Boolean logic, a _group_ refers to a set of terms or expressions that are treated as a single unit by using parentheses, allowing you to perform Boolean operations on them together. Essentially, it defines the order of operations by grouping certain elements within a complex logical statement.

When you want to combine multiple Boolean operations in a specific way, you enclose them within parentheses to indicate that these operations should be calculated first.

By grouping terms, you can control the order in which Boolean operators like AND and OR are applied. Use the +**Group** button to define your conditions more precisely. For example:

* Without grouping, A OR B AND C would be evaluated as: A OR (B AND C) due to precedence rules
* With grouping, (A OR B) AND C forces OR to be evaluated before AND.

## Forms and options filter

### Use the options filter in a form

1. Navigate to **Automations > Assets > Forms > + Add**.
2. Name your form, and click **Submit**.
3. Drag one of the three applicable form fields onto the form builder canvas. Remember, options filter is only available for Radio Buttons, Dropdown, and Multi-Select.
4. Click on the dragged form field to open the right side menu.
5. Click on **Filter Options**. This will open the **Create Option Filters** dialog.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-25 at 11.02.23 AM.png" alt=""><figcaption></figcaption></figure>

6. Set up your desired filters using the AND and OR options, with relevant use of the **+Rule** and **+Group** buttons.
7. Click **apply filter** at the bottom right of your screen.
8. Click **Close** when finished. The option filter will automatically save and be applied to your form. Note that you’ll still need to click **Save** at the top right of your form builder screen to update these changes within your form.

![](<../../../.gitbook/assets/Screenshot 2025-02-26 at 12.28.51 PM.png>)



### Options filter and syncing of forms

The greatest advantage of the options filter is that it allows for the overriding of a form. Synchronized forms will block you from modifying attributes to prevent sync malfunction, by default. Under filter options in the form builder, you’ll find an **Override** button at the bottom right. Clicking will override this individual filter. Note that if you have multiple filters, and want to modify all of them, you’ll need to click **Override** for each filter.

<figure><img src="../../../.gitbook/assets/Screenshot 2025-02-25 at 5.14.54 PM.png" alt=""><figcaption></figcaption></figure>

### Org-based preview and org-specific instances

Use the org context drop-down selector to choose the child organization that you'd like to preview, and see how the form will function for that specific organization. Previews don't require cloning, and won't affect the saved form configurations except for the options filter. The options generator will display data as if the form were triggered in just that specific organization.  The default-set options filter will be used if no custom filters were provided for the selected organization.

Click the drop-down selector to view and chose from your list of all total organizations.

<div data-full-width="false"><figure><img src="../../../.gitbook/assets/Screenshot 2025-06-03 at 12.16.25 PM.png" alt=""><figcaption></figcaption></figure></div>

Selecting the preview organization sets the context of the form builder. and opening the preview dialog will use that organization's context to generate the correct preview, tailoring filtering logic for each instance without duplicating forms or unsyncing fields.

{% hint style="info" %}
By default, a field will inherit the parent organization's filter unless if it explicitly overridden. <br>
{% endhint %}
