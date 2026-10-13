# Rewst actions

## Available Rewst actions

_Rewst actions_ provide you the tools to effectively manage and customize your Rewst Classic environment. From setting up organizations and users to associating with multi-tenanted objects, these actions form the foundation of your interaction with the platform. This guide explores each of the available actions in detail, providing you a clear path to maximize the potential of your Rewst functionality.

{% hint style="info" %}
Click to expand each of the Rewst action accordions below to see its documentation.
{% endhint %}

<details>

<summary>Associate External Object action</summary>

This action links an external resource (like a PSA ticket ID) to the current workflow execution. This creates a traceable relationship between a Rewst execution and an object in another system. Call this early in a workflow triggered by a PSA ticket or other external event. It lets you correlate executions to external objects for auditing and lookup purposes.

**Parameters**

* **identifier:** Unique identifier of the external resource you'd like to associate.
* **reference\_id:** Reference for the external resource that you will be able to call back on.
* **run\_as\_user (optional):** Defined user's ID or default user's ID (if blank) for running the task.
* **fail\_on\_conflict (optional):** Set this option to true if you don't want to overwrite any existing `reference_id`/`identifier` pair already exists.

**Output**

None

</details>

<details>

<summary>Bulk Create Organizations action</summary>

This action creates multiple Rewst organizations in a single action call, rather than looping through Create Organization actions individually. It's ideal for MSP onboarding automation where you're provisioning multiple client orgs at once. Feed in a list built from a PSA or spreadsheet import.

**Parameters**

* **Managing** **Organization ID:** The ID of the managing organization. If not provided, the organization that initiated the operation will be set as the managing organization.
* **Organizations**, Required: List of organization details to be created. Each entry in the list should contain the following parameters:
  * **Is Enabled**: Boolean indicating if the organization should be enabled.
  * **Name**: The name of the organization in Rewst. The name must be unique.
  * **Domain**: The domain name of the organization's website, excluding protocol.

**Output**

* An array of created organization objects is returned, each with `id`, `name`, `domain`, `org_slug`, `managing_org_id`, and `managingOrg`.

</details>

<details>

<summary>Bulk Upsert Organization Variables action</summary>

This action creates or updates multiple org variables in one call. If a variable with the given name already exists for the org, it's updated; otherwise it's created. It's the go-to action for provisioning a new client org with all its required org variables in one shot. Build the array in a noop transition data alias, then pass it here.

**Parameters**

* **Organization Variables:** A list of objects where each object represents an organization variable to be created or updated. Each object must include:
  * **Name:** The name of the organization variable.
  * **Value:** The value of the organization variable.
  * **Category:** The category used to define the organization variable. Options include: `general`, `contact`, `system`, `secret`.
  * **Use as default:** If true, this variable's value will be used as the default value for any managed organizations without a defined value.
  * **Organization ID**, optional: The ID of the organization.

**Output**

* Returns a list of objects. Each object represents an upserted organization variable and includes properties such as ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Create Organization action</summary>

This action creates a single organization within Rewst. Use it in client onboarding workflows. Always check if the org already exists first via List Organizations to avoid duplicate creation errors.

**Parameters**

* **Name**, required: The name of the organization to be created. This name must be unique within Rewst.
* **Domain**, optional: The domain of the new organization, excluding protocol.
* **Org Slug**: A kebab-case unique identifier, auto-generated if not provided.
* **Is Enabled**, Optional, default is true: A boolean indicating whether the new organization is enabled or not.
* **Tag IDs**: tags to apply to the org.
* **Managing Organization ID:** Identifier of the managing organization. If not provided, the organization that initiated the operation will be set as the managing organization.

**Output**

* Outputs the details of the newly created organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Create Organization Variable action</summary>

Creates a new organization variable that's available for use within an organization's workflow context. Use it when you need to set a single config value for an org. For setting many at once, use the Bulk Upsert Organization Variables action instead.

**Parameters**

* **Name:** The name of the organization variable.
* **Value:** The value of the organization variable.
* **Organization ID**, optional: The ID of the organization.
* **Use as default:** If true, this variable's value will be used as the default value for any managed organizations without a defined value.
* **Category:** The category used to define the organization variable. Options include: - `general`, `contact`, `system`, `secret`.
* **Pack Config ID**: Associates the variable with a specific integration config if relevant.

**Output**

* The action returns an object containing the new variable details including the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Create Template action</summary>

This action programmatically creates a new Rewst Template— message or script— within the organization. It's useful in provisioning workflows where you need to dynamically generate and store templates per client org.

**Parameters**

* **Name:** The name of the template.
* **Description:** A brief description of the template.
* **Body:** The actual template content.
* **Content Type:** The type of content used in the template.
* **Language:** The language used in the template. Options include: `html`, `markdown`, `powershell`, `python`, `yaml`.

**Output**

* The action returns the newly created template's information, including its `id`.

</details>

<details>

<summary>Delete Organization Variable action</summary>

This action deletes a specific organization variable for a selected organization using the variable's name. Use it in offboarding or cleanup workflows to remove org variables that are no longer needed. Always confirm the variable exists first if you want to avoid silent failures

**Parameters**

* **Organization ID:** The ID of an organization.
* **Name:** The name of the organization variable to be deleted.

**Output**

* The action returns an `is_deleted` object indicating the success of the operation, including the name of the deleted variable and the ID of the organization from which it was deleted.

</details>

<details>

<summary>Delete Template action</summary>

This action lets you delete an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization.

**Parameters**

* **Template ID**: The ID of the template you wish to delete.

**Output**

None

</details>

<details>

<summary>Delete User Invite action</summary>

This action cancels and removes a pending user invite from your Rewst organization. Use it in offboarding or access revocation workflows to clean up any outstanding invites for a user who should no longer have access.

**Parameters**

* **Email:** Email address of the user invite to delete.

**Output**

* The returned object shows the number of invites deleted.

</details>

<details>

<summary>Export Object action</summary>

The `rewst_export_object` task is a Rewst platform action that exports Rewst objects— workflows, triggers, forms, templates, sites, or pages— into a portable bundle format that can be shared, backed up, or imported into other Rewst environments. The exported bundle includes cryptographic signing to ensure the integrity and authenticity of the exported data.

**Parameters:**

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

This action has its own separate documentation page [here](generic-graphql-request-action.md).

</details>

<details>

<summary>Get External Reference action</summary>

This action facilitates the retrieval of details about the any external integration or manually set references. You can use it to fetch all external integration references associated with a specific organization in Rewst or to find the organization and workflow execution associated with a specific external reference ID. It runs under specified user credentials or default user, but requires organization ID for context.

**Parameters**

* **org\_id**: ID of the organization in Rewst.
* **identifier**: Unique identifier of the external resource.
* **reference\_id**: Reference ID of the external resource.
* **run\_as\_user**, optional: Specify user credentials.

**Output**

The action returns detailed information about the external reference, such as the `org_id` in Rewst linked to it, the type of `identifier`, and the external `reference_id`. This information is helpful for cross-system data synchronization and management.

</details>

<details>

<summary>Get Form action</summary>

This action retrieves a single Rewst Form by ID or name. Use it when you need to dynamically reference a form's metadata or trigger information within a workflow.

<br>

**Parameters**

* **Name:** The name of the form.
* **ID:** The ID of the form.

**Output**

* The action returns information about the specified form: `id`, `name`, `org_id`, `triggers`, `tags`, `description`, `is_synchronized`, `created_at`, `updated_at`.

</details>

<details>

<summary>Get Microsoft CSP Customer action</summary>

This action retrieves a single Microsoft CSP customer record from Rewst's CSP integration data. Use it to look up a specific CSP customer by tenant ID or company name before linking or unlinking it to a Rewst org.

**Parameters**

* **CSP Integration Configuration ID**: The ID of a Microsoft integration configuration in Rewst.
* **Where**, filter object: Filter by `tenantId`, `companyName`, `hasConsent`, or `linkedOrganizations.id`

**Output**

* The action returns the CSP customer record with `id`, `tenant_id`, `company_name`, `has_consent`, `csp_tenant_id`, and `linked_organizations`.

</details>

<details>

<summary>Get Organization action</summary>

This action retrieves data for a single organization in Rewst. Use it when you need to confirm an org's details or retrieve its metadata mid-workflow. Often used after Create Organization to confirm the result.

**Parameters**

* **Organization ID:** Identifier of the organization to fetch data for. This ID is unique for each organization within Rewst.

**Output**

* The action returns the details of the organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Get Organization Variable action</summary>

This action retrieves a specific organization variable for a selected organization using the variable's name or value. Use it when you need to check if a specific org variable exists or retrieve its current value programmatically. Note: secret variables will be masked — use `ORG.VARIABLES` in Jinja to access secret values at runtime instead.

**Parameters**

* **Name**, optional: The name of the organization variable to look up.
* **Organization ID**, optional: A drop-down list of the labels that correlate with the ID of an organization you'd like to look in.
* **Value**, optional: Filter by the value of the organization variable.

**Output**

* The action returns an object or list of objects representing the organization variable, including the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>Get Template action</summary>

This action lets you retrieve the details of an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. Use when you need to read the body of a template programmatically — for example, to render it with dynamic data or pass it to another system. This action won't work for child orgs of the workflow's organization.

**Parameters**

* **Template ID**: The ID of the template you wish to retrieve.

**Output**

* The action returns the requested template's information:  `id`, `name`, `body`, `language`, `content_type`, `org_id`, `created_at`, `updated_at`.

</details>

<details>

<summary>Get Trigger action</summary>

This action retrieves a single workflow trigger by ID, name, or enabled status. Use it to inspect a trigger's current state before updating it, or to retrieve trigger metadata for reporting purposes.<br>

**Parameters**

* **Name:** The name of the trigger.
* **ID:** The ID of the trigger.
* **Enabled:** A boolean value that indicates whether the trigger is enabled or not.

**Output**

* The action returns information about the specified trigger:  `id`, `name`, `enabled`, `criteria`, `parameters`, `workflow_id`, `triggerType`, `organization`, `activatedForOrgs`.

</details>

<details>

<summary>Get User action</summary>

This action retrieves a single Rewst user by email address or user ID. Use it to verify a user exists in Rewst before inviting them, or to retrieve their ID for use in other actions.

**Parameters**

* **ID:** The ID of a user in Rewst.
* **Organization ID:** The ID of an organization in Rewst.
* **Email address:** The email of a user in Rewst.

**Output**

* The returned object includes the user's details like ID, role, organization ID, assigned role IDs, username, and a boolean indicating superuser status.

</details>

<details>

<summary>Invite User to Rewst action</summary>

Invite a user to join your organization in Rewst. Use it in client onboarding workflows to automatically provision Rewst access for new users. Set `send_email` to true if you want Rewst to handle the notification.

**Parameters**

* **Email:** Email address of the user to invite.
* **Roles:** Role IDs to assign to user.
* **Send Email?**: Whether to send the invitation email; default is false — useful if you're managing the invite flow yourself.

**Output**

* The returned object includes the invite details such as ID, email, organization ID, assigned role IDs, a boolean indicating acceptance status, and the ID of the inviter.

</details>

<details>

<summary>Link Microsoft CSP Customer action</summary>

This acton links one or more Rewst organizations to a Microsoft CSP customer in Microsoft. Use it in Microsoft CSP onboarding workflows after creating a Rewst org, to establish the CSP relationship that enables Microsoft-scoped actions to run against that tenant.

**Parameters**

* **CSP Integration Configuration ID**: The ID of a Microsoft CSP integration configuration in Rewst.
* **Microsoft CSP Customer ID**: The ID of the Microsoft CSP Customer in Rewst that you want to link your organization or organizations to.
* **Organization IDs** The list of Rewst organization IDs to link.

**Output**

None

</details>

<details>

<summary>List Apps action</summary>

Lists all apps, also known as sites, associated with the current organization in Rewst. Use it to enumerate available apps, typically as a precursor to the List Pages or List Page Elements actions.

**Parameters**

* **Run as user**, optional: The ID of the user to run the query as. If omitted, defaults to the workflow's context user.

**Output**

* The action returns a list of apps, including details such as ID, name, and organization association.

</details>

<details>

<summary>List Forms </summary>

This action returns all Rewst Forms for the current organization. Use it to enumerate forms for reporting, or to find a form's ID dynamically before passing it to Get Form or other actions.

**Parameters**

* **run\_as\_user**, required: The user ID that the action will run as. If not specified, the default user for your organization will be used.

**Outputs**

* The task returns an array of form objects, where each form contains:

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

<summary>List Forms With Granular Permissions</summary>

This action is the same as the List Forms action, but filters the results based on the permissions of the specified Run As User. This means it only returns forms the given user is actually allowed to see/use. Use it when building user-facing workflows where you need to show only the forms a specific user has access to, rather than all forms in the org.

**Parameters**

* **run\_as\_user**, required: The user whose permissions determine which forms are returned.

**Outputs**

* The task returns an array of form objects, where each form contains:

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

This action retrieves a comprehensive list of integrations installed for a specific organization in Rewst, providing a detailed overview of each integration's attributes. Use it to check which integrations are configured for a client org before running integration-dependent tasks, or to audit integration coverage across your client base.

**Parameters**

* **Organization ID:** The unique identifier for an organization in Rewst. This parameter is required to fetch the specific integration details pertinent to the organization.

**Output**

The action generates a detailed list of integrations, including:

* **Integration ID, Name, and Reference:** Basic identifiers providing clarity on each integration.
* **Pack Configurations:** In-depth details of configurations applied to each integration, offering insights into their setup and customization.
* **Applied Triggers:** Information on workflow triggers linked to each integration, useful for understanding operational dynamics.
* **Foreign Object References:** Crucial data points that link integrations to external references, enhancing cross-platform data synchronization and management.

</details>

<details>

<summary>List Microsoft CSP Customer action</summary>

This action returns all Microsoft CSP customers associated with your CSP integration. Use it to enumerate all CSP customers, typically to find unlinked customers and pair them with Rewst orgs during onboarding automation.<br>

**Parameters**

* **CSP Integration Configuration ID**: Your Microsoft CSP pack config ID.
* **Microsoft CSP Customer ID**: The ID of the Microsoft CSP Customer in Rewst that you want to link your organization or organizations to.
* **Organization IDs**: The list of Rewst organization IDs to link.

**Output**

* The action returns an array of CSP customer objects with `id`, `tenant_id`, `company_name`, `has_consent`, `csp_tenant_id`, `linked_organizations`.

</details>

<details>

<summary>List Organizations action</summary>

This action fetches a list of all organizations in Rewst. This is the standard way to enumerate all your client orgs. It's commonly used at the start of multi-tenant workflows that need to iterate over all managed organizations.

**Parameters**

* Managing **Organization ID:** Identifier of the managing organization to fetch organizations for. This ID is unique for each organization within Rewst.
* **Name**, optional: Name of the organization to search for. The name must be unique within Rewst.

**Output**

* The action returns a list of organizations, each with its corresponding Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>List Organization Variables action</summary>

This action lists all organization variables visible to the selected organization. Use it to audit what org variables are set for a client, or to check for the existence of a variable before creating it. Remember: for secret variable values at runtime, use `ORG.VARIABLES.variable_name` in Jinja instead.

**Parameters**

* **Organization ID**, optional: A dropdown list of the labels that correlate with the ID, visible in the code editor window, of an organization you'd like to retrieve.

**Output**

* The action returns a list of objects. Each object represents an organization variable and includes the ID, name, value, organization ID, category, timestamps, associated organization, and more.

</details>

<details>

<summary>List Templates action</summary>

This action retrieves a list of all existing templates. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization. Use it to find a template's ID dynamically, audit template content, or enumerate templates for reporting.

**Parameters**

* No parameters are required for this action.

**Output**

* The action returns a list of all templates, with each entry including information about a template, such as its `id`, `name`, `description`, `body`, `content_type`, and `language`.

</details>

<details>

<summary>List Triggers action</summary>

This action returns all workflow triggers for the current organization. Use it  to audit trigger configurations, find a trigger's ID before updating it, or check which workflows have active triggers.

**Parameters**

* No parameters are required for this action.

**Output**

* The action returns a list of all triggers, each item including information about a trigger:  `id`, `name`, `enabled`, `criteria`, `parameters`, `workflow_id`, `triggerType`, `organization`, `activatedForOrgs`.

</details>

<details>

<summary>List User Invites to Rewst action</summary>

This action returns all pending and/or accepted user invites for the current organization. Use it to check whether a user has already been invited before calling Invite User to Rewst, to avoid duplicate invites.

**Parameters**

* No parameters needed for this action.

**Output**

* The returned list includes a list of user invite objects. Each object contains the invite's ID, email, organization ID, assigned role IDs, a boolean indicating acceptance status, and the ID of the inviter.

</details>

<details>

<summary>List Users by Organization action</summary>

This action returns all users and optionally invitees for the current organization. Use it to audit who has access to a Rewst org, check for existing users before inviting, or build user-management automation.

**Parameters**

* **Include User Invites?:** Whether or not to include user invites in the results; default is true.
* **Which Invites to Include:** Which invitees to include. Can be **all**, **accepted**, or **pending**, with a default to all.

**Output**

* A list of users with details like ID, role, organization ID, assigned role IDs, username, and a boolean indicating superuser status.

</details>

<details>

<summary>List Workflows actions</summary>

This action returns all workflows for the current organization. Use it to enumerate workflows for auditing, find a workflow's ID dynamically, or build meta-automation that operates on workflows themselves.

**Parameters**

* **Run As User**

**Output**

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

{% hint style="info" %}
Note that this action won't return workflow notes. To retrieve that information, use the [Rewst - Generic GraphQL Request](rewst-actions.md#generic-graphql-request-action) action to query `workflowNotes` .
{% endhint %}

</details>

<details>

<summary>List Workflow Executions With Time Savings action</summary>

This action returns workflow execution data aggregated with time savings metrics, useful for ROI reporting. Use it in reporting workflows to generate ROI summaries for clients or internal dashboards. Feed the output into a Send Mail or PSA ticket update.

**Parameters**

* **Updated At**, required: Only include executions updated after this datetime.
* **Workflow Status**: Filter by `succeeded`, `failed`, or `running`.
* **Group by Sub Org**: If true, groups results by child org instead of by workflow; default is false.

**Output**

The action returns data including:

* `ran_for_org`: Organization identifier
* `workflow_id`: Unique workflow identifier
* `seconds_saved`: Calculated time savings in seconds
* `workflow_name`: Name of the workflow
* `total_executions`: Total number of executions

</details>

<details>

<summary>Unlink Microsoft CSP Customer action</summary>

This action removes the link between one or more Rewst organizations and a Microsoft CSP customer record. Use it in offboarding workflows when a client is leaving your CSP or being migrated to a different tenant relationship.<br>

**Parameters:**

* **CSP Integration Configuration ID**: Your Microsoft CSP pack config ID.
* **Microsoft CSP Customer ID**: The CSP customer to unlink from.
* **Organization IDs**: The list of Rewst organization IDs to unlink.

**Output**

None

</details>

<details>

<summary>Update Organization action</summary>

This action updates properties of an existing Rewst organization. Use it in onboarding/offboarding workflows to enable/disable orgs, or to update org metadata when client details change.

**Parameters**

* **Organization ID:** Identifier of the organization to be updated. This ID is unique for each organization within Rewst.
* **Name**: New name for the organization. This name must be unique within Rewst.
* **Domain**: New domain for the organization, excluding protocol.
* **Org Slug**: New slug.
* **Is Enabled**: Enable or disable user login for this org.
* **Tag IDs**: Replace the org's tags with this list.
* **Remove All Tags**: If true, strips all tags from the org; tag IDs are ignored when this is true.

**Output**

Outputs the updated details of the organization, which includes the Organization ID, Domain, Name, Managing Organization ID, and Enabled Status.

</details>

<details>

<summary>Update Template action</summary>

This action lets you update the details of an existing template. Template actions are used to manage templates that exist at the organization level of the workflow in which you are building. This action won't work for child orgs of the workflow's organization. Use it in workflows that dynamically maintain template content — for example, updating a weekly report template with new data before sending it.

**Parameters**

* **Template ID:** The ID of the template you wish to update, it is a required field.
* **Body:** The new content of the template.
* **Content Type:** The new type of content used in the template. The options are `message` and `script`.
* **Description:** A brief description of the template.
* **Language:** The new language used in the template. The options include: `html`, `markdown`, `powershell`, `python`, `yaml`.

**Output**

* The action returns the updated template's information, including its `id`.

</details>

<details>

<summary>Update Trigger action</summary>

The rewst\_update\_trigger task is used to modify existing workflow triggers within the Rewst platform. This action allows you to update properties of a trigger such as its name, enabled status, description, and the user it runs as. Useit  to programmatically enable or disable triggers as part of maintenance windows, scheduled automation pauses, or onboarding flows that need to activate triggers for new client orgs.

**Parameters**

* **Trigger\_id**: The ID of the trigger to be updated
* **Name**: New name for the trigger
* **Enabled**: Whether the trigger should be enabled or disabled
* **Description**: New description for the trigger
* **Run\_as\_user**: The user ID that the trigger will run as; defaults to organization default user if not specified

**Output**

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

This action lists all pages for a specified app in Rewst.

**Parameters**

* **App ID:** The ID of the app for which to fetch pages.
* **Run as user - optional:** The ID of the user to run the query as.

**Output**

* The action returns a list of pages within the specified app, including each page's ID, name, and metadata.

</details>

<details>

<summary>List Page Elements action</summary>

Lists all elements within a specific page in an app, including their Element IDs and key properties.

**Parameters**

* **Page ID:** The ID of the page whose elements you want to retrieve.
* **Run as user**, optional: The ID of the user to run the query as.

**Output**

* The action returns a dictionary mapping element IDs to their properties, including type, Craft ID, and other element-specific details.

</details>

<details>

<summary>Update Text Element Content action</summary>

Updates the text-based content of a page element— such as a text block, button, link, HTML container, markdown block, or accordion— within a specified page.

**Parameters**

* **Content:** The new text content to set for the element.
* **Page ID:** The ID of the page containing the element to update.
* **Element ID:** The ID of the page element whose text content you want to update.
* **Run as user**, optional: The ID of the user to run the query as.

**Output**

* The action returns the updated element's details, including confirmation of the new text content.

</details>
