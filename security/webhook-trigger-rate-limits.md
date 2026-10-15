# Webhook trigger rate limits

{% hint style="warning" %}
These rate limits apply only to the Rewst Classic product, not our new Rewst product. For rate limiting info for new Rewst, see our guidance [here](https://docs.rewst.help/rewst-documentation/security/organization-rate-limits).&#x20;
{% endhint %}

{% hint style="info" %}
_Rate limiting_ is a technique to control the number of requests a user or application can make to a service within a specific time frame. It's used to prevent system overload, ensure fair usage, and protect against attacks like DDoS or scraping by temporarily slowing or rejecting requests that exceed predefined limits.

Rewst will enable rate limits for our webhook triggers on February 18, 2026. Existing customers should see the section [Existing customer rate limit transition](webhook-trigger-rate-limits.md#existing-customer-rate-limit-transition) for instructions on how to prepare.
{% endhint %}

To ensure platform reliability and consistent performance for the entire platform, Rewst applies rate limits to inbound webhook triggers.

{% hint style="info" %}
Current limits per trigger

* 50 requests per second
* 1000 requests per minute

These limits apply individually to each webhook trigger, not to your organization as a whole. Our integrations operate well within these thresholds under normal conditions.

The rate limit occurs at ingest rather than after trigger criteria are considered.
{% endhint %}

## Common causes of rate limit errors

* Misconfigured integrations sending duplicate events
* Bulk operations triggering large volumes of webhooks simultaneously
* Retry storms from upstream services

## Response when limit is exceeded

If your webhook traffic exceeds our limits, Rewst will respond with an HTTP `429 Too Many Requests` status code. This is a [standard response](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status) that signals the sending service to [slow down and retry](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Retry-After), and is displayed in the header of the webhook response.

As webhook requests originate from external platforms, Rewst can't retry the request on your behalf. The event is lost once it's rejected, unless the external platform is configured to retry on 429 responses. Most well-designed webhook senders will automatically back-off and retry when they receive a 429 response. WHRL However, note that Rewst has built integrations with MSP-requested tools, and not all tools have 429 responses built in yet.

### Example response

Below is an example of the 429 response Rewst sends back to the involved partner app when your trigger is rate limited. Use this table to reference its meaning.

```
{
  "data": "",
  "status_code": 429,
  "headers": {
    "Date": "Fri, 23 Jan 2026 06:01:50 GMT",
    "Content-Length": "0",
    "Connection": "keep-alive",
    "x-envoy-ratelimited": "true",
    "x-ratelimit-remaining": "0",
    "x-ratelimit-reset": "10",
    "Retry-After": "10",
    "strict-transport-security": "max-age=15552000; includeSubDomains",
    "Server": "istio-envoy"
  },
  "cookies": {}
}
```

| Item Key                                          | Example Value | Meaning                                            |
| ------------------------------------------------- | ------------- | -------------------------------------------------- |
| HTTP status code - `status`                       | `429`         | Too Many Requests — rate limit exceeded.           |
| Envoy rate limited - `x-envoy-ratelimited`        | `true`        | Request was blocked by Envoy due to rate limiting. |
| Retry after - `retry-after` / `x-ratelimit-reset` | `10`          | Wait 10 seconds before retrying the request.       |

## How to resolve and prevent rate limit issues

{% hint style="warning" %}
Naive immediate retries will cause loops and continued rate limiting.
{% endhint %}

* Review your integration configuration to ensure that events aren't being sent multiple times.
* Verify that upstream services are correctly handling 429 responses and implementing back-off.
* If you're performing bulk operations, consider spacing them out over time.
* Add delays or exponential back-off before retrying.
* Filter events before sending requests. Configure the source system to only emit webhook events that are actually needed: limit event types, scopes, objects, environments, etc.
* If supported, batch or consolidate events. Prefer sending fewer webhook requests that contain multiple changes or events, or use built-in batching aggregation options on the source platform to reduce request volume.
* Contact [Rewst support](../support-and-community/roc-support/) if you need further guidance on how to prevent rate limiting.

## Existing customer rate limit transition

Rewst recommends evaluating your applications that send automated HTTP requests to Rewst before the transition date to ensure your webhook triggers are not exceeding the fair use limits put in place.

### Supplemental partner documentation

Below are links to related documentation from some of the apps Rewst integrates with, which may help you in ensuring that your webhook triggers are within limit. Partner documentation may require logging in to that partner app to view content.

[Receive change notifications through webhooks – Microsoft Graph](https://learn.microsoft.com/en-us/graph/change-notifications-delivery-webhooks): This is Microsoft’s direct documentation of webhook delivery semantics for Graph.

[Webhooks error handling - Autotask Official Documentation](https://www.autotask.net/help/developerhelp/Content/APIs/Webhooks/Webhooks_Error_Handling.htm): This contains an authoritative description of Autotask webhook retry behavior.

[ConnectWise developer guide](https://developer.connectwise.com/Special:Userlogin?returntotitle=Products%2FConnectWise_PSA%2FDeveloper_Guide#tab=login): This contains ConnectWise's documentation on how their product handles retries.

## Webhook integration triggers reference table

| integration\_name                 | trigger\_name                                     | description                                                                                                                                                                                                                            |
| --------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Autotask PSA                      | Company Webhook                                   | Creating a webhook enables you to subscribe to notifications for events that take place in Autotask.                                                                                                                                   |
| Autotask PSA                      | Configuration Item Webhook                        | Creating a webhook enables you to subscribe to notifications for events that take place in Autotask.                                                                                                                                   |
| Autotask PSA                      | Contact Webhook                                   | Creating a webhook enables you to subscribe to notifications for events that take place in Autotask.                                                                                                                                   |
| Autotask PSA                      | Ticket Note Webhook                               | Creating a webhook enables you to subscribe to notifications for events that take place in Autotask.                                                                                                                                   |
| Autotask PSA                      | Ticket Webhook                                    | Creating a webhook enables you to subscribe to notifications for events that take place in Autotask.                                                                                                                                   |
| ConnectWise PSA                   | Activity Record Saved                             | Receive notifications when an Activity record is saved in CW Manage                                                                                                                                                                    |
| ConnectWise PSA                   | Agreement Record Saved                            | Receive notifications when an Agreement record is saved in CW Manage                                                                                                                                                                   |
| ConnectWise PSA                   | Company Record Saved                              | Receive notifications when a Company record is saved in CW Manage                                                                                                                                                                      |
| ConnectWise PSA                   | Configuration Record Saved                        | Receive notifications when a Configuration record is saved in CW Manage                                                                                                                                                                |
| ConnectWise PSA                   | Contact Record Saved                              | Receive notifications when a Contact record is saved in CW Manage                                                                                                                                                                      |
| ConnectWise PSA                   | Expense Record Saved                              | Receive notifications when an Expense record is saved in CW Manage                                                                                                                                                                     |
| ConnectWise PSA                   | Invoice Record Saved                              | Receive notifications when an Invoice record is saved in CW Manage                                                                                                                                                                     |
| ConnectWise PSA                   | Opportunity Record Saved                          | Receive notifications when an Opportunity record is saved in CW Manage                                                                                                                                                                 |
| ConnectWise PSA                   | Product Catalog Record Saved                      | Receive notifications when a Product Catalog record is saved in CW Manage                                                                                                                                                              |
| ConnectWise PSA                   | Project Record Saved                              | Receive notifications when a Project record is saved in CW Manage                                                                                                                                                                      |
| ConnectWise PSA                   | Purchase Order Record Saved                       | Receive notifications when a Purchase Order record is saved in CW Manage                                                                                                                                                               |
| ConnectWise PSA                   | Schedule Entry Record Saved                       | Receive notifications when a Schedule Entry record is saved in CW Manage                                                                                                                                                               |
| ConnectWise PSA                   | Ticket Record Saved                               | Receive notifications when a Ticket record is saved in CW Manage                                                                                                                                                                       |
| ConnectWise PSA                   | Time Entry Record Saved                           | Receive notifications when a Time Entry record is saved in CW Manage                                                                                                                                                                   |
| Core                              | Form Submission                                   |                                                                                                                                                                                                                                        |
| Core                              | Webhook                                           |                                                                                                                                                                                                                                        |
| Discord                           | Custom Interaction                                | Triggers a workflow for a custom interaction event. The command, modal or message component must be created first. See [Discord API docs](https://discord.com/developers/docs/interactions/application-commands) for more information. |
| Discord                           | Message Command                                   | Triggers a workflow when a specified message command is activated in a guild (server)                                                                                                                                                  |
| Discord                           | Slash Command                                     | Triggers a workflow when a specified slash command is sent to a guild (server) channel                                                                                                                                                 |
| Discord                           | User Command                                      | Triggers a workflow when a specified user command is activated in a guild (server)                                                                                                                                                     |
| HubSpot                           | object\_changed                                   | Fires on create, update, delete of a hubspot item                                                                                                                                                                                      |
| Microsoft Graph                   | Chat Message Subscription                         | Subscribe to chat messages in all chats                                                                                                                                                                                                |
| Microsoft Graph                   | Chat Message Subscription by Chat ID              | Subscribe to changes to chat messages in a specific chat                                                                                                                                                                               |
| Microsoft Graph                   | Email Message Change Subscription                 | Subscribe to changes for a user's email messages. Does not allow specifying mailbox folder.                                                                                                                                            |
| Microsoft Graph                   | Group Change Subscription                         | Subscribe to changes to all groups                                                                                                                                                                                                     |
| Microsoft Graph                   | Security Alert Subscription                       | Receive notifications when a new Security Alert is produced in Microsoft Graph                                                                                                                                                         |
| Microsoft Graph                   | Teams Message Subscription                        | Subscribe to chat messages in all channels in all teams                                                                                                                                                                                |
| Microsoft Graph                   | Teams Message Subscription by Team and Channel ID | Subscribe to changes to chat messages in a specific channel                                                                                                                                                                            |
| Microsoft Graph                   | User Change Subscription                          | Subscribe to changes to all users                                                                                                                                                                                                      |
| OpenText Core Endpoint Protection | File Detection                                    | Event that is triggered when the WSA client detects a (potentially) malicious file.                                                                                                                                                    |
| OpenText Core Endpoint Protection | Web Threat Shield URL Action                      | Event that is triggered when Web Threat Shield (WTS) acts on a URL.                                                                                                                                                                    |
| Slack                             | Slash Command                                     | A Slack Slash Command                                                                                                                                                                                                                  |
