# Ubiquiti integration

{% hint style="info" %}
If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the Ubiquiti integration do?

Our Ubiquit integration enables the automation of finance processes by seamlessly connecting Xero and Rewst. Automate workflows for managing client financial data, invoices, and more.

## Set up the Ubiquiti integration

### Set up steps in Ubiquiti

1. Open [UniFi Site Manager](https://unifi.ui.com/) and log in to your account.
2. Navigate to the **API** section in the Site Manager.
3. Click **Create a New API Key**.
4. Enter `Rewst` into the **Name** field.
5. Choose **Never Expires** from the **Expiration** drop-down selector.
6. Choose **Read Only** permissions. The Ubiquiti API is currently read-only. No write endpoints exist.
7. Click **Create.**
8. Note that the key value will only be shown once. Copy the generated key and store it somewhere secure. You'll need this information for further steps in Rewst.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `Ubiquiti` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-03-23 at 12.59.36 PM.png>)
3. Click on the integration tile to launch the configuration setup page.
4. Enter the copied API key value into the **API Key** field.
5. Click **Save Configuration**.
6. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.&#x20;

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

Ubiquiti's own API documentation can be found [here](https://developer.ui.com/site-manager/v1.0.0/gettingstarted).&#x20;

| Category        | Action                   | Description                                                                                                    |
| --------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------- |
| Devices         | List Devices             | Retrieves a list of UniFi devices managed by hosts where the UI account is owner or super admin                |
| Generic Request | Ubiquiti API Request     | Generic action for making authenticated requests against the Ubiquiti Site Manager API                         |
| Hosts           | Get Host by ID           | Retrieves detailed information about a specific host                                                           |
| Hosts           | List Hosts               | Retrieves a list of all hosts (UniFi consoles/controllers) associated with the UI account                      |
| Isp Metrics     | Get ISP Metrics          | Retrieves ISP metrics data for all sites linked to the API key                                                 |
| Isp Metrics     | Query ISP Metrics        | Query ISP metrics with specific site filters and time ranges                                                   |
| Sd Wan          | Get SD-WAN Config Status | Retrieves the deployment status of a specific SD-WAN configuration                                             |
| Sd Wan          | List SD-WAN Configs      | Retrieves a list of SD-WAN configurations                                                                      |
| Sd Wan          | Get SD-WAN Config by ID  | Retrieves detailed information about a specific SD-WAN configuration                                           |
| Sites           | List Sites               | Retrieves a list of all sites from hosts running the UniFi Network application, associated with the UI account |
