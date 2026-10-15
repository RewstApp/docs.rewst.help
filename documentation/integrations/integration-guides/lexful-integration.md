# Lexful integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the Lexful integration do?

Our Lexful integration enables the automation of IT documentation management. Use the Lexful API within Rewst workflows to manage assets, organizations, users, labels, and asset types through a flexible schema-driven API with built-in search, revision history, and access control.

## Set up the Lexful integration

### Set up steps in Lexful

1. Sign in to your Lexful account with administrative credentials.
2. Navigate to **Platform > API Keys**.
3. Select **New Key**.&#x20;
4. Enter `Rewst` into the **API key name** **field**.
5. Click **Create Key**
6. Copy the **API Key ID** and **API Key Secret** from the dialog that appears. Store these values somewhere secure. You'll need them for further steps in Rewst. Note that the secret will only be displayed once, and can't be retrieved again after you navigate away from the page.
7. Copy the **Account ID** from the bar above the key list.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `Lexful` in the integrations page.
3. Click on the integration tile to launch setup.
4. Enter the information copied from Lexful into the relevant fields:
   1. **API Key ID**
   2. **API Key Secret**
   3. **Account ID**
5. Enter the **Base URL, Production**: `https://api.us.lexful.app`
6. Click **Save Configuration**.
7. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).
{% endhint %}

View Lexful's own API documentation [here](https://developer.lexful.ai/).

| Category                | Action                          | Description                                                                                                                    |
| ----------------------- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Account Management      | Get Account Settings            | Retrieves account settings for the authenticated account.                                                                      |
| Account Management      | Update Account Settings         | Updates account settings for the authenticated account. Only provide the fields you want to update.                            |
| Assets                  | List Asset Access Grants        | Lists access grants for an asset.                                                                                              |
| Assets                  | Delete Asset                    | Deletes an asset.                                                                                                              |
| Assets                  | Get Asset Revision              | Retrieves a specific revision of an asset.                                                                                     |
| Assets                  | Get a Secure Value              | Retrieves the decrypted value of a secure/encrypted asset property.                                                            |
| Assets                  | Update Asset                    | Updates an existing asset. Request body accepts dynamic properties based on asset type schema.                                 |
| Assets                  | Create Asset                    | Creates a new asset of the specified type. Request body accepts dynamic properties based on asset type schema.                 |
| Assets                  | List Asset Revisions            | Lists the revision history for an asset. Supports pagination.                                                                  |
| Assets                  | List Asset                      | Lists all assets of a given type. Supports pagination.                                                                         |
| Assets                  | Get Asset                       | Retrieves a specific asset by ID.                                                                                              |
| Assets                  | Remove Asset Access Grants      | Removes access grants from an asset.                                                                                           |
| Assets                  | Get Asset Counts                | Retrieves asset count statistics, optionally filtered by asset type or organization.                                           |
| Assets                  | Add Asset Access Grants         | Sets access grants for an asset. Idempotent — duplicate grants are ignored.                                                    |
| Asset Types             | Delete Asset Type Property      | Deletes a property from an asset type. Irreversible.                                                                           |
| Asset Types             | List Asset Types                | Lists all asset type definitions. Supports pagination.                                                                         |
| Asset Types             | Get Asset Type                  | Retrieves a specific asset type definition.                                                                                    |
| Asset Types             | Update Asset Type Property      | Updates an existing property on an asset type.                                                                                 |
| Asset Types             | Create Asset Type Property      | Adds a property to an asset type.                                                                                              |
| Asset Types             | Delete Asset Type Reference     | Deletes a reference from an asset type. Irreversible.                                                                          |
| Asset Types             | Create Asset Type Reference     | Adds a reference relationship to an asset type.                                                                                |
| Asset Types             | Update Asset Type Reference     | Updates an existing reference on an asset type.                                                                                |
| Asset Types             | Create Asset Type               | Creates a new asset type definition.                                                                                           |
| Asset Types             | Update Asset Type               | Updates an existing asset type definition.                                                                                     |
| Generic Request         | Lexful API Request              | Generic action for making authenticated requests against the Lexful API. Auto-includes Authorization and X-Account-ID headers. |
| Labels                  | Update Label                    | Updates an existing label.                                                                                                     |
| Labels                  | Delete Label                    | Deletes a label (soft delete).                                                                                                 |
| Labels                  | Remove Label from Organizations | Removes a label from one or more organizations.                                                                                |
| Labels                  | Create Label                    | Creates a new label.                                                                                                           |
| Labels                  | Assign Label to Organizations   | Assigns a label to one or more organizations. Idempotent.                                                                      |
| Labels                  | Remove Label from Assets        | Removes a label from one or more assets.                                                                                       |
| Labels                  | Assign Label to Assets          | Assigns a label to one or more assets. Idempotent.                                                                             |
| Labels                  | Get Label                       | Retrieves a specific label by ID.                                                                                              |
| Labels                  | List Labels                     | Lists all labels. Supports pagination.                                                                                         |
| Organization Management | Delete Organization             | Deletes an organization. All associated data will be permanently deleted.                                                      |
| Organization Management | List Organizations              | Lists all organizations in your Lexful account. Supports pagination.                                                           |
| Organization Management | Bulk Update Organizations       | Updates multiple organizations in a single request - up to 100. Each object must include an `id` field.                        |
| Organization Management | Update Organization             | Updates an existing organization. Only provide fields to update.                                                               |
| Organization Management | Get Organization                | Retrieves details for a specific organization.                                                                                 |
| Organization Management | Create Organization             | Creates a new organization. Supports single or bulk creation - up to 100.                                                      |
| Search                  | Search                          | Searches across assets and organizations. Returns results ranked by relevance or recency.                                      |
| User Management         | List User Roles                 | Lists all available user role definitions.                                                                                     |
| User Management         | Update User                     | Updates an existing user. Only provide fields to update.                                                                       |
| User Management         | List Users                      | Lists all users in your Lexful account. Supports pagination.                                                                   |
| User Management         | Delete User                     | Deletes a user.                                                                                                                |
| User Management         | Create User                     | Creates a new user.                                                                                                            |
| User Management         | Get User                        | Retrieves a specific user by ID.                                                                                               |
