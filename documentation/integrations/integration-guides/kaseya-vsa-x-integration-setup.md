# Kaseya VSA X integration

{% hint style="info" %}
&#x20;If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the Kaseya VSA X integration do?

Our Kaseya VSA X integration enables automation of remote monitoring and management. Use the Kaseya VSA X API within Rewst worfkflows to automate tasks such as obtaining asses inventory, executing commands, and running procedures on endpoints.&#x20;

## Set up the Kaseya VSA X integration

### Set up steps in Kaseya

1. Log in to the Kaseya VSA X Admin Console. You will need to have administrator privileges to create API tokens.
2. Navigate **Administration > Server Admin > Overview**. \
   \
   <img src="../../../.gitbook/assets/Screenshot 2025-05-05 at 3.59.33 PM.png" alt="" data-size="original">
3. Copy the **Name** under the **Server Information** submenu.
4. Navigate to **Administration > Configuration > API Access**.
5. If prompted, re-enter your account password.
6. Click **Create Token**.
7. Name your token. Enter a descriptive name for your token in the Create token dialog box. This will help you to identify the token later. Don't set an expiration date for the token.
8. Click **Next**.
9. If you want to limit the ip address access for the API token, follow the directions for doing so here in Rewst's [security policy](../../../security/security-policy.md) listing of domains. Be sure to align this with whichever region of Rewst you are using.&#x20;
10. Configure your token permissions to have access to your chosen organizations and API permissions in which you want to have access to in Rewst.
11. Click **Create Token**.
12. Copy the value for the **Token ID** and **Token Secret**. Store these somewhere secure, as you won't be able to view them again once you move away from this page. You'll need both for further steps in Rewst.

### Set up steps in Rewst

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `Kaseya VSA X` in the integrations page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2025-05-05 at 3.48.06 PM.png>)
3. Click on the integration tile to launch the configuration setup page.
4. Under **Parameters**, enter the information copied from Kaseya into the relevant fields:
   1. **Hostname**: Kaseya VSA X server hostname, e.g. `example.kaseyalab.com`
   2. **Token ID**
   3. **Token Secret**
5. Click **Save Configuration**.
6. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.&#x20;

### Migrate from Kaseya VSA integration to Kaseya VSA X

1. Configure the new Kaseya VSA X integration from the instructions above.
2. Update the `default_rmm` organization variable to be `kaseya_vsa_x`&#x20;

&#x20;       OR&#x20;

&#x20;       Re-run the config orgs form to choose Kaseya VSA X as their default RMM.

3. Create a script called `Run Powershell (Rewst)` with the inputs `post_url` and `script_url`:

<figure><img src="../../../.gitbook/assets/Screenshot 2024-09-09 at 2.44.05 PM.png" alt=""><figcaption></figcaption></figure>

and the contents:

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$wc = New-Object System.Net.WebClient
$wc.Encoding = [System.Text.Encoding]::UTF8
$commands = ($wc.DownloadString("$script_url"))
iex $commands
```

Optionally, reduce API calls to Kaseya by setting an org var called `kaseya_vsa_10_scriptid` with the GUID value of the above script.

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Use custom PowerShell scripts with your RMM integration

If you're writing custom PowerShell scripts to use and run with your RMM integration, you'll need to manually add webhook calls. Any custom script will time out if used without first adding the webhook calls. The use of standard built-in Rewst scripts with your RMM does not require you to add the calls.

The webhook calls everyone doing this custom scripting should use will always be as follows.

```
### Send all the data back to RewstyRewst ###


$postData = $PS_Results | ConvertTo-Json
Invoke-RestMethod -Method 'Post' -Uri $post_url -Body $postData -ContentType 'application/json; 
charset=utf-8'
```

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

| Category            | Action                                 | Description                                                                   |
| ------------------- | -------------------------------------- | ----------------------------------------------------------------------------- |
| **Device**          | List Devices                           | Returns a list of devices.                                                    |
| **Device**          | Get Device by ID                       | Returns the device details.                                                   |
| **Generic Request** | Kaseya VSA X API Request               | Generic action for making authenticated requests against the Kaseya VSA X API |
| **Script**          | List All Automation Scripts            | Returns a list of automation scripts.                                         |
| **Script**          | Get a Specific Automation Script by ID | Returns the automation script details.                                        |
| **Script**          | Run Automation Script                  | Runs a specific automation script                                             |
