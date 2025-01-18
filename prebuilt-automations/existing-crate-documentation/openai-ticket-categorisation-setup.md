# OpenAI ticket categorization

{% hint style="info" %}
**Azure OpenAI Instance**

Note that this crate works for both OpenAI and OpenAI with an Azure instance.\
In order to use the Azure instance, you will need to follow the [Azure OpenAI Integration Setup](../../documentation/integrations/ai/openai/azure-openai-integration-setup.md) steps and follow the below steps.
{% endhint %}

### What does this Crate do?

This crate uses the OpenAI API to categorize tickets, using your built-in types, sub-types etc. as the categories.

This means that rather than your tech having to triage a ticket after the fact, the ticket will already be triaged almost immediately when it comes into the PSA.

This crate was built with various reasons in mind, but most notably to help with the following:

* **Internal Reporting** - Our experience at MSPs is that the majority of tickets are categorized incorrectly. This means that when you're trying to report on the types of tickets you're getting, you're not getting an accurate picture. This crate will help you get a more accurate picture of the types of tickets you're getting, and the types of tickets your techs are working on. This then allows both you and your techs to make better decisions - knowledge is power!
* **Automation Building** - One of the most common questions we get asked is "What do we automate?" - this crate will help you answer that question. By categorizing your tickets, you can then see which types of tickets are taking up the most time, and which types of tickets are taking up the most time for your techs. This then allows you to make better decisions about what to automate.
* **General Time Savings** - Whilst triaging tickets is a necessary evil, it's also a time-consuming one when you think about the number of tickets that come in. This crate will help you save time by using your own data to categorize tickets, rather than having to do it manually.

### This sounds great, but I use \[Insert PSA] - can I use this?

Yes! This crate is PSA agnostic, so it will work with any of the PSAs that we support and also have a trigger type that kicks off the automation.

This list is currently:

* ConnectWise Manage
* Datto PSA
* HaloPSA
* Kaseya BMS

If you're using a PSA that isn't on this list, please let us know and we'll look at whether it has the ability to trigger an automation based on a ticket being created.

### So what steps does the Crate actually take? What is the automation?

1. We identify the initial description/note on the ticket
2. We identify the PSA that the ticket came from, and convert the JSON payload we got sent into standard variables (such as ticket title, description, etc.)
3. We identify a list of your existing types, subtypes, and items (depending on the PSA)
4. We send this data to OpenAI with a prompt, specifying the types and subtypes, etc. from your PSA. Note that this prompt is templatized, so you are able to configure/tweak it to your liking
5. OpenAI then returns the category that it thinks the ticket falls into as a JSON object
6. We then parse this JSON object and update the ticket with the category that OpenAI has returned
7. We then update the ticket with a note, showing the category that OpenAI returned as well as the reasoning behind it

### What do I need to get started?

We've tried to make this as user-friendly and straightforward as possible to get started, so this crate is installable from the [Crate Marketplace](https://app.rewst.io/marketplace/crates/0faa5757-a92a-4d75-9ddc-3549ea51bca2).

There are three steps to getting this crate up and running:

1. Set up the integration with OpenAI in your Rewst account.
2. Unpack the crate in the marketplace.
3. Enjoy! [and tell us how awesome it is!](openai-ticket-categorisation-setup.md#feedback)

#### Step 1 - Set up the integration with OpenAI in your Rewst account

In order to use this crate, you'll need to have an OpenAI account.

Follow the instructions on the [OpenAI Integration Setup](../../documentation/integrations/ai/openai/openai-integration-setup.md) page to get this set up and then come back here!

Remember, you can also set up an Azure instance of OpenAI, and use that with this crate. If you want to do that, you'll need to follow the Azure OpenAI Integration Setup steps.

#### Step 2 - Unpack the crate in the marketplace

Find the crate in the marketplace, called "OpenAI Ticket Categorization". Alternatively, [click here](https://app.rewst.io/marketplace/crates/0faa5757-a92a-4d75-9ddc-3549ea51bca2) to go straight to the crate.

<figure><img src="../../.gitbook/assets/CrateInMarketplace.png" alt=""><figcaption><p>Searching for the Crate</p></figcaption></figure>

Once in the crate, select your PSA from the dropdown, the OpenAI Model, and if you want issues with OpenAI reported in the ticket.

<figure><img src="../../.gitbook/assets/CrateOpenAICategorySelectPSAAndTokens.png" alt=""><figcaption><p>Selecting a PSA, OpenAI Model, and error reporting</p></figcaption></figure>

On the following screen, you'll be asked to **disable the triggers that you don't need** for the PSAs that are not required (we'll make this easier soon!).

<figure><img src="../../.gitbook/assets/DisabledTriggers.png" alt=""><figcaption><p>Disable The Unused Triggers</p></figcaption></figure>

The trigger that will kick off the automation when a ticket is created, is the one left enabled. In our example, Halo PSA.

<figure><img src="../../.gitbook/assets/Enabledtriggers.png" alt=""><figcaption><p>Enabled Trigger</p></figcaption></figure>

That's it, hit "Unpack" and you're good to go! Create a ticket in your PSA with a typical description and summary, and then watch the magic happen!

<figure><img src="../../.gitbook/assets/HaloPSANote.png" alt=""><figcaption></figcaption></figure>

### Useful Organization Variables (Optional)

These Organization Variables give you more control over the functionality of this workflow.
 - ORG.VARIABLES.ticket_cat_max_tokens
    - Allows you to manually set the max tokens
 - ORG.VARIABLES.ai_model_ticket_cat
    - Allows you to manually set the model


### Feedback

Genuinely, if you like this crate and have followed these instructions to get it up and running, we'd love to hear from you! We're always looking for feedback on how we can improve our crates, so please [click me](mailto:roc@rewst.io) and let us know what you think! If you'd like to only say thanks, that's cool too! You can [click me instead](https://engine.rewst.io/webhooks/custom/trigger/db81c9a8-13f7-458a-9306-287054605844/c47fdd7f-4075-47a8-ba92-94e790e67c06?crate=OpenAITicketCategorisation) and we'll send an awesome gif to our internal Slack channel! 😁
