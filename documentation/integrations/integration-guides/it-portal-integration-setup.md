# IT Portal integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the IT Portal integration do?

Our IT Portal integration allows your Rewst workflows to read from and write to IT Portal automatically, so your documentation stays up to date without manual effort. The key action categories available include:

* Accounts - List, create, get, and update portal accounts
* Companies - Create and manage company records
* Contacts - List, create, and manage contact records
* Documents - Create, retrieve, update, and delete documents
* Facilities - Manage facility records
* IP Networks - Create and manage IP network documentation
* Knowledge Base - Create and manage KB articles
* Interactions - Manage interaction records
* Generic Request - Make any authenticated API call to ITPortal for anything not covered by a dedicated action

## Set up the IT Portal integration

### Set up steps in IT Portal

1. Log in to IT Portal with your credentials.
2. Navigate to **Profile (name) > Admin Settings > API Keys**.
3. Click **Create API 2. x Key**. Don't click to create a 3.0 key, as this won't work with Rewst's integration.
4. Toggle the option **Allow to create same name objects** to off.
5. Enter a description for the API key. We recommend `REWST`.
6. Click **Create**.
7.  Copy the new API key and store it somewhere secure. Once you leave this screen you won't be able to view the key again. You'll need this information for further steps in Rewst.

    <img src="https://docs.rewst.help/~gitbook/image?url=https%3A%2F%2F3039672601-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fh0G0em3PH6aDfPoI5XpN%252Fuploads%252Fk2OwZ48iznrZIlPW4yUM%252FScreenshot%25202026-10-21%2520at%252011.27.15%25E2%2580%25AFAM.png%3Falt%3Dmedia%26token%3Db7a136ff-f6a7-4b21-b1ad-a10f9d8ba7b0&#x26;width=768&#x26;dpr=3&#x26;quality=100&#x26;sign=2e6b2dcb27d88f7705f8b56b2a9434c4&#x26;sv=3" alt="" height="653" width="1500">

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `IT Portal` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-05-02 at 11.45.36 AM.png>)
3. Click on the integration tile to launch the configuration setup page.
4. Under **Parameters**:
   1. Enter the key copied from IT Portal into the **API Key** field.
   2. Enter the **Base URL** from your IT Portal environment - e.g. `demo.itportal.com` .
5. Click **Save Configuration**.
6. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).
{% endhint %}

| Category                   | Action                             | Description                                                                                                                                                                |
| -------------------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Accounts**               | List Accounts                      | Fetches lists of portal accounts with optional filters. See notes on individual parameters below                                                                           |
| **Accounts**               | Create Account                     | New account will be added to the portal                                                                                                                                    |
| **Accounts**               | Get Account                        | This method fetches a single account resource. It is the canonical URI for any account resource provided by the API                                                        |
| **Accounts**               | Delete Account                     | Description coming soon...                                                                                                                                                 |
| **Accounts**               | Update Account                     | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Accounts**               | Get Credentials For Account        | This method fetches a single account credentials resource                                                                                                                  |
| **Additional Credentials** | List Additional Credentials        | Fetches lists of additional credentials with optional filters. See notes on individual parameters below                                                                    |
| **Additional Credentials** | Create Additional Credential       | New additional credential will be added to the portal object                                                                                                               |
| **Additional Credentials** | Get Additional Credential          | This method fetches a single additional credential resource. It is the canonical URI for any additional credential resource provided by the API                            |
| **Additional Credentials** | Delete Additional Credential       | Description coming soon...                                                                                                                                                 |
| **Additional Credentials** | Update Additional Credential       | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Addresses**              | Create Address                     | New address will be added to the Portal company                                                                                                                            |
| **Addresses**              | List Addresses                     | Fetches lists of addresses with optional filters. See notes on individual parameters below                                                                                 |
| **Addresses**              | Get Address                        | This method fetches a single address resource. It is the canonical URI for any address resource provided by the API                                                        |
| **Addresses**              | Delete Address                     | Description coming soon...                                                                                                                                                 |
| **Addresses**              | Update Address                     | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Agreements**             | List Agreements                    | Fetches lists of portal agreements with optional filters. See notes on individual parameters below                                                                         |
| **Agreements**             | Create Agreement                   | New agreement will be added to the portal                                                                                                                                  |
| **Agreements**             | Get Agreement                      | This method fetches a single agreement resource. It is the canonical URI for any agreement resource provided by the API                                                    |
| **Agreements**             | Delete Agreement                   | Description coming soon...                                                                                                                                                 |
| **Agreements**             | Update Agreement                   | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Cabinets**               | List Cabinets                      | Fetches lists of portal cabinets with optional filters. See notes on individual parameters below                                                                           |
| **Cabinets**               | Create Cabinet                     | New cabinet will be added to the portal                                                                                                                                    |
| **Cabinets**               | Get Cabinet                        | This method fetches a single cabinet resource. It is the canonical URI for any cabinet resource provided by the API                                                        |
| **Cabinets**               | Delete Cabinet                     | Description coming soon...                                                                                                                                                 |
| **Cabinets**               | Update Cabinet                     | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Categories Types**       | List KB Categories                 | Fetches lists of portal KB categories with optional filters. See notes on individual parameters below                                                                      |
| **Categories Types**       | List Company Types                 | Fetches lists of portal company types with optional filters. See notes on individual parameters below                                                                      |
| **Categories Types**       | List Account Types                 | Fetches lists of portal account types with optional filters. See notes on individual parameters below                                                                      |
| **Categories Types**       | List Agreement Types               | Fetches lists of portal agreement types with optional filters. See notes on individual parameters below                                                                    |
| **Categories Types**       | List Contact Types                 | Fetches lists of portal contact types with optional filters. See notes on individual parameters below                                                                      |
| **Categories Types**       | List Facility Types                | Fetches lists of portal facility types with optional filters. See notes on individual parameters below                                                                     |
| **Categories Types**       | List Device Types                  | Fetches lists of portal device types with optional filters. See notes on individual parameters below                                                                       |
| **Categories Types**       | List Document Types                | Fetches lists of portal document types with optional filters. See notes on individual parameters below                                                                     |
| **Companies**              | List Companies                     | Fetches lists of portal companies with optional filters. See notes on individual parameters below                                                                          |
| **Companies**              | Create Company                     | New Company will be added to the portal                                                                                                                                    |
| **Companies**              | Get Company                        | This method fetches a single company resource. It is the canonical URI for any company resource provided by the API                                                        |
| **Companies**              | Delete Company                     | Description coming soon...                                                                                                                                                 |
| **Companies**              | Update Company                     | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Companies**              | List Company Accounts              | Fetches lists of portal accounts with optional filters. See notes on individual parameters below                                                                           |
| **Companies**              | List Company Addresses             | Fetches lists of portal addresses with optional filters. See notes on individual parameters below                                                                          |
| **Configurations**         | List Configurations                | Fetches lists of portal configurations with optional filters. See notes on individual parameters below                                                                     |
| **Configurations**         | Create Configuration               | New configuration will be added to the portal. For the Configuration Type ID, please create at least one Configuration via ITPortal then use the Get Configuration action. |
| **Configurations**         | Get Configuration                  | This method fetches a single configuration resource. It is the canonical URI for any configuration resource provided by the API                                            |
| **Configurations**         | Delete Configuration               | Description coming soon...                                                                                                                                                 |
| **Configurations**         | Update Configuration               | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Contacts**               | List Contacts                      | Fetches lists of portal contacts with optional filters. See notes on individual parameters below                                                                           |
| **Contacts**               | Create Contact                     | New contact will be added to the portal                                                                                                                                    |
| **Contacts**               | Get Contact                        | This method fetches a single contact resource. It is the canonical URI for any contact resource provided by the API                                                        |
| **Contacts**               | Delete Contact                     | Description coming soon...                                                                                                                                                 |
| **Contacts**               | Update Contact                     | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | List Devices                       | Fetches lists of portal devices with optional filters. See notes on individual parameters below                                                                            |
| **Devices**                | Create Device                      | New device will be added to the portal                                                                                                                                     |
| **Devices**                | Get Device                         | This method fetches a single device resource. It is the canonical URI for any device resource provided by the API                                                          |
| **Devices**                | Delete Device                      | Description coming soon...                                                                                                                                                 |
| **Devices**                | Update Device                      | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | Get Management URLs For Device     | This method fetches a single device Management Urls resource                                                                                                               |
| **Devices**                | Create Device Management URL       | New Device Management Url will be added to the portal                                                                                                                      |
| **Devices**                | Get IPs For Device                 | This method fetches a single device IPs resource                                                                                                                           |
| **Devices**                | Create Device IP                   | New device IP will be added to the portal                                                                                                                                  |
| **Devices**                | Get Configuration Files For Device | This method fetches a single device configurations files resource                                                                                                          |
| **Devices**                | Get Credentials For Device         | This method fetches a single device credentials resource                                                                                                                   |
| **Devices**                | Update Device IP                   | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | Delete Management URL              | Description coming soon...                                                                                                                                                 |
| **Devices**                | Update Device Management URL       | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | Get Notes For Device               | This method fetches a single device Notes resource                                                                                                                         |
| **Devices**                | Create Device Note                 | New device Note will be added to the portal                                                                                                                                |
| **Devices**                | Update Device Note                 | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | Get Switch Port Ranges For Device  | This method fetches a single device mapped switch port ranges resource                                                                                                     |
| **Devices**                | Create Device Switch Port Range    | New device switch port range will be added to the portal                                                                                                                   |
| **Devices**                | Delete Switch Port Range           | Description coming soon...                                                                                                                                                 |
| **Devices**                | Update Switch Port Range           | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Devices**                | Update Switch Port                 | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Documents**              | List Documents                     | Fetches lists of portal documents with optional filters. See notes on individual parameters below                                                                          |
| **Documents**              | Create Document                    | New document will be added to the portal                                                                                                                                   |
| **Documents**              | Get Document                       | This method fetches a single document resource. It is the canonical URI for any document resource provided by the API                                                      |
| **Documents**              | Delete Document                    | Description coming soon...                                                                                                                                                 |
| **Documents**              | Update Document                    | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Facilities**             | List Facilities                    | Fetches lists of portal facilities with optional filters. See notes on individual parameters below                                                                         |
| **Facilities**             | Create Facility                    | New facility will be added to the portal                                                                                                                                   |
| **Facilities**             | Get Facility                       | This method fetches a single facility resource. It is the canonical URI for any facility resource provided by the API                                                      |
| **Facilities**             | Delete Facility                    | Description coming soon...                                                                                                                                                 |
| **Facilities**             | Update Facility                    | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Generic Request**        | IT Portal API Request              | Generic action for making authenticated requests against the IT Portal API                                                                                                 |
| **Interactions**           | Delete Interaction                 | Description coming soon...                                                                                                                                                 |
| **Interactions**           | List Interactions                  | Description coming soon...                                                                                                                                                 |
| **Interactions**           | Create Interactions                | Description coming soon...                                                                                                                                                 |
| **Ip Networks**            | List IP Networks                   | Fetches lists of portal IP Networks with optional filters. See notes on individual parameters below                                                                        |
| **Ip Networks**            | Create IP Network                  | New ip network will be added to the portal                                                                                                                                 |
| **Ip Networks**            | Get IP Network                     | This method fetches a single IP network resource. It is the canonical URI for any IP network resource provided by the API                                                  |
| **Ip Networks**            | Delete IP Network                  | Description coming soon...                                                                                                                                                 |
| **Ip Networks**            | Update IP Network                  | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Kbs**                    | List KBs                           | Fetches lists of portal knowledge base articles with optional filters. See notes on individual parameters below                                                            |
| **Kbs**                    | Create KBs                         | New knowledge base article will be added to the portal                                                                                                                     |
| **Kbs**                    | Get KB                             | This method fetches a single knowledge base article resource. It is the canonical URI for any KB resource provided by the API                                              |
| **Kbs**                    | Delete KB                          | Description coming soon...                                                                                                                                                 |
| **Kbs**                    | Update KB                          | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Sheets**                 | Get Sheet                          | Fetch object sheet                                                                                                                                                         |
| **Sheets**                 | Delete Sheet                       | Description coming soon...                                                                                                                                                 |
| **Sheets**                 | Update Sheet                       | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **Sheets**                 | Create Sheet                       | New Sheet will be added to the object                                                                                                                                      |
| **Sites**                  | List Sites                         | Fetches lists of portal sites with optional filters. See notes on individual parameters below                                                                              |
| **Sites**                  | Create Site                        | New site will be added to the portal                                                                                                                                       |
| **Sites**                  | Get Site                           | This method fetches a single site resource. It is the canonical URI for any site resource provided by the API                                                              |
| **Sites**                  | Delete Site                        | Description coming soon...                                                                                                                                                 |
| **Sites**                  | Update Site                        | Updates specific fields on an entity (RFC 7396)                                                                                                                            |
| **System**                 | List Companies Main Contacts       | Fetches lists of portal main contacts with optional filters. See notes on individual parameters below                                                                      |
| **System**                 | List Users                         | Fetches lists of portal users                                                                                                                                              |
| **System**                 | List Countries                     | Fetches lists of countries                                                                                                                                                 |
| **System**                 | List Security Groups               | Fetches lists of portal security groups                                                                                                                                    |
| **Templates**              | List Templates                     | Fetches lists of portal templates with values                                                                                                                              |
| **Templates**              | Update Field For ID Field          | Updates specific field on an entity's template                                                                                                                             |
