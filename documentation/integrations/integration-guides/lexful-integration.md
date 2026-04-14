# Lexful integration

{% hint style="info" %}
&#x20;If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the Lexful integration do?

Our Lexful integration enables the automation of IT documentation management. Use the Lexful API within Rewst workflows to manage entities, organizations, users, labels, and entity types through a flexible schema-driven API with built-in search, revision history, and access control.

## Set up the Lexful integration

### Set up steps in Lexful

1. Navigate to your [Lexful Dashboard](https://app.us.lexful.app) and log in with your account credentials.
2. Navigate to **Settings > Platform > APIs** .
3. Enter `Rewst` into the **API key name** **field**.
4. Click **Generate API Key**
5. Copy the **API Key ID**, **Account ID**, and **API Key Secret** and store these values somewhere secure. You'll need them for further steps in Rewst. Note that the secret will only be displayed once, and can't be retrieved again after you navigate away from the page.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `Lexful` in the integrations page.
3. Click on the integration tile to launch setup.
4. Enter the information copied from Lexful into the relevant fields:
   1. **API Key ID**&#x20;
   2. **API Key Secret**&#x20;
   3. **Account ID**
5. Enter the **Base URL**:
   * **Production**: `https://api.lexful.com` - default, use this for most integrations
   * **UAT**: `https://api.uat.lexful.net` - for testing, only use this if you are certain it applies to your instance of Lexful
6. Click **Save Configuration**.
7. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.&#x20;

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

View Lexful's own API documentation [here](https://lexful.mintlify.app/).

| Category                | Action                          | Description                                                                                                                     |
| ----------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Account Management      | Get Account Settings            | Retrieves account settings for the authenticated account.                                                                       |
| Account Management      | Update Account Settings         | Updates account settings for the authenticated account. Only provide the fields you want to update.                             |
| Entities                | List Entity Access Grants       | Lists access grants for an entity.                                                                                              |
| Entities                | Delete Entity                   | Deletes an entity. Irreversible.                                                                                                |
| Entities                | Get Entity Revision             | Retrieves a specific revision of an entity.                                                                                     |
| Entities                | Get a Secure Value              | Retrieves the decrypted value of a secure/encrypted entity property.                                                            |
| Entities                | Update Entity                   | Updates an existing entity. Request body accepts dynamic properties based on entity type schema.                                |
| Entities                | Create Entity                   | Creates a new entity of the specified type. Request body accepts dynamic properties based on entity type schema.                |
| Entities                | List Entity Revisions           | Lists the revision history for an entity. Supports pagination.                                                                  |
| Entities                | List Entities                   | Lists all entities of a given type. Supports pagination.                                                                        |
| Entities                | Get Entity                      | Retrieves a specific entity by ID.                                                                                              |
| Entities                | Remove Entity Access Grants     | Removes access grants from an entity.                                                                                           |
| Entities                | Get Entity Counts               | Retrieves entity count statistics, optionally filtered by entity type or organization.                                          |
| Entities                | Add Entity Access Grants        | Sets access grants for an entity. Idempotent — duplicate grants are ignored.                                                    |
| Entity Types            | Delete Entity Type Property     | Deletes a property from an entity type. Irreversible.                                                                           |
| Entity Types            | List Entity Types               | Lists all entity type definitions. Supports pagination.                                                                         |
| Entity Types            | Get Entity Type                 | Retrieves a specific entity type definition.                                                                                    |
| Entity Types            | Update Entity Type Property     | Updates an existing property on an entity type.                                                                                 |
| Entity Types            | Create Entity Type Property     | Adds a property to an entity type.                                                                                              |
| Entity Types            | Delete Entity Type Reference    | Deletes a reference from an entity type. Irreversible.                                                                          |
| Entity Types            | Create Entity Type Reference    | Adds a reference relationship to an entity type.                                                                                |
| Entity Types            | Update Entity Type Reference    | Updates an existing reference on an entity type.                                                                                |
| Entity Types            | Create Entity Type              | Creates a new entity type definition.                                                                                           |
| Entity Types            | Update Entity Type              | Updates an existing entity type definition.                                                                                     |
| Generic Request         | Lexful API Request              | Generic action for making authenticated requests against the Lexful API. Auto-includes Authorization and X-Account-ID headers.  |
| Labels                  | Update Label                    | Updates an existing label.                                                                                                      |
| Labels                  | Delete Label                    | Deletes a label (soft delete).                                                                                                  |
| Labels                  | Remove Label from Organizations | Removes a label from one or more organizations.                                                                                 |
| Labels                  | Create Label                    | Creates a new label.                                                                                                            |
| Labels                  | Assign Label to Organizations   | Assigns a label to one or more organizations. Idempotent.                                                                       |
| Labels                  | Remove Label from Entities      | Removes a label from one or more entities.                                                                                      |
| Labels                  | Assign Label to Entities        | Assigns a label to one or more entities. Idempotent.                                                                            |
| Labels                  | Get Label                       | Retrieves a specific label by ID.                                                                                               |
| Labels                  | List Labels                     | Lists all labels. Supports pagination.                                                                                          |
| Organization Management | Delete Organization             | Deletes an organization. Irreversible. All associated data will be permanently deleted.                                         |
| Organization Management | List Organizations              | Lists all organizations in your Lexful account. Supports pagination.                                                            |
| Organization Management | Bulk Update Organizations       | Updates multiple organizations in a single request - up to 100. Each object must include an `id` field.                         |
| Organization Management | Update Organization             | Updates an existing organization. Only provide fields to update.                                                                |
| Organization Management | Get Organization                | Retrieves details for a specific organization.                                                                                  |
| Organization Management | Create Organization Type        | Creates a new organization type. Supports single or bulk creation - up to 100.                                                  |
| Organization Management | Create Organization Status      | Creates a new organization status. Supports single or bulk creation - up to 100.                                                |
| Organization Management | Create Organization             | Creates a new organization. Supports single or bulk creation - up to 100.                                                       |
| Organization Management | List Organization Types         | Lists all organization type definitions. Supports pagination.                                                                   |
| Organization Management | List Organization Statuses      | Lists all organization status definitions. Supports pagination.                                                                 |
| Search                  | Search                          | Searches across entities and organizations. Returns results ranked by relevance or recency.                                     |
| User Management         | List User Roles                 | Lists all available user role definitions.                                                                                      |
| User Management         | Update User                     | Updates an existing user. Only provide fields to update.                                                                        |
| User Management         | List Users                      | Lists all users in your Lexful account. Supports pagination.                                                                    |
| User Management         | Delete User                     | Deletes a user. Irreversible.                                                                                                   |
| User Management         | Create User                     | Creates a new user.                                                                                                             |
| User Management         | Get User                        | Retrieves a specific user by ID.                                                                                                |
