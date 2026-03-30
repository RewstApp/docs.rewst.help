# ConnectWise ASIO integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## **What does the ConnectWise ASIO integration do?**

The ConnectWise ASIO platform empowers Managed Service Providers (MSPs) to streamline their operations by consolidating the management of diverse tools and products within a single, unified interface.

## Set up the **ConnectWise ASIO** integration

### Set up steps in **ConnectWise ASIO**

#### **Generate the Client ID**

1. Log in to [https://developer.connectwise.com](https://developer.connectwise.com).
2. Click the **Client ID** tab.
3. Click the **Create New Integration** under the **Your clientId(s)** section.
4. Fill out the following fields, select the applicable radio button, and select the applicable drop-down list item:
   * **Integration Name**
   * **Description**
   * **Integration Type** - Select either **Public** or **Private**
     * Public is meant to be used with multiple ConnectWise instances that aren't yours
     * Private is meant to be used only by you and your instances
   * **Technical Contact Email**
   * **Product** - Select the applicable product

#### Copy the needed information for Rewst

1. Go to [https://home.connectwise.com/](https://home.connectwise.com/).
2. Hover over **ASIO Platform** under **My ConnectWise Hub**. Click the **Launch** button that appears. This will launch ASIO in a new tab of your browser.
3. Navigate to **Integrations** **> API Access** in the left side panel.
4. Click **Generate API Access +** .
5. Enter Rewst into the **API Key Name** field.
6. Enter your desired explanation into the **Description** field.
7. Use the **Scopes** drop-down to select the following scopes that will be attached to the API Key. This list is what Rewst recommends for the integration. If desired, you may add additional scopes or remove scopes. The integration will require at least one scope to work. Note that any scoping that deviates from our recommended list may create unknown errors or dependencies. Rewst support is not responsible for assisting you with custom scoping.
   1. platform.companies.read&#x20;
   2. platform.sites.read&#x20;
   3. platform.asset.read&#x20;
   4. platform.custom\_fields\_definitions.read&#x20;
   5. platform.custom\_fields\_values.read&#x20;
   6. platform.custom\_fields\_values.write&#x20;
   7. platform.patching.read&#x20;
   8. platform.automation.read&#x20;
   9. platform.automation.create
   10. platform.devices.read
8. Check off the **Consent** box.
9. Click **Generate API Access**.
10. The information that appears on your screen can only be viewed this one time and will disappear after you leave the screen. Copy both the **Client ID** and **API Key** and store it some place secure. You'll need it for additional steps in Rewst.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-01-14 at 4.13.23 PM.png" alt="" width="375"><figcaption></figcaption></figure>

### Set up steps in Rewst

{% hint style="warning" %}
If editing an existing setup of the integration, note that previously created access tokens are cached with a lifetime of one hour. Wait an hour before reauthorizing.&#x20;
{% endhint %}

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `ConnectWise ASIO` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/image (3) (5).png>)
3. Click on the integration tile to launch the configuration setup page.
4. Enter the following details copied from ConnectWise ASIO into the relevant fields under the **Parameters** section:
   * **API Key -** This is the OAuth2 API Key for ConnectWise API access
   * **Client ID** - Also known as the client key, this is the OAuth2 Client ID for ConnectWise API access
5. The **Scopes** field will automatically populate with all the recommended scopes for Rewst integration. If you chose custom scoping in ASIO, you'll need to delete or add those scopes accordingly. Click <img src="../../../.gitbook/assets/Screenshot 2026-02-16 at 10.10.29 AM.png" alt="" data-size="line"> to expand the drop-down selector of total available scopes.

<figure><img src="../../../.gitbook/assets/image (84) (1).png" alt="" width="375"><figcaption></figcaption></figure>

3. Click **Save Configuration**.
4. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.

### Use PowerShell with ConnectWise ASIO

When you run PowerShell tasks in a workflow, Rewst will automatically retrieve the needed ASIO ID. No action is required on your part.

### Future additional functionality

In future, when Rewst adds functionality to our ConnectWise ASIO integration, additional scopes may need to be added manually to your integration's configuration to take advantage of that functionality. The order of operations for any scope update is to first add or remove a scope in ConnectWise ASIO, then add or remove a scope to the scopes list in the configuration setup page in Rewst. If you do not add new scopes, your integration will still work as it had previously, but won't contain the new added functionality.

{% hint style="success" %}
Got an idea for a new integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

| Category            | Action                       | Description                                                                                         |
| ------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------- |
| **Companies**       | List Companies               | Gets a list of all companies (clients) in ConnectWise ASIO                                          |
| **Endpoints**       | List Computers               | Gets a list of all endpoints (devices) across all companies                                         |
| **Endpoints**       | Get Computer Devices         | Gets detailed information about a specific computer including hardware, software, and configuration |
| **Endpoints**       | List Computer Drives         | List drives for a specific computer                                                                 |
| **Endpoints**       | Get Computer Services        | List a computer's services                                                                          |
| **Device Groups**   | List Groups                  | Gets a list of all device groups (both static and dynamic)                                          |
| **Custom Fields**   | List Extra Data Field(s)     | Gets a list of all custom field definitions across all entity types                                 |
| **Custom Fields**   | Get Computer EDFs            | List extra data fields from the specified computer                                                  |
| **Custom Fields**   | Update Extra Data Field      | Updates custom field values for a specific endpoint                                                 |
| **Custom Fields**   | Get Client EDFs              | List extra data fields from the specified client                                                    |
| **Custom Fields**   | Get Location EDFs            | List extra data fields from the specified location                                                  |
| **Custom Fields**   | Update Location EDFs         | Updates extra data fields for a specific location                                                   |
| **Custom Fields**   | Update Client EDFs           | Updates extra data fields for a specific client                                                     |
| **Automation**      | List Shell Scripts           | Gets a list of shell scripts                                                                        |
| **Automation**      | List Scripts                 | Gets a list of scripts                                                                              |
| **Automation**      | List Tasks                   | Gets a list of tasks                                                                                |
| **Automation**      | Schedule Task                | Schedule a task on target endpoints                                                                 |
| **Patching**        | Get Computer Patching Stats  | Retrieve an individual computer's patching statistics                                               |
| **Generic Request** | ConnectWise ASIO API Request | Generic action for making authenticated requests against the ConnectWise ASIO API                   |
