# ServiceNow integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the ServiceNow integration do?

Our ServiceNow integration enables the automation of IT service management and business processes. Use the ServiceNow API within Rewst workflows to create and update incidents, manage change requests, retrieve and modify user information, and streamline approval processes.

## Set up the ServiceNow integration

Before you complete integration setup, you'll need to obtain a developer instance from ServiceNow. This is a request process documented on their own website [here](https://developer.servicenow.com/dev.do#!/guides/yokohama/now-platform/devsite_account_guide_yokohama_developer-site-account-guide/DAG_DevSiteAcctGuide). The steps listed below won't work until you have this completed. If you already had a [developer or partner instance granted at the time of your ServiceNow onboarding](https://developer.servicenow.com/dev.do#!/guides/yokohama/developer-program/dev-program/dev-program-guide), this should be sufficient. Actions taken within the developer instance won't affect what's in your customer or partner instances

### Set up steps in ServiceNow

1. Log in to your ServiceNow account.
2.  Click on the **Developer Program** tile under the **My Apps** menu.<br>

    <figure><img src="../../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>
3. Click **Start Building** if prompted. This will appear if this is your first time logging in to the Developer Portal.
4. Find the hostname for your ServiceNow instance. This would be the part of the URL that appears before the first / . For example, in a URL that reads as `dev12345.service-now.com/abc123/4567` , the host name would be `dev12345.service-now.com` .
5. Copy the hostname someplace secure. You'll need this for further steps in Rewst.
6. Navigate to **All > User Administration > Users**.
7.  Click **New** to add a new user.<br>

    <figure><img src="../../../.gitbook/assets/image (75).png" alt=""><figcaption><p>The new user set up page</p></figcaption></figure>
8. Enter `RewstAPI` into the **User ID** field. Save this information with your hostname. You'll need it for further steps in Rewst.&#x20;
9. Check the **Active** box.&#x20;
10. Click **Submit**.
11. Click on the new user that appears in the total user table to re-open its record.&#x20;
12. Click **Set Password**.
13. Click **Generate** to create a new secure password. Copy this password and save the information with your hostname and username.&#x20;
14. Click **Save Password**.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `ServiceNow` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-05-05 at 11.14.58 AM.png>)
3. Click on the integration tile to launch the configuration setup page.
4. Under **Parameters**, enter the information you copied out of ServiceNow into the relevant fields:
   1. **Hostname**
   2. **Password**
   3. **User Name**
5. Click **Save Configuration**.
6. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.&#x20;

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## ServiceNow Domain Separation in Rewst&#x20;

{% hint style="info" %}
See ServiceNow's own documentation on Domain Separation [here](https://support.servicenow.com/kb?id=kb_article_view\&sysparm_article=KB0715934).
{% endhint %}

_Domain Separation_ in ServiceNow is a way to separate data, processes, and administrative tasks into logical groupings called domains, so that users in one domain cannot see or interact with data in another domain unless explicitly permitted. This shouldn't be confused with [multi-instance integration](../multi-instance-integration/), which is a way of setting up integrations that is specific to Rewst. While the Rewst integration was not explicitly designed for MSPs who use Domain Separation, they can still use Rewst with the ServiceNow integration. Any call or action that can be initiated from ServiceNow can be received by Rewst.&#x20;

Note that Domain Separated ServiceNow users will need to [clone and customize](../../../prebuilt-automations/crates/#synced-versus-unsynced-crates) any related Rewst Crates to successfully use them. When using Rewst tasks for ServiceNow, they can be scoped at either the global - parent - level or the domain - child - level. In some tasks, you can use the **No Domain** field to add a flag that indicates whether the record search should be restricted to only domains for which the logged-in user is configured.



<figure><img src="../../../.gitbook/assets/image (335).png" alt=""><figcaption><p>An example of a task with the <strong>No Domain</strong> field</p></figcaption></figure>

## Triggers for ServiceNow integration

| Trigger type name | Type    | Description                                                     |
| ----------------- | ------- | --------------------------------------------------------------- |
| New Table Record  | Polling | Trigger which returns an object containing the database records |

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

These endpoints requires the following plugins:

* Customer Service plugin (`com.sn_customerservice`) + `csm_ws_integration` role and is provided within the now namespace
* Order Management for Customer Service Management (`app-csm-order-mgmt`) + `sn_csm_order_mgmt` role
* Order Management for Telecommunications (`sn_ind_tmt_orm`) - Optional
* Telecommunications Assurance Workflows
* Customer Service (`com.sn_customerservice`)
* Customer Service Install Base Management (`com.snc.install_base`)



| category            | action                                         | description                                                                                                                                                                            |
| ------------------- | ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Account             | List Accounts                                  | Retrieves a specified set of Customer Service Management (CSM) accounts.                                                                                                               |
| Account             | Get Account by ID                              | Retrieves the specified Customer Service Management (CSM) account.                                                                                                                     |
| Consumer            | List Consumers                                 | Retrieves a specified set of Customer Service Management (CSM) consumer records.                                                                                                       |
| Consumer            | Get Consumer by ID                             | Retrieves the specified Customer Service Management (CSM) consumer record.                                                                                                             |
| Consumer            | Create New Consumer                            | Creates a new Customer Service Management (CSM) consumer.                                                                                                                              |
| Contact             | Create New Contact                             | Creates a new Customer Service Management (CSM) contact.                                                                                                                               |
| Contact             | Get Contact by ID                              | Retrieves the specified Customer Service Management (CSM) contact.                                                                                                                     |
| Contact             | List Contacts                                  | Retrieves a specified set of Customer Service Management (CSM) contacts.                                                                                                               |
| Generic Request     | Generic API Request                            | Generic action for making authenticated requests against the ServiceNow API                                                                                                            |
| Order               | List Product Order                             | Retrieves all product orders                                                                                                                                                           |
| Order               | Create New Order                               | Creates a new order with line items and characteristics.                                                                                                                               |
| Order               | Get Service Order                              | Retrieves specific service orders                                                                                                                                                      |
| Order               | Update Service Order                           | Update specific service order                                                                                                                                                          |
| Order               | Create Service Order                           | create new service order                                                                                                                                                               |
| Order               | Update Customer Order                          | Updates the specified customer order.                                                                                                                                                  |
| Order               | Cancel Customer Order                          | Cancel the specified customer order.                                                                                                                                                   |
| Order               | List Product Order by ID                       | Retrieves the specified product order.                                                                                                                                                 |
| Order               | List Service Orders                            | Retrieves all service orders                                                                                                                                                           |
| Order               | Get Order by ID                                | Retrieves complete order details by specifying the sys\_id or order number.                                                                                                            |
| Order               | Cancel Service Order                           | Cancel the specified service order.                                                                                                                                                    |
| Order               | Create Customer Order                          | Creates the specified customer order.                                                                                                                                                  |
| Service Catalog     | Display Value                                  | Returns the display value of the specified variable.                                                                                                                                   |
| Service Catalog     | Submit Order                                   | Checks out the user cart, based on the current check-out type (one-step or two-step ).                                                                                                 |
| Service Catalog     | Process Checkout                               | Retrieves and processes the checkout for the current cart based on whether the two-step checkout process is enabled.                                                                   |
| Service Catalog     | List Catalogs                                  | Retrieves a list of catalogs to which the user has access based on the passed in parameters.                                                                                           |
| Service Catalog     | Get Item Detail from Wish List                 | Retrieves the details of the specified item stored in the wish list cart.                                                                                                              |
| Service Catalog     | Submit Record Producer                         | Creates a record and returns the Table API relative path and redirect URL to access the created record.                                                                                |
| Service Catalog     | List Items Needed by Order Guide               | Retrieves a list of items based on the needs described for an order guide.                                                                                                             |
| Service Catalog     | Delete Cart                                    | Deletes a specified cart and the contents of the cart.                                                                                                                                 |
| Service Catalog     | List Wish List Items - Current User            | Retrieves the list of items in the logged in user's wish list.                                                                                                                         |
| Service Catalog     | Get Catalog Item by ID                         | Retrieves a specified catalog item.                                                                                                                                                    |
| Service Catalog     | Add Item to Wish List                          | Adds the specified item to the wish list cart.                                                                                                                                         |
| Service Catalog     | Delete Item from Cart                          | Deletes the specified item from the current cart.                                                                                                                                      |
| Service Catalog     | Get Catalog Information                        | Retrieves the available information for a specified catalog.                                                                                                                           |
| Service Catalog     | List Catalog Items                             | Retrieves a list of catalog items based on the specified parameters.                                                                                                                   |
| Service Catalog     | Update Item in Cart                            | Updates the specified item in the logged in user's cart.                                                                                                                               |
| Service Catalog     | Verify User Acquisition Rights to Catalog Item | Verifies whether the specified delegated user has acquisition rights to the specified service catalog item.                                                                            |
| Service Catalog     | Add Item to Cart                               | Adds the specified item to the cart of the current user.                                                                                                                               |
| Service Catalog     | List Users with sUndelegated Item Request      | Returns a list of users whose request for the specified item cannot be delegated (requested by another user.) Can call before Add to Cart or Order Now                                 |
| Service Catalog     | Order Item                                     | Orders the specified catalog item.                                                                                                                                                     |
| Service Catalog     | Get Shipping Address by User ID                | Retrieves the shipping address of the specified user based on the glide.sc.req\_for.roles property and the default behavior configured in the glide.sc.req\_for.roles.defaultproperty. |
| Service Catalog     | Get Contents for Checkout                      | Retrieves an array of contents requested for checkout.                                                                                                                                 |
| Service Catalog     | List Categories by Catalog                     | Retrieves the list of available categories for the specified catalog.                                                                                                                  |
| Service Catalog     | Get Cart\_Content                              | Retrieves the details of the items within the logged in user's cart.                                                                                                                   |
| Service Catalog     | Get Category Information                       | Retrieves the available information for a specified category.                                                                                                                          |
| Table               | List Table Records                             | Retrieves multiple records for the specified table.                                                                                                                                    |
| Table               | List Database Tables                           | Retrieves the list of tables for the ServiceNow instance.                                                                                                                              |
| Trouble Ticket Open | Create Trouble Ticket                          | Creates a record in the Case \[sn\_customerservice\_case] or Incident \[incident] table.                                                                                               |
| Trouble Ticket Open | List All Trouble Tickets                       | Retrieves a list of all trouble ticket records from the Case \[sn\_customerservice\_case] and Incident \[incident] tables.                                                             |
| Trouble Ticket Open | Update Trouble Ticket by ID                    | Updates a specified record in the Case \[sn\_customerservice\_case] or Incident \[incident] table.                                                                                     |
| Trouble Ticket Open | Get Trouble Ticket by ID                       | Retrieves a specified record from the Case \[sn\_customerservice\_case] or Incident \[incident] table.                                                                                 |
| Uncategorized       | Get Catalog Items List                         | Retrieves a list of catalog items based on the specified parameters.                                                                                                                   |
| Uncategorized       | Get Contacts                                   | Retrieves a specified set of Customer Service Management (CSM) contacts.                                                                                                               |
| Uncategorized       | Get Wish List - Current User                   | Retrieves the list of items in the logged in user's wish list.                                                                                                                         |
| Uncategorized       | Get Accounts                                   | Retrieves a specified set of Customer Service Management (CSM) accounts.                                                                                                               |
| Uncategorized       | Get List of Categories by Catalog              | Retrieves the list of available categories for the specified catalog.                                                                                                                  |
| Uncategorized       | Get Consumers                                  | Retrieves a specified set of Customer Service Management (CSM) consumer records.                                                                                                       |
| Uncategorized       | Get All Trouble Tickets                        | Retrieves a list of all trouble ticket records from the Case \[sn\_customerservice\_case] and Incident \[incident] tables.                                                             |
| Uncategorized       | Get Users Undelegated Item Request             | Returns a list of users whose request for the specified item cannot be delegated (requested by another user.) Can call before Add to Cart or Order Now                                 |
| Uncategorized       | Verify User Acquisition Rights to Catalog Item | Verifies whether the specified delegated user has acquisition rights to the specified service catalog item.                                                                            |
| Uncategorized       | Add Item to Wish List                          | Adds the specified item to the wish list cart.                                                                                                                                         |
| Uncategorized       | Get Cart                                       | Retrieves the details of the items within the logged in user's cart.                                                                                                                   |
| Uncategorized       | Get List of Catalogs                           | Retrieves a list of catalogs to which the user has access based on the passed in parameters.                                                                                           |
| Uncategorized       | Get Items by Order Guide                       | Retrieves a list of items based on the needs described for an order guide.                                                                                                             |
