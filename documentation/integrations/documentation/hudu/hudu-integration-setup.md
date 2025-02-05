# Hudu integration setup

{% hint style="success" %}
**This Integration supports multiple instances**

[Check out our instructions to set up multiple instances here](../../general/multi-instance-integration/multi-instance-integration-setup.md).
{% endhint %}

## What does the Hudu integration do?

Rewst's Hudu integration enables the automation of documentation management. Use the Hudu API within Rewst workflows to perform actions such as managing and documenting assets, websites, passwords, and procedures.

## Set up the API account in Hudu

Before configuring the Rewst integration, you must generate an API user.

1. Log in to your Hudu instance.
2. Click on the **Admin** tab in the top menu.
3.  Scroll down and click **API Keys** under the **Account Administration** menu.\


    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-02-04 at 2.07.19 PM.png" alt=""><figcaption></figcaption></figure>
4. Click the **+ New API Key** button at the upper right of the page.
5.  Enter the following:



    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-02-04 at 2.10.32 PM.png" alt=""><figcaption></figcaption></figure>

    1. **Name:** Rewst
    2. **Allowed IP Addresses:** 3.139.170.31
    3. Check the box for **Can access passwords?**
    4. Check the box for **Can perform destructive actions?**
    5. Check the box for **Can perform export actions?**
6. Click **Create New Key**.
7. Copy and save the API key that is generated and listed at the top of the page under **New API Key**.

## Set up steps in Rewst

1. Navigate to **Configuration > Integrations** in the left side menu of your Rewst platform.
2. In the Integrations page, search for the Hudu integration.\
   ![](<../../../../.gitbook/assets/Screenshot 2025-02-04 at 2.15.09 PM.png>)
3. Click on the integration tile to begin the installation process.
4. Enter the name of your choice for your integration.
5. Enter description if desired.
6. Enter your copied API key from your Hudu Instance.
7. Add your Hudu Instance hostname  in the **Hudu URL** field: for example,  yourinstance.huducloud.com
8.  Click **Save Configuration**.\


    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-02-04 at 2.19.52 PM.png" alt=""><figcaption></figcaption></figure>

Rewst will perform a quick validation of the information. Beneath that integration authentication section you'll see the following options:

1. **Suggest Values**: This option will attempt to generate mappings between Rewst organizations and child organization in this integration.
2. **Refresh Options**: This will re-read the potential mapping options - both organizations and companies in IT Glue.
3. **Save Mappings**: This will apply mapping configuration changes.

