# Add Client to Rewst Crate

{% hint style="info" %}
If you’re new to Crates, read through our introductory Crate documentation [here](https://docs.rewst.help/prebuilt-automations/crates). Find the Add Client to Rewst Crate in our Crate Marketplace.\
This page will cover how to add a new child organization with the Add Client to Rewst Crate. You can find  instructions for all ways of adding new organizations [here](../../integrations/organization-variables.md#what-is-an-organization).
{% endhint %}

## What does the Add Client to Rewst Crate do?

The Add Client to Rewst Crate lets you easily use a form to add a new child organization to Rewst and map your installed integrations to the organization. Use this form every time you sign on a new customer and need to add them as a new child org in Rewst. The form will prompt you to create users and set specific [organization variables](../../integrations/organization-variables.md#what-is-an-organization-variable). Note that this Crate does not handle Microsoft Mappings.

### Workflow breakdown

1. The workflow begins with the **core\_noop** task which serves as the initialization point and processes the input data to prepare organization variables for creation by filtering out system-reserved keys and categorizing variables into integration and general configuration types.
2. The **rewst\_list\_organizations** task retrieves a list of all existing organizations within the current managing organization to check if the new client organization already exists in the Rewst platform.
3. If the organization name does not already exist in the system, the **rewst\_create\_organization** task creates a new organization in Rewst using the provided organization name and domain, establishing it as a managed organization under the current parent organization.
4. If the organization already exists, the workflow skips the creation step and retrieves the existing organization ID to proceed with configuration updates.
5. The **create\_integration\_org\_var** task iterates through the filtered integration-specific organization variables and creates them as system-category variables within the target organization, configuring essential integration settings and connection parameters.
6. The **invite\_forms\_users** task processes the list of users designated for forms-only access and sends invitations to each user with the appropriate role permissions, granting them access to execute forms within the organization.
7. The **invite\_member\_users** task processes the list of users designated for full member access and sends invitations to each user with both forms and member role permissions, providing them with broader access to the organization's resources.
8. The **create\_general\_org\_var** task iterates through the filtered general organization variables and creates them as general-category variables within the target organization, establishing configuration settings for identity providers, user management, and other operational parameters.
9. The workflow completes successfully after all organization variables have been created and all user invitations have been processed, resulting in a fully configured client organization ready for use within the Rewst platform.

## Unpack the Add Client to Rewst Crate

1. Navigate to **Marketplace** **> Crates** in the left side menu of the Rewst platform.
2.  Search for `Add Client to Rewst`.

    \
    ![](<../../../.gitbook/assets/image (95).png>)<br>
3. Click on the Crate tile to begin unpacking.
4. Click **Unpack Crate**.
5. Click **Continue**.
6. Click **Unpack**.

### Use the Crate

After unpacking, use the Crate's form to add a new child organization.

1. Navigate to **Automations > Assets > Forms** in the left side menu of your Rewst platform.
2. Search for `Add New Client to Rewst`.
3. Click **⋮ > Usages > View Direct URLs.**
4. Click on the link for the organization which contains the user you wish to manage. This will launch the form in a new tab.
5. Fill out the form following the guidance below.

#### What you need to fill out the form

Once you're in the form, you'll see the following fields:

* **Company Name**: The name of the customer you want to add to Rewst
* **Customer Primary Domain**: The domain of the company - for example, `Rewstyhouse.com .`

This form will also give you the option to map the following installed integration categories:

* **PSA**
* **RMM**
* **Network Monitoring & Remote Admin**
* **Documentation & CRM**
* **Licensing & Distribution**
* **Backup & Security**

With the above filled out and configured, you can add or invite users to the new site as the following roles:

* **Forms-only User**: Only able to view Rewst forms
* **Member Users**: Able to view forms, results, and create workflows in Rewst

<figure><img src="../../../.gitbook/assets/filling-out-the-form.gif" alt=""><figcaption><p>Filling out the Form</p></figcaption></figure>

{% hint style="info" %}
**Organization variables needed**

Setting the following variables will allow a number of Crates, including the New User Onboarding Crate, to work without further client-specific setup:

* **Primary Identity Provider**: Azure Active Directory, On-prem AD, JumpCloud
* **New User Approval Email**: used if there needs to be an approver for new user creation
* **User Name Format**: Username Format for user creation Flast, First.Last etc
* **User Start-Date Behavior**: Document the start date in the ticket and create the user now, or pause workflow until the set user creation date
* **Do not attempt to create a new o365 mailbox**: check this box if you do not want a mailbox created for the user
{% endhint %}

When all fields and desired settings have been updated, remember to click **Submit**.

{% hint style="warning" %}
**Make sure you map the Microsoft Cloud Solution Provider (CSP) tenant for your customer**

You will then want to find the CSP tenant for your new customer and map it to the Rewst organization that you have created. You can do this by navigating to **Configuration > Integrations > Microsoft Cloud Integration Bundle** to find the relevant CSP tenant.
{% endhint %}

{% hint style="info" %}
Got an idea for a new Crate? Rewst is constantly adding new Crates to our Crate Marketplace. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/crates).
{% endhint %}
