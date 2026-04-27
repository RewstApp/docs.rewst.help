# Generic GraphQL request action

## What is GraphQL?

{% hint style="info" %}
Learn more about GraphQL in its official documentation [here](https://graphql.org/learn/introduction/).&#x20;
{% endhint %}

GraphQL is an open-source query language for APIs and a server-side runtime for fulfilling those queries. It enables clients to interact with a single endpoint to get the exact data they need, without chaining requests together. Unlike traditional REST APIs that return fixed datasets, GraphQL allows clients to request specific data, eliminating over-fetching or under-fetching of data and offering improved efficiency. The [GraphQL Schema](https://graphql.org/learn/schema/) defines the structure of the data and available operations, serving as a clear contract between the frontend and backend. Like REST APIs, GraphQL is composed of a basic request and response for each call. While REST APIs rely on multiple endpoints for this process, GraphQL shifts the responsibility of defining what should be called back to the user.

GraphQL in Rewst works off of two _operation types_:

1. Query: Used for reading or fetching data
2. Mutation: Used for writing, updating, or deleting data

{% hint style="info" %}
GraphQL has a third operation type called subscription. Rewst's generic GraphQL action currently only supports queries and mutations. If there is a subscription you are looking to use in Rewst, please submit a request to our product team for a dedicated action.
{% endhint %}

## What is the Rewst GraphQL generic request action?

{% hint style="warning" %}
Before using the Generic GraphQL request action, we recommend that you have:

* An understanding of GraphQL query structure and syntax
* Familiarity with Rewst's data model and the below available schema documentation
{% endhint %}

\
The Rewst GraphQL generic request action is used for making authenticated requests against Rewst's GraphQL API. This action is available in the Rewst actions section of the Workflow Builder's actions library, but is open-ended in its capabilities. It enables:

* Direct API access: Execute custom GraphQL queries and mutations against Rewst's backend
* Advanced data retrieval: Access data structures not available through standard actions
* Custom automation: Build sophisticated workflows with precise data control
* Administrative operations: Perform bulk operations and administrative tasks programmatically

<figure><img src="../../../.gitbook/assets/Screenshot 2026-04-22 at 10.53.52 AM.png" alt=""><figcaption></figcaption></figure>

Make your choices in the **Parameters** tab of the action's settings to set it up in your workflow:

* **Operation type**: Choose the type of GraphQL operation, **query** or **mutation**
* **Graph operation**: The name of the specific GraphQL operation to execute
  * Uses the Graph Operations reference
  * Options in the drop-down list will dynamically populate based on your selected operation type
* **Variable values**: Variables to pass to the GraphQL operation
  * JSON object type, but can be passed via Jinja
  * Contains the input parameters for the selected operation
* **Response fields**: Enter text into this field to specify the fields to include in the GraphQL response
  * Only provide the inner content, as it will be wrapped in curly braces
  * Example, `id orgName email { name }`&#x20;
* **Raw query**: The complete raw GraphQL query string to execute
  * An advanced alternative to using the other fields and selectors in the Parameters tab
  * Allows for full control over query structure

## Generic GraphQL request action usage examples

### Basic query example

```yaml
operation_type: "query"
operation: "organizations"
variable_values: 
  limit: 50
  order: [["name"]]
fields: "id, name, domain, isEnabled"
```

### Mutation example

```yaml
operation_type: "mutation"
operation: "createOrgVariable"
variable_values:
  orgVariable:
    name: "custom_setting"
    value: "production"
    orgId: "{{ CTX.organization.id }}"
    category: "general"
fields: "id, name, value, category"
```

### Raw query example

```yaml
raw_query: |
  query GetWorkflowDetails($workflowId: ID!) {
    workflow(where: {id: $workflowId}) {
      id
      name
      description
      tasks {
        id
        name
        action {
          name
          pack {
            name
          }
        }
      }
    }
  }
variable_values:
  workflowId: "{{ CTX.workflow_id }}"
```

## Generic GraphQL request action: Allowed operations&#x20;

{% hint style="info" %}
## Schema reference

Key entity types include:

* Organization: Core organizational data and settings
* Workflow: Automation workflow definitions and execution data
* Action: Available actions and their configurations
* Trigger: Event triggers and their configurations
* Form: Dynamic forms and field definitions
* Template: Reusable templates and scripts
* User: User accounts and permissions
* Pack: Integration packs and their components
{% endhint %}

### Operation type: Queries

#### **Action and configuration queries**

<details>

<summary><strong><code>actionOption</code> -</strong> Retrieves a specific action option configuration.</summary>

**GraphQL schema**

```graphql
actionOption(where: ActionOptionWhereInput): ActionOption

type ActionOption {
  actions: [Action!]
  id: ID
  optionLabel: String
  optionValue: String
  organizationId: ID
  organization: Organization
  packConfigId: ID
  resourceName: String
  packConfig: PackConfig
}
```

**Usage example:**

```yaml
operation_type: "query"
operation: "actionOption"
variable_values:
  where:
    packConfigId: "{{ CTX.pack_config_id }}"
    optionLabel: "environment"
fields: "id, optionLabel, optionValue, resourceName"
```

</details>

<details>

<summary><strong><code>actionOptions</code></strong>-Retrieves multiple action options with filtering and sorting.</summary>

**GraphQL schema:**

```graphql
actionOptions(
  where: ActionOptionWhereInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["optionLabel"]]
): [ActionOption!]!
```

**Usage example:**

```yaml
operation_type: "query"
operation: "actionOptions"
variable_values:
  where:
    organizationId: "{{ CTX.org_id }}"
  limit: 50
  order: [["optionLabel", "asc"]]
fields: "id, optionLabel, optionValue, organization { name }"
```

</details>

<details>

<summary><strong><code>localReferenceOptions</code></strong>-Gets dropdown options for local reference models.</summary>

**GraphQL schema:**

```graphql
localReferenceOptions(
  modelName: LocalReferenceModel!
  orgId: ID!
  filterArg: JSON
): [DropdownOption!]!

enum LocalReferenceModel {
  Crate
  CustomDatabase
  Organization
  PackConfig
  Role
  Template
  TemplateExport
  User
  Workflow
  Trigger
  Form
  Site
  Page
}

type DropdownOption {
  label: String
  value: String
}
```

**Usage example:**

```yaml
operation_type: "query"
operation: "localReferenceOptions"
variable_values:
  modelName: "Workflow"
  orgId: "{{ CTX.org_id }}"
  filterArg: {"enabled": true}
fields: "label, value"
```

</details>

<details>

<summary><strong><code>resourceTypesByPack</code></strong>-Gets resource types organized by pack.</summary>

**GraphQL schema:**

```graphql
resourceTypesByPack: [PackResourceTypesContainer!]!

type PackResourceTypesContainer {
  id: ID!
  packName: String!
  resourceTypes: [String!]!
}
```

</details>

#### **Action management queries**

<details>

<summary><strong><code>action</code></strong>-Retrieves a specific action definition.</summary>

**GraphQL schema:**

```graphql
action(where: ActionInput, search: ActionSearch): Action

type Action {
  actionOptions: [ActionOption!]!
  className: String
  defaultHumanSecondsSaved: Int
  deprecated: Boolean
  deprecationMessage: String
  description: String
  enabled: Boolean
  entryPoint: String
  category: String
  hidden: Boolean
  icon: String
  id: ID
  name: String
  organization: Organization
  orgId: ID
  outputSchema: JSON
  pack(where: PackInput): Pack
  packId: ID!
  parameters(populateOptions: Boolean = true): JSON
  ref: String
  runner: Runner
  uid: ID
  visibleForOrganizations: [Organization!]!
  workflow: Workflow
}
```

**Usage example:**

```yaml
operation_type: "query"
operation: "action"
variable_values:
  where:
    ref: "http_request"
    packId: "core"
fields: "id, name, description, parameters, outputSchema"
```

</details>

<details>

<summary><strong><code>actions</code></strong>-Retrieves multiple actions with filtering.</summary>

**GraphQL schema:**

```graphql
actions(
  where: ActionInput
  search: ActionSearch
  limit: Int = 100
  offset: Int
  order: [[String!]!] = [["name"]]
): [Action!]!
```

**`actionsForOrg`**-Gets actions available to a specific organization.

**GraphQL schema:**

```graphql
actionsForOrg(
  where: ActionInput
  search: ActionSearch
  limit: Int = 100
  offset: Int
  order: [[String!]!] = [["name"]]
  orgId: ID
): [Action!]!
```

</details>

#### **System and Debug Queries**

<details>

<summary><strong><code>announcement</code></strong>-Gets system announcements.</summary>



</details>

<details>

<summary><strong><code>debug-</code></strong>Debug endpoint for system information.</summary>

**GraphQL schema:**

```graphql
debug: Boolean
```

</details>

#### **Component management queries**

<details>

<summary><strong><code>component</code></strong>-Retrieves a specific component definition.</summary>

**GraphQL schema:**

```graphql
component(id: ID!): Component

type Component {
  id: ID!
  orgId: ID!
  name: String!
  description: String
  currentVersion: Int
  createdBy: User
  createdById: ID
  createdAt: String
  updatedAt: String
  versions: [ComponentVersion!]
  updatedBy: User
  updatedById: ID
}
```

</details>

<details>

<summary><strong><code>components</code></strong>-Gets multiple components for an organization.</summary>

**GraphQL schema:**

```graphql
components(orgId: ID!): [Component]
```

**`componentsByRoots`**-Gets components by their root IDs.

**GraphQL schema:**

```graphql
componentsByRoots(rootIds: [ID]!): [Component]
```

</details>

<details>

<summary><strong><code>componentTree</code></strong>-Gets the component tree structure.</summary>



**GraphQL schema:**

```graphql
componentTree(id: ID!): ComponentTree

type ComponentTree {
  encoded: String!
  component: Component!
  orgId: ID!
  versionNumber: Int
  createdAt: String
  updatedAt: String
  updatedBy: User
}
```

</details>

#### **Crate management queries**

<details>

<summary><strong><code>crateTokenTypes</code></strong>-Gets available crate token types.</summary>

**GraphQL schema:**

```graphql
crateTokenTypes: [String!]!
```

</details>

<details>

<summary><strong><code>crate</code></strong>-Retrieves a specific crate.</summary>

**GraphQL schema:**

```graphql
crate(
  where: CrateWhereInput
  search: CrateSearchInput
  selectedOrgId: ID
): Crate

type Crate {
  associatedPacks: [Pack!]
  category: String
  crateTriggers: [CrateTrigger!]
  createdAt: String
  description: String
  id: ID!
  isPublic: Boolean!
  isUnpackedForSelectedOrg: Boolean
  lastPublishedAt: String
  maturity: CrateMaturity
  name: String!
  orgId: ID!
  primaryPack: Pack
  primaryPackId: ID
  providedValue: String
  replicationRegions: [CrateReplicationRegion!]
  requiredOrgVariables: [String!]
  setupAssistance: Boolean
  setupTime: Int
  sourceEnvironment: String
  status: CrateStatus!
  tags: [Tag!]
  tagIds: [ID!]
  tokens: [CrateToken!]!
  triggers: [Trigger!]
  unpackingCount: Int
  unpackedWorkflowId: ID
  updatedAt: String
  workflow: Workflow
  workflowId: ID
  gid: ID
  updatedById: ID
  createdById: ID
}
```

</details>

<details>

<summary><strong><code>crates</code></strong>-Gets multiple crates with filtering and sorting.</summary>

**GraphQL schema:**

```graphql
crates(
  where: CrateWhereInput
  search: CrateSearchInput
  selectedOrgId: ID
  limit: Int
  offset: Int
  order: [[String!]!] = [["unpackingCount", "desc"], ["createdAt", "asc"]]
): [Crate!]!
```

</details>

<details>

<summary><strong><code>crateExportInfo</code></strong>-Gets export information for a workflow to crate.</summary>

**GraphQL schema:**

```graphql
crateExportInfo(workflowId: ID!): JSON
```

</details>

<details>

<summary><strong><code>crateUnpackingArgumentSet</code></strong>-Gets crate unpacking argument sets.</summary>

**GraphQL schema:**

```graphql
crateUnpackingArgumentSet(
  where: CrateUnpackingArgumentSetWhereInput
): CrateUnpackingArgumentSet

type CrateUnpackingArgumentSet {
  arguments: [CrateUnpackingArgument!]!
  crate: Crate!
  crateId: ID!
  crateTriggerUnpackings: [CrateTriggerUnpacking!]!
  createdAt: String!
  createdBy: User!
  createdById: ID!
  humanSecondsSaved: Int!
  id: ID!
  orgId: ID!
  updatedAt: String
  updatedBy: User
  updatedById: ID
  workflowName: String!
}
```

</details>

#### **Feature preview queries**

<details>

<summary><strong><code>featurePreviewSetting</code></strong>-Gets a specific feature preview setting.</summary>

**GraphQL schema:**

```graphql
featurePreviewSetting(where: FeaturePreviewSettingWhereInput): FeaturePreviewSetting

type FeaturePreviewSetting {
  description: String!
  id: ID!
  isStaffOnly: Boolean!
  label: String!
}
```

</details>

<details>

<summary><strong><code>featurePreviewSettings</code></strong>-Gets multiple feature preview settings.</summary>

**GraphQL schema:**

```graphql
featurePreviewSettings(
  where: FeaturePreviewSettingWhereInput,
  order: [[String!]!] = [["createdAt"]]
): [FeaturePreviewSetting]
```

</details>

#### **Foreign Object Reference Queries**

<details>

<summary><strong><code>foreignObjectReference</code></strong>-Gets a specific foreign object reference.</summary>

**GraphQL schema:**

```graphql
foreignObjectReference(
  where: ForeignObjectReferenceWhereInput
): ForeignObjectReference

type ForeignObjectReference {
  action: Action
  actionId: ID
  id: ID!
  identifier: ID
  organization: Organization!
  orgId: ID!
  packConfig: PackConfig
  packConfigId: ID
  referenceId: ID!
  workflowExecution: WorkflowExecution
  workflowExecutionId: ID
}
```

</details>

<details>

<summary><strong><code>foreignObjectReferences</code></strong>-Gets multiple foreign object references.</summary>

**GraphQL schema:**

```graphql
foreignObjectReferences(
  where: ForeignObjectReferenceWhereInput
): [ForeignObjectReference!]!
```

</details>

#### **Form management queries**

<details>

<summary><strong><code>form</code></strong>-Retrieves a specific form definition.</summary>

**GraphQL schema:**

```graphql
form(
  where: FormWhereInput
  search: FormSearchInput
  orgContextId: ID
): Form

type Form {
  clonedFrom: Form
  clonedFromId: ID
  cloneOverrides: JSON
  clones: [Form]
  createdBy: User
  createdById: ID
  createdAt: String
  description: String
  fields(orgContextId: ID): [FormField]
  id: ID!
  isSynchronized: Boolean
  name: String!
  organization: Organization!
  orgId: ID!
  tags: [Tag!]!
  triggers: [Trigger!]
  unpackedFrom: Crate
  unpackedFromId: ID
  updatedAt: String
  updatedBy: User
  updatedById: ID
  warrant: Warrant
}
```

</details>

<details>

<summary><strong><code>forms</code></strong>-Gets multiple forms with filtering.</summary>

**GraphQL schema:**

```graphql
forms(
  where: FormWhereInput
  search: FormSearchInput
  limit: Int
  offset: Int
  hasTagIds: [ID]
  order: [[String!]!] = [["name"]]
): [Form!]!
```

</details>

<details>

<summary><strong><code>packConfigsForForm</code></strong>-Gets pack configurations associated with a form.</summary>

**GraphQL schema:**

```graphql
packConfigsForForm(formId: ID!, orgId: ID!, triggerId: ID): [PackConfig!]!
```

</details>

<details>

<summary><strong><code>evaluatedForm</code></strong>-Gets an evaluated form for a specific trigger.</summary>

**GraphQL schema:**

```graphql
evaluatedForm(
  where: EvaluatedFormWhereInput
  orgContextId: ID
): Form
```

</details>

#### **Microsoft CSP Queries**

<details>

<summary><strong><code>microsoftCSPCustomer</code></strong>-Gets Microsoft CSP customer information.</summary>

**GraphQL schema:**

```graphql
microsoftCSPCustomer(
  cspPackConfigId: ID!
  where: MicrosoftCSPCustomerWhereInput
): MicrosoftCSPCustomer

type MicrosoftCSPCustomer {
  createdAt: String!
  companyName: String!
  cspTenantId: String!
  hasConsent: Boolean!
  id: ID!
  linkedOrganizations: [Organization!]
  tenantId: String!
  updatedAt: String!
}
```

</details>

<details>

<summary><strong><code>microsoftCSPCustomers</code></strong>-Gets multiple Microsoft CSP customers.</summary>

**GraphQL schema:**

```graphql
microsoftCSPCustomers(
  cspPackConfigId: ID!
  search: MicrosoftCSPCustomerSearchInput,
  where: MicrosoftCSPCustomerWhereInput
): [MicrosoftCSPCustomer!]!
```

</details>

#### **Trigger instance queries**

<details>

<summary><strong><code>orgTriggerInstance</code></strong>-Gets a specific organization trigger instance.</summary>

**GraphQL schema:**

```graphql
orgTriggerInstance(
  where: OrgTriggerInstanceWhereInput
  search: OrgTriggerInstanceSearchInput
): OrgTriggerInstance

type OrgTriggerInstance {
  id: ID!
  isManualActivation: Boolean
  organization: Organization
  orgId: ID
  lastSearchedAt: String
  trigger: Trigger
  triggerId: ID
  state: JSON
  createdAt: String!
  updatedAt: String!
}
```

</details>

<details>

<summary><strong><code>orgTriggerInstances</code></strong>-Gets multiple organization trigger instances.</summary>

**GraphQL schema:**

```graphql
orgTriggerInstances(
  where: OrgTriggerInstanceWhereInput
  search: OrgTriggerInstanceSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["createdAt"]]
): [OrgTriggerInstance!]!
```

</details>

#### **Organization variable queries**

<details>

<summary><strong><code>orgVariable</code></strong>-Gets a specific organization variable.</summary>

**GraphQL schema:**

```graphql
orgVariable(
  where: OrgVariableWhereInput
  search: OrgVariableSearchInput
  maskSecrets: Boolean
): OrgVariable

type OrgVariable {
  cascade: Boolean!
  category: OrgVariableCategory!
  createdAt: String!
  id: ID!
  name: String!
  organization: Organization!
  orgId: ID!
  packConfig: PackConfig
  packConfigId: ID
  updatedAt: String
  value: String
}

enum OrgVariableCategory {
  contact
  general
  secret
  system
}
```

</details>

<details>

<summary><strong><code>orgVariables</code></strong>-Gets multiple organization variables.</summary>

**GraphQL schema:**

```graphql
orgVariables(
  where: OrgVariableWhereInput
  search: OrgVariableSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
  maskSecrets: Boolean
): [OrgVariable!]!
```

</details>

<details>

<summary><strong><code>visibleOrgVariables</code></strong>-Gets organization variables visible to a specific organization.</summary>

**GraphQL schema:**

```graphql
visibleOrgVariables(
  search: OrgVariableSearchInput
  visibleForOrgId: ID!
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [OrgVariable!]!
```

</details>

#### **Organization management queries**

<details>

<summary><strong><code>organization</code></strong>-Gets a specific organization.</summary>

**GraphQL schema:**

```graphql
organization(
  where: OrganizationWhereInput
  search: OrganizationSearchInput
): Organization

type Organization {
  actions: [Action!]!
  activatedTriggers: [Trigger!]!
  createdAt: String
  createdTags: [Tag!]!
  domain: String
  deletedAt: String
  forms: [Form!]!
  id: ID
  isMsp: Boolean
  isStaff: Boolean
  isEnabled: Boolean
  isDeleted: Boolean
  isInternal: Boolean
  installedPacks: [Pack!]!
  featurePreviewSettings: [OrganizationFeaturePreviewSetting]
  managedOrgAutoInstallingWorkflows: [Workflow!]!
  managedAndSubOrgs: [Organization!]!
  managedOrgs: [Organization!]!
  managingOrg: Organization
  managingOrgId: ID
  name: String!
  orgSlug: String
  packConfigs: [PackConfig!]!
  resultsRetentionDays: Int
  rocSiteId: String
  tags: [Tag!]!
  templates: [Template!]!
  tid: ID
  triggerInstances: [OrgTriggerInstance!]!
  triggers: [Trigger!]!
  users: [User!]!
  variables: [OrgVariable!]!
  visibleActions: [Action!]!
  visiblePackConfigs: [PackConfig!]!
  visibleWorkflows: [Workflow!]!
  workflowExecutions: [WorkflowExecution!]!
  workflows: [Workflow!]!
  supportAccessStatus: SupportAccessStatus
}
```

</details>

<details>

<summary><strong><code>organizations</code></strong>-Gets multiple organizations.</summary>

**GraphQL schema:**

```graphql
organizations(
  where: OrganizationWhereInput
  search: OrganizationSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [Organization!]!
```

</details>

<details>

<summary><strong><code>orgSearch</code></strong>-Performs organization search with breadcrumbs.</summary>

**GraphQL schema:**

```graphql
orgSearch(
  search: String
  rootOrgId: ID!
  breadcrumbRootOrgId: ID!
): [OrgSearchResult!]!

type OrgSearchResult {
  id: ID!
  name: String!
  hasChildren: Boolean!
  breadcrumbs: [OrgBreadcrumb]
  managingOrgId: ID
  supportAccessStatus: SupportAccessStatus
  isInternal: Boolean
  }
```

</details>

<details>

<summary><strong><code>softDeletedOrgs</code></strong>-Gets soft-deleted organizations.</summary>

**GraphQL schema:**

```graphql
softDeletedOrgs(managingOrgId: ID!): [Organization!]!
```

</details>

#### **Pack action option queries**

<details>

<summary><strong><code>packActionOption</code></strong>-Gets a specific pack action option.</summary>

**GraphQL schema:**

```graphql
packActionOption(where: PackActionOptionWhereInput): PackActionOption

type PackActionOption {
  id: ID!
  name: String!
  packId: ID!
  path: String!
  method: HTTPMethod
  paginate: Boolean
  queryParams: JSON
  pathParams: JSON
  headers: JSON
  requiredPathVars: [String!]
  requiredQueryVars: [String!]
  requiredHeaderVars: [String!]
  resultsKey: String
  valueField: String!
  label: String!
  labelIsTemplate: Boolean
  valueFieldIsPath: Boolean
  maxPages: Int
  pageSize: Int
}
```

</details>

<details>

<summary><strong><code>packActionOptions</code></strong>-Gets multiple pack action options.</summary>

**GraphQL schema:**

```graphql
packActionOptions(
  where: PackActionOptionWhereInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["label"]]
): [PackActionOption!]!
```

</details>

#### **Pack bundle queries**

<details>

<summary><strong><code>packBundle</code></strong>-Gets a specific pack bundle.</summary>

**GraphQL schema:**

```graphql
packBundle(where: PackBundleWhereInput!): PackBundle

type PackBundle {
  configSchema: JSON
  description: String
  id: ID!
  name: String!
  packs: [Pack!]!
  ref: String!
}
```

</details>

<details>

<summary><strong><code>packBundles</code></strong>-Gets multiple pack bundles.</summary>

**GraphQL schema:**

```graphql
packBundles(
  where: PackBundleWhereInput
  search: PackBundleSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [PackBundle]!
```

</details>

#### **Pack configuration queries**

<details>

<summary><strong><code>packConfig</code></strong>-Gets a specific pack configuration.</summary>

**GraphQL schema:**

```graphql
packConfig(
  where: PackConfigWhereInput
  search: PackConfigSearch
  includeSpec: Boolean
): PackConfig

type PackConfig {
  appliedToTriggers: [Trigger!]!
  config: JSON
  default: Boolean
  description: String
  id: ID
  metadata: JSON
  name: String!
  organization: Organization
  foreignObjectReferences: [ForeignObjectReference!]!
  orgId: ID
  orgVariables: [OrgVariable!]!
  pack: Pack
  packId: ID
  actionOptions: [ActionOption!]!
  updatedAt: String
  createdAt: String
  visibleForOrganizations: [Organization!]!
}
```

</details>

<details>

<summary><strong><code>packConfigs</code></strong>-Gets multiple pack configurations.</summary>

**GraphQL schema:**

```graphql
packConfigs(
  where: PackConfigWhereInput
  search: PackConfigSearch
  resourceNames: String
  order: [[String!]!]
  includeSpec: Boolean
): [PackConfig!]!
```

</details>

<details>

<summary><strong><code>packConfigsForOrg</code></strong>-Gets pack configurations for a specific organization.</summary>

**GraphQL schema:**

```graphql
packConfigsForOrg(
  packIds: [ID!]!
  orgId: ID!
  includeSpec: Boolean
): [PackConfig!]!
```

</details>

#### **Pack management queries**

<details>

<summary><strong><code>pack</code></strong>-Gets a specific integration pack.</summary>

**GraphQL schema:**

```graphql
pack(where: PackWhereInput): Pack

type Pack {
  actions: [Action!]!
  configFormSchema: JSON
  configSchema: JSON
  metadata: JSON
  description: String
  id: String
  orgId: ID
  installedBy: [Organization]
  isDefault: Boolean
  isOauthConfiguration: Boolean
  isMultitenancyEnabled: Boolean
  name: String
  orgVariables: JSON
  packBundle: PackBundle
  packBundleId: ID
  packConfigs: [PackConfig!]!
  packOverrides: [PackOverride]
  packTestAction: Action
  packType: PackType
  ref: String
  icon: String
  sensorTypes: [SensorType!]!
  setupInstructions: String
  status: PackStatus!
  tags: [Tag!]!
  triggerTypes: [TriggerType!]!
  uid: String
  version: String
}
```

</details>

<details>

<summary><strong><code>packsAndBundlesByInstalledState</code></strong>-Gets packs and bundles organized by installation state.</summary>

**GraphQL schema:**

```graphql
packsAndBundlesByInstalledState(
  orgId: ID!
  includeCustomPack: Boolean
): PacksAndBundlesByInstalledState!

type PacksAndBundlesByInstalledState {
  installedPacksAndBundles: [PackOrPackBundle!]
  marketplacePacksAndBundles: [PackOrPackBundle!]
}
```

</details>

#### **Page management queries**

<details>

<summary><strong><code>page</code></strong>-Gets a specific page definition.</summary>

**GraphQL schema:**

```graphql
page(where: PageWhereInput!): Page

type Page {
  createdBy: User
  createdById: ID
  createdAt: String
  id: ID!
  loader: Loader
  name: String!
  path: String!
  site: Site
  siteId: ID
  updatedAt: String
  updatedBy: User
  updatedById: ID
  workflows: [Workflow!]!
  nodes: [PageNode]
  permission: Permission
  orgId: ID
  variables: [JSON]
  organization: Organization
  isSynchronized: Boolean
  clonedFromId: ID
  clonedFrom: Site
  cloneOverrides: JSON
  clones: [Page]
  title: String
}
```

</details>

<details>

<summary><strong><code>pageVars</code></strong>-Gets page variables.</summary>

**GraphQL schema:**

```graphql
pageVars(id: ID!, query: JSON): JSON
```

</details>

<details>

<summary><strong><code>pages</code></strong>-Gets multiple pages.</summary>

**GraphQL schema:**

```graphql
pages(
  where: PageWhereInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
  search: PageSearchInput
): [Page!]!
```

</details>

#### **Permission queries**

<details>

<summary><strong><code>permission</code></strong>-Gets a specific permission.</summary>

**GraphQL schema:**

```graphql
permission(where: PermissionWhereInput): Permission

type Permission {
  id: ID
  templateId: ID
  authorizedForOrganizations: [Organization]
  authorizedForSubOrganizations: [Organization]
  excludeOrganizations: [Organization]
  roleIds: [String]
  override: String
  objectType: String
  objectId: String
  orgId: ID
  relation: String
  permissionType: String
  subjectType: String
  subjectId: String
}
```

</details>

<details>

<summary><strong><code>permissions</code></strong>-Gets multiple permissions.</summary>

**GraphQL schema:**

```graphql
permissions(where: PermissionWhereInput): [Permission!]!
```

</details>

#### **Sensor type queries**

<details>

<summary><strong><code>sensorType</code></strong>-Gets a specific sensor type.</summary>

**GraphQL schema:**

```graphql
sensorType(
  where: SensorTypeInput
  search: SensorTypeSearchInput
): SensorType

type SensorType {
  description: String
  enabled: Boolean
  entryPoint: String
  id: ID
  name: String
  notifyOnTriggerChanges: Boolean
  pack: Pack
  ref: String
  triggerTypes: [TriggerType!]!
}
```

</details>

<details>

<summary><strong><code>sensorTypes</code></strong>-Gets multiple sensor types.</summary>

**GraphQL schema:**

```graphql
sensorTypes(
  where: SensorTypeInput
  search: SensorTypeSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [SensorType!]!
```

</details>

#### **Site and app management queries**

<details>

<summary><strong><code>site</code></strong>-Gets a specific site/app.</summary>

**GraphQL schema:**

```graphql
site(where: SiteWhereInput, search: SiteSearchInput): Site

type Site {
  createdBy: User
  createdById: ID
  createdAt: String
  domain: String
  id: ID!
  isLive: Boolean
  statusCode: Int
  statusMessage: String
  name: String!
  organization: Organization
  orgId: ID!
  shared: Boolean
  updatedAt: String
  updatedBy: User
  updatedById: ID
  template: String
  theme: JSON
  themeReferenceOrgVariable: String
  pages: [Page]
  permission: Permission
  customDomain: String
  isDnsValidated: Boolean
  useCustomDomain: Boolean
  isSynchronized: Boolean
  clonedFromId: ID
  clonedFrom: Site
  cloneOverrides: JSON
  clones: [Site]
  faviconUrl: String
}
```

</details>

<details>

<summary><strong><code>sites</code></strong>-Gets multiple sites/apps.</summary>

**GraphQL schema:**

```graphql
sites(where: SiteWhereInput, search: SiteSearchInput): [Site!]!
```

</details>

<details>

<summary><strong><code>getAppPermissions</code></strong>-Gets app permissions for an organization.</summary>

**GraphQL schema:**

```graphql
getAppPermissions(orgId: ID!): [Site!]!
```

</details>

<details>

<summary><strong><code>getSiteTheme</code></strong>-Gets site theme configuration.</summary>

**GraphQL schema:**

```graphql
getSiteTheme(id: ID, domain: String): JSON
```

</details>

#### **Tag management queries**

<details>

<summary><strong><code>tag</code></strong>-Gets a specific tag.</summary>

**GraphQL schema:**

```graphql
tag(where: TagWhereInput, search: TagSearchInput): Tag

type Tag {
  crates: [Crate!]
  createdAt: String
  description: String
  id: ID
  name: String
  organization: Organization
  organizations: [Organization!]!
  orgId: ID
  packs: [Pack!]!
  triggers: [Trigger!]!
  updatedAt: String
  color: String
}
```

</details>

<details>

<summary><strong><code>tags</code></strong>-Gets multiple tags.</summary>

**GraphQL schema:**

```graphql
tags(
  where: TagWhereInput
  search: TagSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
  includeTagsWithNoOwner: Boolean = false
): [Tag!]!
```

</details>

<details>

<summary><strong><code>crateTags</code></strong>-Gets tags associated with crates.</summary>

**GraphQL schema:**

```graphql
crateTags(
  where: TagWhereInput
  search: TagSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [Tag!]!
```

</details>

#### **Task and execution analytics queries**

<details>

<summary><strong><code>dailyTaskCountsByDateRange</code></strong>-Gets daily task counts within a date range.</summary>

**GraphQL schema:**

```graphql
dailyTaskCountsByDateRange(
  orgId: ID!
  startDate: String!
  endDate: String!
): [TaskCountByDate!]!

type TaskCountByDate {
  date: String!
  count: Int!
}
```

</details>

<details>

<summary><strong><code>taskExecutionStats</code></strong>-Gets task execution statistics.</summary>

**GraphQL schema:**

```graphql
taskExecutionStats(orgId: ID!, createdSince: String): Int!
```

</details>

<details>

<summary><strong><code>taskLog</code></strong>-Gets a specific task log entry.</summary>

**GraphQL schema:**

```graphql
taskLog(
  where: TaskLogWhereInput
  search: TaskLogSearchInput
): TaskLog

type TaskLog {
  createdAt: String
  executionId: String
  executionTime: String
  id: ID
  input: JSON
  message: String
  originalParentTaskId: String
  originalPrincipalOrgId: ID
  originalPrincipalOrgName: String
  originalRunAsOrgId: String
  originalRunAsOrgName: String
  originalWorkflowExecutionId: String
  originalWorkflowTaskId: String
  originalWorkflowTaskName: String
  parentTask: WorkflowTask
  parentTaskId: ID
  result: JSON
  runAsOrg: Organization
  runAsOrgId: ID
  principalOrg: Organization
  principalOrgId: ID
  status: String
  taskExecutionId: ID
  updatedAt: String
  workflow: Workflow
  workflowExecution: WorkflowExecution
  workflowExecutionId: String
  workflowTask: WorkflowTask
  workflowTaskId: ID
}
```

</details>

<details>

<summary><strong><code>taskLogs</code></strong>-Gets multiple task log entries.</summary>

**GraphQL schema:**

```graphql
taskLogs(
  where: TaskLogWhereInput
  search: TaskLogSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["createdAt"]]
  ): [TaskLog!]!
```

</details>

#### **Template management queries**

<details>

<summary><strong><code>template</code></strong>- Gets a specific template.</summary>

**GraphQL schema:**

```graphql
template(where: TemplateInput): Template

type Template {
  body: String!
  clonedFrom: Template
  clonedFromId: ID
  cloneOverrides: JSON
  clones: [Template]
  contentType: String!
  context: JSON
  createdAt: String!
  description: String
  id: ID!
  isShared: Boolean
  isSynchronized: Boolean
  language: String!
  name: String!
  organization: Organization!
  orgId: ID!
  permission: Permission
  tags: [Tag!]!
  unpackedFrom: Crate
  unpackedFromId: ID
  updatedAt: String!
  updatedBy: User
  updatedById: ID
}
```

</details>

<details>

<summary><strong><code>templates</code></strong>-Gets multiple templates.</summary>

**GraphQL schema:**

```graphql
templates(
  where: TemplateInput
  search: TemplateSearch
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [Template!]!
```

</details>

<details>

<summary><strong><code>jinjaTemplate</code></strong>-Gets a Jinja template for rendering.</summary>

**GraphQL schema:**

```graphql
jinjaTemplate(where: TemplateInput): Template
```

</details>

#### **Trigger type queries**

<details>

<summary><strong><code>triggerType</code></strong>-Gets a specific trigger type.</summary>

**GraphQL schema:**

```graphql
triggerType(where: TriggerTypeWhereInput): TriggerType

type TriggerType {
  description: String
  id: ID
  name: String
  pack: Pack
  parametersSchema(filterArg: JSON, orgId: ID): JSON
  outputSchema: JSON
  ref: String
  isPoll: Boolean
  isWebhook: Boolean
  sensorType: SensorType
  triggers: [Trigger!]!
  webhookUrlTemplate: String
  canRunForManagedOrgs: Boolean
  enabled: Boolean
}
```

</details>

<details>

<summary><strong><code>triggerTypes</code></strong>-Gets multiple trigger types.</summary>

**GraphQL schema:**

```graphql
triggerTypes(
  where: TriggerTypeWhereInput
  search: TriggerTypesSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [TriggerType!]!
```

</details>

#### **Trigger management queries**

<details>

<summary><strong><code>trigger</code></strong>-Gets a specific trigger.</summary>

**GraphQL schema:**

```graphql
trigger(
  where: TriggerWhereInput
  search: TriggerSearchInput
): Trigger

type Trigger {
  activatedForOrgs: [Organization!]!
  autoActivateManagedOrgs: Boolean!
  clonedFrom: Trigger
  clonedFromId: ID
  cloneOverrides: JSON
  clones: [Trigger]!
  criteria: JSON
  description: String
  enabled: Boolean
  id: ID!
  isSynchronized: Boolean
  name: String
  organization: Organization!
  orgId: ID
  orgInstances: [OrgTriggerInstance]
  packOverrides: [PackOverride!]
  parameters: JSON
  state: JSON
  tags: [Tag!]!
  triggerType: TriggerType
  triggerTypeId: ID!
  unpackedFrom: Crate
  unpackedFromId: ID
  vars: [JSON]
  workflowId: ID!
  form: Form
  formId: ID
  workflow: Workflow!
}
```

</details>

<details>

<summary><strong><code>workflowCompletionListeners</code></strong>-Gets workflow completion listeners.</summary>

**GraphQL schema:**

```graphql
workflowCompletionListeners(
  where: TriggerWhereInput
  search: TriggerSearchInput
): [Trigger!]!
```

</details>

<details>

<summary><strong><code>triggers</code></strong>-Gets multiple triggers.</summary>

**GraphQL schema:**

```graphql
triggers(
  includeUnlisted: Boolean
  where: TriggerWhereInput
  search: TriggerSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [Trigger!]!
```

</details>

<details>

<summary><strong><code>triggerDbNotificationErrors</code></strong>-Gets database notification errors for a trigger.</summary>

**GraphQL schema:**

```graphql
triggerDbNotificationErrors(triggerId: ID!): [DatabaseNotificationError!]!

type DatabaseNotificationError {
  detail: String!
  raised_at: String!
  type: String!
}
```

</details>

#### **User invite queries**

<details>

<summary><strong><code>userInvite</code></strong>-Gets a specific user invite.</summary>

**GraphQL schema:**

```graphql
userInvite(
  where: UserInviteWhereInput
  search: UserInviteSearchInput
): UserInvite

type UserInvite {
  acceptedAt: String
  createdAt: String
  createdBy: User
  createdById: ID
  email: String!
  id: ID!
  isAccepted: Boolean
  organization: Organization!
  orgId: ID!
  roleIds: [String]
  roles: [JSON]
  sendEmail: Boolean
}
```

</details>

<details>

<summary><strong><code>userInvites</code></strong>-Gets multiple user invites.</summary>

**GraphQL schema:**

```graphql
userInvites(
  where: UserInviteWhereInput
  search: UserInviteSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["email"]]
): [UserInvite]
```

</details>

#### **User management queries**

<details>

<summary><strong><code>me</code></strong>-Gets current user information.</summary>

**GraphQL schema:**

```graphql
me: User

type User {
  createdAt: String
  favoriteActions: [UserFavoriteAction!]!
  id: ID
  isApiUser: Boolean
  isSuperuser: Boolean
  isTestUser: Boolean
  managedOrgs: [Organization!]!
  orgId: ID
  organization: Organization
  preferences: UserPreferences!
  roleIds: [String!]!
  roles: [JSON]
  sub: String
  username: String
  parentUserId: ID
  parentUsername: String
}
```

</details>

<details>

<summary><strong><code>userOrganization</code></strong>-Gets the user's organization.</summary>

**GraphQL schema:**

```graphql
userOrganization: Organization
```

</details>

<details>

<summary><strong><code>user</code></strong>-Gets a specific user.</summary>

**GraphQL schema:**

```graphql
user(where: UserWhereInput, search: UserSearchInput): User
```

</details>

<details>

<summary><strong><code>users</code></strong>-Gets multiple users.</summary>

**GraphQL schema:**

```graphql
users(
  where: UserWhereInput
  search: UserSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["username"]]
): [User!]!
```

</details>

<details>

<summary><strong><code>getTestUsers</code></strong>-Gets test users.</summary>

**GraphQL schema:**

```graphql
getTestUsers(where: UserWhereInput): [User!]!
```

</details>

<details>

<summary><strong><code>getTestUserSession</code></strong>-Gets current test user session.</summary>

**GraphQL schema:**

```graphql
getTestUserSession: User
```

</details>

#### **Workflow analytics queries**

<details>

<summary><strong><code>timeSavedGroupByWorkflow</code></strong>-Gets time saved statistics grouped by workflow.</summary>

**GraphQL schema:**

```graphql
timeSavedGroupByWorkflow(
  orgId: ID!
  workflowStatus: String
  updatedAt: String!
  useStatsTable: Boolean! = true
): [TimeSavedGroupByWorkflow!]!

type TimeSavedGroupByWorkflow {
  workflowId: ID!
  workflowName: String
  secondsSaved: Int
  totalExecutions: Int
  successfulExecutions: Int
  failedExecutions: Int
}
```

</details>

<details>

<summary><strong><code>timeSavedGroupBySubOrg</code></strong>-Gets time saved statistics grouped by sub-organization.</summary>

**GraphQL schema:**

```graphql
timeSavedGroupBySubOrg(
  orgId: ID!
  workflowStatus: String
  updatedAt: String!
  useStatsTable: Boolean! = true
): [TimeSavedGroupByOrg!]!

type TimeSavedGroupByOrg {
  workflowId: ID!
  workflowName: String
  secondsSaved: Int
  totalExecutions: Int
  ranForOrg: String
  }
```

</details>

<details>

<summary><strong><code>workflowExecutionStats</code></strong>-Gets workflow execution statistics.</summary>

**GraphQL schema:**

```graphql
workflowExecutionStats(
  orgId: ID!
  createdSince: String!
  rollUpTimeSaved: Boolean
  includeSubWorkflows: Boolean
): WorkflowExecutionStats

type WorkflowExecutionStats {
  delayed: Int!
  failed: Int!
  humanSecondsSaved: Int!
  paused: Int!
  pending: Int!
  running: Int!
  succeeded: Int!
}
```

</details>

<details>

<summary><strong><code>workflowExecution</code></strong>-Gets a specific workflow execution.</summary>

**GraphQL schema:**

```graphql
workflowExecution(
  where: WorkflowExecutionWhereInput
  search: WorkflowExecutionSearchInput
): WorkflowExecution

type WorkflowExecution {
  childExecutions: [WorkflowExecution!]!
  completionHandledExecution: WorkflowExecution
  completionHandlerExecutions: [WorkflowExecution!]!
  conductor: WorkflowExecutionConductor
  createdAt: String
  id: ID
  numAwaitingResponseTasks: Int
  numSuccessfulTasks: Int
  organization: Organization!
  orgId: ID!
  originatingExecutionId: ID
  parentExecution: WorkflowExecution
  parentExecutionId: ID
  parentTaskExecutionId: ID
  pendingTasks: [PendingTask]
  processedCompletionAt: String
  status: String
  subExecutions: [WorkflowExecution!]!
  taskLogs: [TaskLog!]!
  updatedAt: String
  workflow: Workflow!
}
```

</details>

<details>

<summary><strong><code>workflowExecutions</code></strong>-Gets multiple workflow executions.</summary>

**GraphQL schema:**

```graphql
workflowExecutions(
  where: WorkflowExecutionWhereInput
  search: WorkflowExecutionSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["createdAt"]]
  includeSubOrgs: Boolean
): [WorkflowExecution]
```

</details>

<details>

<summary><strong><code>workflowExecutionContexts</code></strong>-Gets workflow execution contexts.</summary>

**GraphQL schema:**

```graphql
workflowExecutionContexts(workflowExecutionId: ID!): JSON
```

</details>

<details>

<summary><strong><code>dailyTimeSavedByDateRange</code></strong>-Gets daily time saved within a date range.</summary>

**GraphQL schema:**

```graphql
dailyTimeSavedByDateRange(
  orgId: ID!
  startDate: String!
  endDate: String!
): [TimeSavedByDate!]!

type TimeSavedByDate {
  date: String!
  seconds: Int!
}
```

</details>

#### **Workflow patch queries**

<details>

<summary><strong><code>workflowPatch</code></strong>-Gets a specific workflow patch.</summary>

**GraphQL schema:**

```graphql
workflowPatch(id: ID!): WorkflowPatch!

type WorkflowPatch {
  id: ID!
  patchType: PatchType!
  patch: JSON!
  comment: String!
  commentDescription: String
  user: User
  workflowId: ID!
  foreignId: ID
  createdAt: String!
  updatedAt: String!
}
```

</details>

<details>

<summary><strong><code>workflowPatches</code></strong>-Gets multiple workflow patches.</summary>

**GraphQL schema:**

```graphql
workflowPatches(
  where: WorkflowPatchWhereInput
  orderBy: WorkflowPatchOrderByInput = createdAt_DESC
  limit: Int
  offset: Int
  createdSince: String
): [WorkflowPatch!]!
```

</details>

#### **Workflow management queries**

<details>

<summary><strong><code>workflow</code></strong>-Gets a specific workflow.</summary>

**GraphQL schema:**

```graphql
workflow(
  where: WorkflowWhereInput
  search: WorkflowSearch
): Workflow

type Workflow {
  autoInstallingForManagedOrgs: [Organization!]!
  action: Action
  clonedFrom: Workflow
  clonedFromId: ID
  cloneOverrides: JSON
  clones: [Workflow]!
  crates: [Crate!]
  completionListeners: [Trigger!]!
  createdAt: String
  createdBy: User
  createdById: ID
  description: String
  humanSecondsSaved: Int!
  id: ID
  input: [String!]!
  inputSchema: JSON
  isSynchronized: Boolean
  name: String
  notes: [WorkflowNote!]
  organization: Organization!
  orgId: ID!
  output: [JSON]!
  outputSchema: JSON
  packsUsed: [Pack!]!
  parentWorkflows: [WorkflowTask]
  permission: Permission
  schemaVersion: String
  tags: [Tag!]!
  tasks: [WorkflowTask!]!
  tasksObject: JSON
  taskActions: [Action!]!
  timeout: Int
  tokens: [JSON!]
  triggers: [Trigger]
  type: WorkflowType!
  unpackedFrom: Crate
  unpackedFromId: ID
  updatedAt: String
  updatedBy: User
  updatedById: ID
  varsSchema: JSON
  version: String
  visibleForOrganizations: [Organization!]!
}
```

</details>

<details>

<summary><strong><code>workflows</code></strong>-Gets multiple workflows.</summary>

**GraphQL schema:**

```graphql
workflows(
  where: WorkflowWhereInput
  search: WorkflowSearch
  hasListeners: Boolean
  hasParentWorkflows: Boolean
  hasTriggers: Boolean
  hasTriggerOfType: TriggerOfType
  hasTokens: Boolean
  isOptionsGenerator: Boolean
  isClone: Boolean
  isSyncClone: Boolean
  hasClones: Boolean
  isCrate: Boolean
  isCrateSource: Boolean
  hasTagIds: [ID!]
  excludeTagIds: [ID!]
  requireMatchingTasks: Boolean
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [Workflow!]!
```

</details>

<details>

<summary><strong><code>workflowNote</code></strong>-Gets a specific workflow note.</summary>

**GraphQL schema:**

```graphql
workflowNote(where: WorkflowNoteWhereInput): WorkflowNote

type WorkflowNote {
  id: ID
  title: String
  clonedFrom: WorkflowNote
  clonedFromId: ID
  createdAt: String
  content: String
  metadata: JSON
  index: Int!
  updatedAt: String
  workflow: Workflow
  workflowId: ID
}
```

</details>

<details>

<summary><strong><code>workflowNotes</code></strong>-Gets multiple workflow notes.</summary>

**GraphQL schema:**

```graphql
workflowNotes(
  where: WorkflowNoteWhereInput
  search: WorkflowNoteSearchInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["index"]]
  ): [WorkflowNote!]!
```

</details>

<details>

<summary><strong><code>workflowTask</code></strong>-Gets a specific workflow task.</summary>

**GraphQL schema:**

```graphql
workflowTask(where: WorkflowTaskWhereInput): WorkflowTask

type WorkflowTask {
  action: Action
  actionId: ID
  description: String
  humanSecondsSaved: Int
  id: ID
  input: JSON
  isMocked: Boolean
  join: Int
  metadata: JSON
  mockInput: JSON
  name: String
  next: [WorkflowTransition!]!
  packOverrides: [PackOverride!]
  publishResultAs: String
  retry: WorkflowTaskRetry
  runAsOrgId: String
  timeout: Int
  transitionMode: TransitionModes
  with: WorkflowTaskWithItems
  workflow: Workflow
  workflowId: ID
  securitySchema: JSON
}
```

</details>

<details>

<summary><strong><code>workflowTasks</code></strong>-Gets multiple workflow tasks.</summary>

**GraphQL schema:**

```graphql
workflowTasks(
  where: WorkflowTaskWhereInput
  limit: Int
  offset: Int
  order: [[String!]!] = [["name"]]
): [WorkflowTask!]!
```

</details>

### Operation type: Mutations

#### **Action option mutations**

<details>

<summary><strong><code>createActionOptions</code></strong>-Creates multiple action options.</summary>

**GraphQL schema:**

```graphql
createActionOptions(
  actionOptions: [ActionOptionInput!]!
  replace: Boolean
): [ActionOption]
```

**Usage example:**

```yaml
operation_type: "mutation"
operation: "createActionOptions"
variable_values:
  actionOptions:
    - optionLabel: "Environment"
      optionValue: "production"
      organizationId: "{{ CTX.org_id }}"
      packConfigId: "{{ CTX.pack_config_id }}"
      resourceName: "server"
  replace: false
fields: "id, optionLabel, optionValue"
```

</details>

#### **Clone operations mutations**

<details>

<summary><strong><code>unlinkClone</code></strong>-Unlinks a cloned object from its source.</summary>

**GraphQL schema:**

```graphql
unlinkClone(id: ID!, objectType: CloneableObjectType!): ID

enum CloneableObjectType {
  form
  template
  trigger
  workflow
  page
  site
}
```

**Usage example:**

```yaml
operation_type: "mutation"
operation: "unlinkClone"
variable_values:
  id: "{{ CTX.workflow_id }}"
  objectType: "workflow"
```

</details>

#### **Component mutations**

<details>

<summary><strong><code>createComponent</code></strong>-Creates a new component.</summary>

**GraphQL schema:**

```graphql
createComponent(component: CreateComponentInput!): Component

input CreateComponentInput {
  orgId: ID!
  name: String!
  description: String
  nodeTree: JSON!
  workflows: [ID]
  isSynced: Boolean
}
```

</details>

<details>

<summary><strong><code>updateComponent</code></strong>-Updates an existing component.</summary>

**GraphQL schema:**

```graphql
updateComponent(component: UpdateComponentInput!): Component
```

</details>

<details>

<summary><strong><code>deleteComponent</code></strong>-Deletes a component.</summary>

**GraphQL schema:**

```graphql
deleteComponent(id: ID!): Boolean
```

</details>

<details>

<summary><strong><code>duplicateComponent</code></strong>-Duplicates an existing component.</summary>

**GraphQL schema:**

```graphql
duplicateComponent(id: ID!): Component
```

</details>

#### **Foreign object reference mutations**

<details>

<summary><strong><code>createForeignObjectReference</code></strong>-Creates a foreign object reference.</summary>

**GraphQL schema:**

```graphql
createForeignObjectReference(
  foreignObjectReference: CreateForeignObjectReferenceInput
): ForeignObjectReference

input CreateForeignObjectReferenceInput {
  actionId: ID
  id: ID
  identifier: ID
  orgId: ID!
  packConfigId: ID
  referenceId: ID!
  workflowExecutionId: ID
}
```

</details>

<details>

<summary><strong><code>createOrUpdateForeignObjectReference</code></strong>-Creates or updates a foreign object reference.</summary>

**GraphQL schema:**

```graphql
createOrUpdateForeignObjectReference(
  foreignObjectReference: CreateForeignObjectReferenceInput
): ForeignObjectReference
```

</details>

#### **Form mutations**

<details>

<summary><strong><code>createForm</code></strong>-Creates a new form.</summary>

**GraphQL schema:**

```graphql
createForm(form: FormCreateInput!): Form

input FormCreateInput {
  clonedFromId: ID
  cloneOverrides: JSON
  description: String
  fields: [FormFieldInput!]
  id: ID
  isSynchronized: Boolean
  name: String
  orgId: ID!
  unpackedFromId: ID
}

```

**Usage example:**

```yaml
operation_type: "mutation"
operation: "createForm"
variable_values:
  form:
    name: "User Information Form"
    description: "Collects user information for onboarding"
    orgId: "{{ CTX.org_id }}"
    fields:
      - type: "TEXT_INPUT"
        index: 0
        schema:
          label: "Full Name"
          required: true
fields: "id, name, description, fields { id, type, schema }"
```

</details>

<details>

<summary><strong><code>submitForm</code></strong>-Submits form data and triggers associated workflow.</summary>

**GraphQL schema:**

```graphql
submitForm(
  id: ID!
  values: JSON!
  triggerId: ID!
  orgId: ID!
): JSON
```

</details>

<details>

<summary><strong><code>setFormTags</code></strong>-Sets tags for a form.</summary>

**GraphQL schema:**

```graphql
setFormTags(form: SetFormTagsInput!): Form

input SetFormTagsInput {
  id: ID!
  tagIds: [ID!]!
}
```

</details>

<details>

<summary><strong><code>shallowCloneForm</code></strong>-Creates a shallow clone of a form.</summary>

**GraphQL schema:**

```graphql
shallowCloneForm(
  id: ID!
  orgId: ID!
  overrides: ShallowCloneOverridesInput
  : Form)
```

</details>

<details>

<summary><strong><code>updateForm</code></strong>-Updates an existing form.</summary>

**GraphQL schema:**

```graphql
updateForm(form: FormUpdateInput!): Form
```

</details>

<details>

<summary><strong><code>deleteForm</code></strong>-Deletes a form.</summary>

**GraphQL schema:**

```graphql
deleteForm(id: ID!): Void
```

</details>

#### **Organization trigger instance mutations**

<details>

<summary><strong><code>updateOrgTriggerInstance</code></strong>-Updates an organization trigger instance.</summary>

**GraphQL schema:**

```graphql
updateOrgTriggerInstance(
  orgTriggerInstance: OrgTriggerInstanceInput!
): OrgTriggerInstance

input OrgTriggerInstanceInput {
  id: ID
  isManualActivation: Boolean
  organization: OrganizationInput
  orgId: ID
  lastSearchedAt: String
  trigger: TriggerUpdateInput
  triggerId: ID
  state: JSON
}
```

</details>

#### **Organization variable mutations**

<details>

<summary><strong><code>createOrgVariable</code></strong>-Creates a new organization variable.</summary>

**GraphQL schema:**

```graphql
createOrgVariable(orgVariable: OrgVariableCreateInput!): OrgVariable

input OrgVariableCreateInput {
  cascade: Boolean!
  id: ID
  name: String!
  value: String!
  category: OrgVariableCategory
  orgId: ID!
  packConfigId: ID
}
```

**Usage example:**

```yaml
operation_type: "mutation"
operation: "createOrgVariable"
variable_values:
  orgVariable:
    name: "api_endpoint"
    value: "https://api.example.com/v1"
    category: "general"
    cascade: true
    orgId: "{{ CTX.org_id }}"
fields: "id, name, value, category, cascade"
```

</details>

<details>

<summary><strong><code>deleteOrgVariable</code></strong>-Deletes an organization variable.</summary>

**GraphQL schema:**

```graphql
deleteOrgVariable(id: ID!): ID
```

</details>

<details>

<summary><strong><code>updateOrgVariables</code></strong>-Updates multiple organization variables.</summary>

**GraphQL schema:**

```graphql
updateOrgVariables(
  orgVariables: [OrgVariableUpdateInput!]!
): [OrgVariable!]!

input OrgVariableUpdateInput {
  cascade: Boolean
  category: OrgVariableCategory
  id: ID
  name: String!
  value: String
  orgId: ID
  packConfigId: ID
}
```

</details>

#### **Organization management mutations**

<details>

<summary><strong><code>bulkCreateOrganizations</code></strong>-Creates multiple organizations in bulk.</summary>

**GraphQL schema:**

```graphql
bulkCreateOrganizations(
  organizations: [OrganizationInput!]!
): [Organization!]!
```

</details>

<details>

<summary><strong><code>bulkDeleteOrganizations</code></strong>-Deletes multiple organizations in bulk.</summary>

**GraphQL schema:**

```graphql
bulkDeleteOrganizations(organizationIds: [ID!]!): Void
```

</details>

<details>

<summary><strong><code>createOrganization</code></strong>-Creates a single organization.</summary>

**GraphQL schema:**

```graphql
createOrganization(organization: OrganizationInput): Organization

input OrganizationInput {
  domain: String
  id: ID
  isEnabled: Boolean
  managingOrgId: ID
  name: String!
  orgSlug: String
  rocSiteId: String
  tid: String
  tagIds: [ID!]
}
```

</details>

<details>

<summary><strong><code>createOrganizations</code></strong>-Creates multiple organizations.</summary>

**GraphQL schema:**

```graphql
createOrganizations(
  organizations: [OrganizationInput!]!
): [Organization]
```

</details>

<details>

<summary><strong><code>deleteOrganization</code></strong>-Deletes an organization.</summary>

**GraphQL schema:**

```graphql
deleteOrganization(id: ID!): Void
```

</details>

<details>

<summary><strong><code>updateManagedAndSubOrganizations</code></strong>-Updates managed and sub-organizations.</summary>

**GraphQL schema:**

```graphql
updateManagedAndSubOrganizations(
  organization: OrganizationUpdateInput!
): Int
```

</details>

<details>

<summary><strong><code>updateOrganization</code></strong>-Updates an organization.</summary>

**GraphQL schema:**

```graphql
updateOrganization(organization: OrganizationUpdateInput): Organization
```

</details>

<details>

<summary><strong><code>bulkUpdateOrganizationFeaturePreviewSettingByLabel</code></strong>-Bulk updates feature preview settings by label.</summary>

**GraphQL schema:**

```graphql
bulkUpdateOrganizationFeaturePreviewSettingByLabel(
  isEnabled: Boolean!
  label: String!
  orgIds: [ID!]!
): [OrganizationFeaturePreviewSetting!]!
```

</details>

#### **Pack configuration mutations**

<details>

<summary><strong><code>synchronizePackBundleConfigs</code></strong>-Synchronizes pack bundle configurations.</summary>

**GraphQL schema:**

```graphql
synchronizePackBundleConfigs(
  orgId: ID!
  packBundleId: ID!
  primaryPackConfigId: ID!
): [SynchronizedPackConfig!]!
```

</details>

<details>

<summary><strong><code>createPackConfig</code></strong>-Creates a new pack configuration.</summary>

**GraphQL schema:**

```graphql
createPackConfig(packConfig: PackConfigCreateInput!): PackConfig

input PackConfigCreateInput {
  id: ID
  name: String!
  default: Boolean
  description: String
  config: JSON
  metadata: JSON
  orgId: ID!
  packId: ID!
}
```

</details>

<details>

<summary><strong><code>deletePackConfig</code></strong>-Deletes a pack configuration.</summary>

**GraphQL schema:**

```graphql
deletePackConfig(id: ID!, orgId: ID!): Void
```

</details>

<details>

<summary><strong><code>refetchPackConfigRefOptions</code></strong>-Refetches pack configuration reference options.</summary>

**GraphQL schema:**

```graphql
refetchPackConfigRefOptions(
  packConfigId: ID!
  reference: JSON
): JobRequestedResponse
```

</details>

<details>

<summary><strong><code>testPackConfig</code></strong>-Tests a pack configuration.</summary>

**GraphQL schema:**

```graphql
testPackConfig(packConfig: PackConfigTestInput!): JobRequestedResponse
```

</details>

<details>

<summary><strong><code>updatePackConfig</code></strong>-Updates a pack configuration.</summary>

**GraphQL schema:**

```graphql
updatePackConfig(packConfig: PackConfigUpdateInput!): PackConfig
```

</details>

<details>

<summary><strong><code>updatePackConfigs</code></strong>-Updates multiple pack configurations.</summary>

**GraphQL schema:**

```graphql
updatePackConfigs(
  packConfigs: [PackConfigUpdateInput!]!
): [PackConfig!]!
```

</details>

#### **Pack mutations**

<details>

<summary><strong><code>generatePackOrBundleAuthUrl</code></strong>-Generates authorization URL for pack or bundle.</summary>

**GraphQL schema:**

```graphql
generatePackOrBundleAuthUrl(
  orgId: ID!
  packBundleId: ID
  packConfigId: ID
  extra: JSON
): AuthUrlResponse

type AuthUrlResponse {
  authUrl: String
  error: String
}
```

</details>

<details>

<summary><strong><code>installPack</code></strong>-Installs a pack for an organization.</summary>

**GraphQL schema:**

```graphql
installPack(orgId: ID!, packId: ID!, name: String): Organization
```

</details>

<details>

<summary><strong><code>getPackInstallations</code></strong>-Gets pack installation information.</summary>

**GraphQL schema:**

```graphql
getPackInstallations(packId: ID!): PackInstalledByResponse
```

</details>

<details>

<summary><strong><code>getPackPageUrl</code></strong>-Gets the URL for a pack page</summary>

**GraphQL schema:**

```graphql
getPackPageUrl(integrationRef: String!, pagePath: String!): String
```

</details>

<details>

<summary><strong><code>updatePack</code></strong>-Updates a pack.</summary>

**GraphQL schema:**

```graphql
updatePack(pack: PackUpdateInput!): Pack
```

</details>

#### **Page mutations**

<details>

<summary><strong><code>createPage</code></strong>-Creates a new page.</summary>

**GraphQL schema:**

```graphql
createPage(
  page: PageCreateInput!
  preset: String
  nodes: [PageNodeInput]
): Page

input PageCreateInput {
  id: ID
  loader: Loader
  siteId: ID
  workflows: [WorkflowInput]
  name: String!
  path: String!
  variables: [JSON]
  orgId: ID!
  clonedFromId: ID
  isSynchronized: Boolean
  cloneOverrides: JSON
}
```

</details>

<details>

<summary><strong><code>updatePage</code></strong>-Updates an existing page.</summary>

**GraphQL schema:**

```graphql
updatePage(
  page: PageUpdateInput!
  nodes: [PageNodeInput]
): Page
```

</details>

<details>

<summary><strong><code>deletePage</code></strong>-Deletes a page.</summary>

**GraphQL schema:**

```graphql
deletePage(id: ID!): Void
```

</details>

<details>

<summary><strong><code>updatePageNode</code></strong>-Updates a page node.</summary>

**GraphQL schema:**

```graphql
updatePageNode(id: ID!, props: JSON!): PageNode
```

</details>

<details>

<summary><strong><code>updatePageNodeByCraftId</code></strong>-Updates a page node by craft ID.</summary>

**GraphQL schema:**

```graphql
updatePageNodeByCraftId(
  craftId: String!
  pageId: ID!
  props: JSON!
): PageNode
```

</details>

#### **Site mutations**

<details>

<summary><strong><code>createSite</code></strong>-Creates a new site/app.</summary>

**GraphQL schema:**

```graphql
createSite(site: SiteCreateInput!): Site

input SiteCreateInput {
  name: String
  domain: String
  orgId: ID!
  template: String
  theme: JSON
  pages: [PagesImportInput]
  clonedFromId: ID
  isSynchronized: Boolean
  cloneOverrides: JSON
}
```

</details>

<details>

<summary><strong><code>updateSite</code></strong>-Updates an existing site/app.</summary>

**GraphQL schema:**

```graphql
updateSite(site: SiteUpdateInput!): Site
```

</details>

<details>

<summary><strong><code>updateSites</code></strong>-Updates multiple sites.</summary>

**GraphQL schema:**

```graphql
updateSites(sites: [SiteUpdateInput!]!): [Site!]!
```

</details>

<details>

<summary><strong><code>deleteSite</code></strong>-Deletes a site/app.</summary>

**GraphQL schema:**

```graphql
deleteSite(id: ID!): Void
```

</details>

<details>

<summary><strong><code>validateSiteCustomDomainDNS</code></strong>-Validates custom domain DNS settings.</summary>

**GraphQL schema:**

```graphql
validateSiteCustomDomainDNS(id: ID!): DNSValidationResponse

type DNSValidationResponse {
  isValid: Boolean
  message: String
}
```

</details>

#### **Tag mutations**

<details>

<summary><strong><code>createTag</code></strong>-Creates a new tag.</summary>

**GraphQL schema:**

```graphql
createTag(tag: TagCreateInput!): Tag

input TagCreateInput {
  id: ID
  name: String
  description: String
  orgId: ID!
  color: String
}
```

</details>

<details>

<summary><strong><code>deleteTag</code></strong>-Deletes a tag.</summary>

**GraphQL schema:**

```graphql
deleteTag(id: ID!): ID
```

</details>

<details>

<summary><strong><code>updateTag</code></strong>-Updates a tag.</summary>

**GraphQL schema:**

```graphql
updateTag(tag: TagUpdateInput!): Tag
```

</details>

<details>

<summary><strong><code>updateTags</code></strong>-Updates multiple tags.</summary>

**GraphQL schema:**

```graphql
updateTags(tags: [TagUpdateInput!]!): [Tag!]!
```

</details>

<details>

<summary><strong><code>setOrganizationTags</code></strong>-Sets tags for an organization.</summary>

**GraphQL schema:**

```graphql
setOrganizationTags(tagIds: [ID!]!, orgId: ID!): Organization
```

</details>

#### **Template mutations**

<details>

<summary><strong><code>createTemplate</code></strong>-Creates a new template.</summary>

**GraphQL schema:**

````graphql
createTemplate(template: TemplateCreateInput!): Template

input TemplateCreateInput {
  body: String!
  clonedFromId: ID
  cloneOverrides: JSON
  contentType: String
  context: JSON
  description: String
  id: ID
  isShared: Boolean
  isSynchronized: Boolean
  language: String
  name: String!
  orgId: ID!
  tags: [TagInput!]
  unpackedFromId: ID
}

## Best Practices

### Query Optimization

1. **Limit Data Retrieval**: Only request the fields you actually need
2. **Use Pagination**: Implement proper limit and offset for large datasets
3. **Filter Early**: Apply filters at the query level rather than post-processing

### Error Handling

```yaml
# Example workflow task with error handling
- name: execute_graphql_query
  action: rewst.generic_graph_request
  parameters:
    operation_type: "query"
    operation: "workflows"
    variable_values:
      limit: 100
      where:
        orgId: "{{ CTX.org_id }}"
  on_failure:
    - log_error:
        message: "GraphQL query failed: {{ RESULT.error }}"
````

</details>

## Security considerations

1. Always validate user inputs before including in queries
2. Use organization and permission filters to restrict data access
3. Track usage patterns for potential security issues

## Common use cases for the Generic GraphQL request action

### Bulk data operations

**Action configuration:**

* **Operation type**: `mutation`
* **Operation**: `updateOrgVariables`
*   **Variable values**:

    ```json
    {
      "orgVariables": [
        {
          "id": "var1",
          "name": "setting1",
          "value": "updated_value1"
        },
        {
          "id": "var2",
          "name": "setting2",
          "value": "updated_value2"
        }
      ]
    }
    ```

### Complex reporting

**Action configuration:**

* **Operation type**: `query`
* **Operation**: `workflows`
*   **Variable values**:

    ```json
    {
      "where": {
        "orgId": "{{ CTX.org_id }}"
      },
      "limit": 1000
    }
    ```
*   **Fields**:

    ```
    id
    name
    description
    createdAt
    updatedAt
    tasks {
      id
      name
      action {
        name
        pack {
          name
        }
      }
    }
    triggers {
      id
      name
      enabled
    }
    ```

### Data synchronization

**Action configuration:**

* **Operation type**: `query`
* **Operation**: `organizations`
*   **Variable values**:

    ```json
    {
      "where": {
        "managingOrgId": "{{ CTX.parent_org_id }}"
      },
      "order": [["name"]]
    }
    ```
* **Fields**: `id, name, domain, createdAt, managedOrgs { id, name }`

## Troubleshoot the Generic GraphQL request action

### **Permission denied**

* Verify the feature flag is enabled for your organization

### **Query syntax errors**

* Validate GraphQL syntax using a GraphQL validator
* Check field names against the schema
* Ensure variable types match the expected schema types

### **Rate limiting**

* Implement exponential backoff for retries
* Consider breaking large operations into smaller batches
* Monitor API usage patterns

### Debug tips

1. Begin with basic queries before building complex operations
2. For debugging, use the `raw_query` parameter to see exact queries
3. Review workflow execution logs for detailed error messages
4. Build queries incrementally, adding fields and filters gradually

