# Rewst actions

## Available Rewst actions

_Rewst actions_ provide you the tools to effectively manage and customize your environment. From setting up organizations and users to associating with multi-tenanted objects, these actions form the foundation of your interaction with the platform. This guide explores each of the available actions in detail, providing you a clear path to maximize the potential of your Rewst functionality.

{% hint style="info" %}
Click to expand each of the Rewst action accordions below to see its documentation.
{% endhint %}

<details>

<summary>Associate External Object action</summary>

Linking external resources, like tickets from a PSA system, to your workflow executions can streamline management and enhance traceability. This action connects an external system's resource to your workflow. It optionally fails if a pre-existing link is detected, and runs under specified user or default user.

**Parameters:**

* **identifier:** Unique identifier of the external resource you'd like to associate.
* **reference\_id:** Reference for the external resource that you will be able to call back on.
* **run\_as\_user (optional):** Defined user's ID or default user's ID (if blank) for running the task.
* **fail\_on\_conflict (optional):** Set this option to true if you don't want to overwrite any existing `reference_id`/`identifier` pair already exists.

**Output:**

The resulting task's output returns the verified information about the associated external object.

</details>

<details>

<summary>Bulk Create Organizations action</summary>

Create multiple organizations at once within Rewst.

**Parameters:**

* Managing **Organization ID:** The ID of the managing organization. If not provided, the organization that initiated the operation will be set as the managing organization.
* Organizations (Required): List of organization details to be created. Each entry in the list should contain the following parameters:
  * Is Enabled: Boolean indicating if the organization should be enabled.
  * Name: The name of the organization in Rewst. The name must be unique.
  * Domain: The domain name of the organization's website, excluding protocol.

**Output:** Outputs a list of newly created organizations, each with its corresponding Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Bulk Upsert Organization Variables action</summary>

Performs a bulk operation to create or update organization variables.

**Parameters:**

* **Organization Variables:** A list of objects where each object represents an organization variable to be created or updated. Each object must include:
  * **Name:** The name of the organization variable.
  * **Value:** The value of the organization variable.
  * **Category:** The category used to define the organization variable. Options include: `general`, `contact`, `system`, `secret`.
  * **Use as default:** If true, this variable's value will be used as the default value for any managed organizations without a defined value.
  * **Organization ID:** (Optional) The ID of the organization.

**Output:** Returns a list of objects. Each object represents an upserted organization variable and includes properties such as ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Create Organization action</summary>

Create a single organization within Rewst.

**Parameters:**

* Name (Required): The name of the organization to be created. This name must be unique within Rewst.
* Domain (Optional): The domain of the new organization, excluding protocol.
* Managing **Organization ID:** Identifier of the managing organization. If not provided, the organization that initiated the operation will be set as the managing organization.
* Is Enabled (Optional, default is true): A boolean indicating whether the new organization is enabled or not.

**Output:** Outputs the details of the newly created organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Create Organization Variable action</summary>

Creates a new organization variable that's available for use within an organization's workflow context.

**Parameters:**

* **Name:** The name of the organization variable.
* **Value:** The value of the organization variable.
* **Category:** The category used to define the organization variable. Options include: `general`, `contact`, `system`, `secret`.
* **Use as default:** If true, this variable's value will be used as the default value for any managed organizations without a defined value.
* **Organization ID:** (Optional) The ID of the organization.

**Output:** Returns an object containing the new variable details including the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Create Template action</summary>

Lets you create a new template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters:**

* **Name:** The name of the template.
* **Description:** A brief description of the template.
* **Body:** The actual template content.
* **Content Type:** The type of content used in the template.
* **Language:** The language used in the template. Options include: `html`, `markdown`, `powershell`, `python`, `yaml`.

**Output:** The action returns the newly created template's information, including its `id`.

</details>

<details>

<summary>Delete Organization Variable action</summary>

Deletes a specific organization variable for a selected organization using the variable's name.

**Parameters:**

* **Organization ID:** The ID of an organization.
* **Name:** The name of the organization variable to be deleted.

**Output:** Returns an object indicating the success of the operation, including the name of the deleted variable and the ID of the organization from which it was deleted.

</details>

<details>

<summary>Delete Template action</summary>

This action lets you delete an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters:**

* **Template ID**: The ID of the template you wish to delete.

**Output:** The action does not return any specific output, but its execution status indicates whether the deletion was successful.

</details>

<details>

<summary>Delete User Invite action</summary>

Delete a user invite from your organization in Rewst.

**Parameters:**

* **Email:** Email address of the user invite to delete.

**Output:** The returned object shows the number of invites deleted.

</details>

<details>

<summary>Export Object action</summary>

The `rewst_export_object` task is a Rewst platform action that exports Rewst objects— workflows, triggers, forms, templates, sites, or pages— into a portable bundle format that can be shared, backed up, or imported into other Rewst environments. The exported bundle includes cryptographic signing to ensure the integrity and authenticity of the exported data.

**Parameters:**&#x20;

* **object\_type** - required: The type of object to export
  * Options: workflow, trigger, form, template, site, page
* **object\_id** - required: The unique ID of the specific object to export
  * Uses a dynamic reference that populates available objects based on the selected object type

**Outputs:**

The action returns a bundle object containing:

* objects: A mapping of serializable keys to their serialized objects (the actual exported data)
* signing: Security verification details including:
  * cert: PEM-encoded X.509 public certificate for signature verification
  * hash: HMAC hashing algorithm name used for the signature
  * signature: base64-encoded signature for integrity verification
* version: Version number of the export bundle format
* exported\_at: Timestamp of when the bundle was created

**Use Cases:**

* Create portable backups of important workflows or other objects
* Move objects between different Rewst environments
* Share workflows or templates with other organizations
* Create snapshots of objects at specific points in time



</details>

<details>

<summary>Generic GraphQL request action</summary>

This action has its own separate documentation page [here](generic-graphql-request-action.md).&#x20;

</details>

<details>

<summary>Get External Reference action</summary>

This action facilitates the retrieval of details about the any external integration or manually set references. You can use it to fetch all external integration references associated with a specific organization in Rewst or to find the organization and workflow execution associated with a specific external reference ID. It runs under specified user credentials or default user, but requires organization ID for context.

**Parameters:**

* **org\_id:** ID of the organization in Rewst.
* **identifier:** Unique identifier of the external resource.
* **reference\_id:** Reference ID of the external resource.
* **run\_as\_user (optional):** Specify user credentials.

**Output:**

Returns detailed information about the external reference(s), such as the `org_id` in Rewst linked to it, the type of `identifier`, and the external `reference_id`. This information is helpful for cross-system data synchronization and management.

***

</details>

<details>

<summary>Get Form action</summary>

Retrieves details about a specific form in the system.

**Parameters:**

* **Name:** The name of the form.
* **ID:** The ID of the form.

**Output:** The action returns information about the specified form.

</details>

<details>

<summary>Get Microsoft CSP Customer action</summary>

Get data for a single Microsoft CSP customer in Rewst.

**Parameters:**

* **CSP Integration Configuration ID**: The ID of a Microsoft integration configuration in Rewst.

</details>

<details>

<summary>Get Organization action</summary>

Retrieve data for a single organization in Rewst.

**Parameters:**

* **Organization ID:** Identifier of the organization to fetch data for. This ID is unique for each organization within Rewst.

**Output:** Outputs the details of the organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Get Organization Variable action</summary>

Retrieves a specific organization variable for a selected organization using the variable's name or value.

**Parameters:**

* **Name:** (Optional) The name of the organization variable.
* **Organization ID:** (Optional) A dropdown list of the labels that correlate with the ID of an organization you'd like to retrieve.
* **Value:** (Optional) The value of the organization variable.

**Output:** Returns an object (or list of objects) representing the organization variable, including the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Get Template action</summary>

Lets you retrieve the details of an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters:**

* **Template ID**: The ID of the template you wish to retrieve.

**Output:** The action returns the requested template's information, including its `name`, `description`, `body`, `content_type`, and `language`.

</details>

<details>

<summary>Get Trigger action</summary>

Retrieves details about a specific trigger in the system.

**Parameters:**

* **Name:** The name of the trigger.
* **ID:** The ID of the trigger.
* **Enabled:** A boolean value that indicates whether the trigger is enabled or not.

**Output:** The action returns information about the specified trigger.

</details>

<details>

<summary>Get User action</summary>

Get user by email or ID in Rewst.

**Parameters:**

* **ID:** The ID of a user in Rewst.
* **Organization ID:** The ID of an organization in Rewst.
* **Email address:** The email of a user in Rewst.

**Output:** The returned object includes the user's details like ID, role, organization ID, assigned role IDs, username, and a boolean indicating superuser status.

</details>

<details>

<summary>Invite User to Rewst action</summary>

Invite a user to your organization in Rewst.

**Parameters:**

* **Email:** Email address of the user to invite.
* **Roles:** Role IDs to assign to user.

**Output:** The returned object includes the invite details such as ID, email, organization ID, assigned role IDs, a boolean indicating acceptance status, and the ID of the inviter.

</details>

<details>

<summary>Link Microsoft CSP Customer action</summary>

Link one or more Rewst organizations to a microsoft CSP customer in Microsoft

**Parameters:**

* **CSP Integration Configuration ID**: The ID of a Microsoft CSP integration configuration in Rewst.
* **Microsoft CSP Customer ID**: The ID of the Microsoft CSP Customer in Rewst that you want to link your organization or organizations to.
* **Organization IDs**: The list of Rewst organization IDs to link.

**Output:** The returned object lists a confirmation of the linked organizations

</details>

<details>

<summary>List Apps action</summary>

Lists all apps, also known as sites, associated with the current organization in Rewst.

**Parameters:**

* **Run as user - optional:** The ID of the user to run the query as. If omitted, defaults to the workflow's context user.

**Output:** Returns a list of apps, including details such as ID, name, and organization association.

</details>

<details>

<summary>List Forms action</summary>

Retrieves a list of all forms in the system.

**Parameters:** No parameters are required for this action.

**Output:** The action returns a list of all forms, each item including information about a form.

</details>

<details>

<summary>List Forms With Granular Permissions</summary>

The rewst\_list\_forms\_with\_granular\_permissions task retrieves a list of all forms in your Rewst organization that the specified user has permission to access, taking into account granular permission settings. If run\_as\_user is set to null,  it will use the default organization user. This action is useful for building dynamic interfaces or workflows that need to work with forms based on user permissions, ensuring users only see forms they have access to.

**Parameters:**

run\_as\_user - required: The user ID that the action will run as. If not specified, the default user for your organization will be used.

**Outputs:**

The task returns an array of form objects, where each form contains:

| Field                | Type    | Description                                                                                  |
| -------------------- | ------- | -------------------------------------------------------------------------------------------- |
| **id**               | String  | Unique identifier for the form                                                               |
| **name**             | String  | Display name of the form                                                                     |
| **description**      | String  | Form description                                                                             |
| **org\_id**          | String  | Organization ID that owns the form                                                           |
| **created\_at**      | String  | Timestamp when the form was created                                                          |
| **updated\_at**      | String  | Timestamp when the form was last modified                                                    |
| **is\_synchronized** | Boolean | Whether the form is synchronized                                                             |
| **tags**             | Array   | List of tags associated with the form (each tag has `id` and `name`)                         |
| **triggers**         | Array   | List of triggers associated with the form (each trigger has `id`, `name`, and `workflow_id`) |



</details>

<details>

<summary>List Integrations For Organization action</summary>

This action retrieves a comprehensive list of integrations installed for a specific organization in Rewst, providing a detailed overview of each integration's attributes.

**Parameters:**

* **Organization ID:** The unique identifier for an organization in Rewst. This parameter is required to fetch the specific integration details pertinent to the organization.

**Output:**

The action generates a detailed list of integrations, including:

* **Integration ID, Name, and Reference:** Basic identifiers providing clarity on each integration.
* **Pack Configurations:** In-depth details of configurations applied to each integration, offering insights into their setup and customization.
* **Applied Triggers:** Information on workflow triggers linked to each integration, useful for understanding operational dynamics.
* **Foreign Object References:** Crucial data points that link integrations to external references, enhancing cross-platform data synchronization and management.

</details>

<details>

<summary>List Microsoft CSP Customer action</summary>

Get a list of Microsoft CSP customers in Rewst.

**Parameters:**

* **CSP Integration Configuration ID**: The ID of a Microsoft integration configuration in Rewst.
* **Microsoft CSP Customer ID**: The ID of the Microsoft CSP Customer in Rewst that you want to link your organization or organizations to.
* **Organization IDs**: The list of Rewst organization IDs to link.

</details>

<details>

<summary>List Organizations action</summary>

Fetch a list of all organizations in Rewst.

**Parameters:**

* Managing **Organization ID:** Identifier of the managing organization to fetch organizations for. This ID is unique for each organization within Rewst.
* Name (Optional): Name of the organization to search for. The name must be unique within Rewst.

**Output:** Outputs a list of organizations, each with its corresponding Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>List Organization Variables action</summary>

Lists all organization variables visible to the selected organization.

**Parameters:**

* **Organization ID:** (Optional) A dropdown list of the labels that correlate with the ID (visible in the code editor window) of an organization you'd like to retrieve.

**Output:** Returns a list of objects. Each object represents an organization variable and includes the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>List Templates action</summary>

Lets you retrieve a list of all existing templates. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters:** _No parameters are required for this action._

**Output:** The action returns a list of all templates, with each entry including information about a template, such as its `id`, `name`, `description`, `body`, `content_type`, and `language`.

</details>

<details>

<summary>List Triggers action</summary>

&#x20;Retrieves a list of all triggers in the system.

**Parameters:** No parameters are required for this action.

**Output:** The action returns a list of all triggers, each item including information about a trigger.

</details>

<details>

<summary>List User Invites to Rewst action</summary>

Get user invite list by your organization in Rewst.

**Parameters:** _No parameters needed for this action._

**Output:** The returned list includes a list of user invite objects. Each object contains the invite's ID, email, organization ID, assigned role IDs, a boolean indicating acceptance status, and the ID of the inviter.

</details>

<details>

<summary>List Users by Organization action</summary>

Get user list and optionally invited users by your organization in Rewst.

**Parameters**:

* **Include User Invites?:** Whether or not to include user invites in the results.
* **Which Invites:** Which invitees to include. Can be `all`, `accepted`, or `pending`.

**Output**: A list of users with details like ID, role, organization ID, assigned role IDs, username, and a boolean indicating superuser status.

</details>

<details>

<summary>List Workflows actions</summary>

This action retrieves a comprehensive list of all workflows in your Rewst organization, giving you visibility into your automation library. This action is particularly useful for workflow management tasks, reporting, and as a starting point for more complex workflow operations that require workflow IDs.

**Parameters:**

* `run_as_user` (optional): Specifies which user the action should run as. If not provided, it uses your organization's default user.

**Output:**

The action returns detailed information for each workflow:

* `id`: Unique workflow identifier
* `name`: The workflow's display name
* `tags`: Array of tags assigned to the workflow
* `org_id`: Organization ID where the workflow belongs
* `triggers`: Array of associated triggers for the workflow
* `created_at`: Timestamp when the workflow was created
* `updated_at`: Timestamp of the last modification
* `organization`: Detailed organization information
* `unpacked_from`: Template source information (if the workflow was created from a template)
* `cloned_from_id`: Source workflow ID (if the workflow was cloned from another)

**Common use cases:**

* Workflow Inventory: Get a complete overview of all workflows in your organization
* Trigger Analysis: Identify which workflows have active triggers
* Workflow Management: Use the returned workflow IDs for subsequent operations on specific workflows
* Organizational Reporting: Generate reports on workflow usage and organization

{% hint style="info" %}
Note that this action won't return workflow notes. To retrieve that information, use the [Rewst - Generic GraphQL Request](rewst-actions.md#generic-graphql-request-action) action to query `workflowNotes` .
{% endhint %}

</details>

<details>

<summary>List Workflow Executions With Time Savings action</summary>

The `rewst_list_workflow_executions_with_time_savings` task is an action from the Rewst integration that lists workflow executions with calculated time savings data. This action retrieves execution data and calculates how much time has been saved through automation. It provides comprehensive analytics about workflow performance and efficiency.

* Retrieves execution data including total executions, seconds saved, workflow names, and organization information
* Calculates time savings for automated workflows
* Filters executions by date, status, and organization
* Groups results either by individual workflow or by sub-organization

**Parameters:**

* **`updated_at`** (required): Include any executions updated after this date (datetime format)
* **`workflow_status`** (optional): Filter by execution status (`succeeded`, `failed`, or `running`)
* **`group_by_sub_org`** (optional): Choose whether to group results by sub-organization (default: false, groups by workflow)
* **`run_as_user`** (optional): The user that the action will run as

**Output:**

The action returns data including:

* `ran_for_org`: Organization identifier
* `workflow_id`: Unique workflow identifier
* `seconds_saved`: Calculated time savings in seconds
* `workflow_name`: Name of the workflow
* `total_executions`: Total number of executions

</details>

<details>

<summary>Unlink Microsoft CSP Customer action</summary>

Unlink one or more Rewst organizations from a Microsoft CSP customer in Rewst.

**Parameters:**

* **CSP Integration Configuration ID**: The ID of a Microsoft integration configuration in Rewst.
* **Microsoft CSP Customer ID**: The ID of the Microsoft CSP Customer in Rewst that you want to link your organization or organizations to.
* **Organization IDs**: The list of Rewst organization IDs to link.

**Output:** The returned object lists a status for the unlink action

***

</details>

<details>

<summary>Update Organization action</summary>

Update details of an existing organization within Rewst.

**Parameters:**

* **Organization ID:** Identifier of the organization to be updated. This ID is unique for each organization within Rewst.
* Name (Optional): New name for the organization. This name must be unique within Rewst.
* Domain (Optional): New domain for the organization, excluding protocol.
* Is Enabled (Optional): Updated enabled status for the organization. It is a boolean value.

**Output:** Outputs the updated details of the organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Update Template action</summary>

This action lets you update the details of an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters:**

* **Template ID:** The ID of the template you wish to update, it is a required field.
* **Body:** The new content of the template.
* **Content Type:** The new type of content used in the template. The options are `message` and `script`.
* **Description:** A brief description of the template.
* **Language:** The new language used in the template. The options include: `html`, `markdown`, `powershell`, `python`, `yaml`.

**Output:** The action returns the updated template's information, including its `id`.



</details>

<details>

<summary>Update Trigger action</summary>

The rewst\_update\_trigger task is used to modify existing workflow triggers within the Rewst platform. This action allows you to update properties of a trigger such as its name, enabled status, description, and the user it runs as. This task is particularly useful for dynamically managing trigger states within workflows, such as enabling ordisabling triggers based on certain conditions or updating trigger configurations programmatically.

**Parameters:**

* Trigger\_id - required: The ID of the trigger to be updated
* Name: New name for the trigger
* Enabled: Whether the trigger should be enabled or disabled
* Description: New description for the trigger
* Run\_as\_user: The user ID that the trigger will run as (defaults to organization default user if not specified)

**Outputs:**

The action returns an object containing the updated trigger information:

* ID: The trigger ID
* Name: The trigger name
* Enabled: Whether the trigger is enabled or not
* Description: The trigger description
* Criteria: The trigger criteria
* Parameters: The trigger parameters
* Workflow\_ID: The associated workflow ID
* Form: Form configuration objects
* TriggerType: Trigger type information
* Organization: Organization information
* ActivatedForOrgs: Organizations where the trigger is activated

</details>

## App Builder-specific Rewst actions

{% hint style="info" %}
These Rewst actions are for use with [App Builder](../../app-builder/) only. Don't use them for general workflow building on the Workflow Builder canvas.
{% endhint %}

<details>

<summary>List Pages action</summary>

Lists all pages for a specified app in Rewst.

**Parameters:**

* **App ID:** The ID of the app for which to fetch pages.
* **Run as user - optional:** The ID of the user to run the query as.

**Output:** Returns a list of pages within the specified app, including each page's ID, name, and metadata.

</details>

<details>

<summary>List Page Elements action</summary>

Lists all elements within a specific page in an app, including their Element IDs and key properties.

**Parameters:**

* **Page ID:** The ID of the page whose elements you want to retrieve.
* **Run as user - optional:** The ID of the user to run the query as.

**Output:** Returns a dictionary mapping element IDs to their properties, including type, Craft ID, and other element-specific details.

</details>

<details>

<summary>Update Text Element Content action</summary>

Updates the text-based content of a page element— such as a text block, button, link, HTML container, markdown block, or accordion— within a specified page.

**Parameters:**

* **Content:** The new text content to set for the element.
* **Page ID:** The ID of the page containing the element to update.
* **Element ID:** The ID of the page element whose text content you want to update.
* **Run as user - optional:** The ID of the user to run the query as.

**Output:** Returns the updated element's details, including confirmation of the new text content.

</details>















