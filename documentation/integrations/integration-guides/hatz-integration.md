# Hatz integration

{% hint style="info" %}
&#x20;If you’re new to integrations in Rewst, read through our introductory integration documentation [here](https://docs.rewst.help/documentation/integrations).
{% endhint %}

## What does the Hatz integration do?

Our HatzAI integration enables you to build, deploy, and manage secure AI agents and workflows across your organization. The integration provides OpenAI-compatible chat completions, App Builder workflows, and file management.&#x20;

## Set up the Hatz integration

### Set up steps in Hatz

1. Log in to the [Hatz Admin Dashboard](https://admin.hatz.ai/login).
2. Navigate to the **Workspace** tab.
3. Click **API Keys**.
4. Enter the name `Rewst` into the field.
5. Click **Generate API Key**.

<figure><img src="../../../.gitbook/assets/Screenshot 2026-03-23 at 12.53.11 PM.png" alt=""><figcaption></figcaption></figure>

6. Copy the API key value and store it somewhere secure. You'll need this information for further steps in Rewst.

### Set up steps in Rewst

Follow the below steps to configure a new integration:

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for `Hatz` in the integrations page.
3. Click on the integration tile to launch the configuration setup page.\
   \
   ![](<../../../.gitbook/assets/Screenshot 2026-03-23 at 12.35.24 PM.png>)<br>
4. Enter the information copied from Hatz into the **API Key** field.
5. Click **Save Configuration**.&#x20;
6. Rewst will do a quick validation of your input. Once completed, you'll see a new section beneath the configuration form for[ organization mapping](https://docs.rewst.help/documentation/integrations#what-is-organization-mapping). Complete your mapping as desired.&#x20;

{% hint style="success" %}
Got an idea for a new Integration? Rewst is constantly adding new integrations to our integrations page. Submit your idea or upvote existing ideas here in our [Canny feedback collector](https://rewst.canny.io/integrations).
{% endhint %}

## Actions and endpoints

{% hint style="info" %}
For more on how actions work in Rewst, check out our [introductory actions documentation here](https://docs.rewst.help/documentation/workflows/actions-in-rewst).&#x20;
{% endhint %}

View Hatz AI's own API documentation [here](https://api-docs.hatz.ai/).&#x20;

| Category         | Action                 | Description                                                                                                    |
| ---------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------- |
| Apps             | Query App              | Executes a Hatz AI app with provided inputs and returns the result.                                            |
| Apps             | Get App                | Retrieves details for a specific app including its configuration, user inputs, and prompt sections.            |
| Apps             | List Apps              | Retrieves a list of all apps/workflows created in the Hatz AI App Builder                                      |
| Chat Completions | Create Chat Completion | Sends messages to an AI model and receives a response.                                                         |
| Files            | Upload File            | Uploads a file to Hatz AI for use in chat completions or apps. Returns a file UUID. Maximum file size is 30MB. |
| Files            | List Files             | Retrieves a list of all files uploaded to Hatz AI.                                                             |
| Generic Request  | Hatz AI API Request    | Generic action for making authenticated requests against the Hatz AI API.                                      |
| Models           | List Models            | Retrieves a list of all available AI models on the Hatz AI platform.                                           |
