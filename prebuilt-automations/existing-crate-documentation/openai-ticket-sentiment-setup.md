# OpenAI ticket sentiment

{% hint style="info" %}
**Azure OpenAI Instance**

Note that this Crate works for both OpenAI and OpenAI with an Azure instance.\
In order to use the Azure instance, you will need to follow the [Azure OpenAI Integration Setup](../../documentation/integrations/ai/openai/azure-openai-integration-setup.md) steps and follow the below steps.
{% endhint %}

### What does this Crate do?

This Crate uses the OpenAI API to analyze the sentiment of the customer note on a ticket.

We are then able to determine whether the sentiment is positive, negative, or neutral based on your configured threshold and then update the ticket priority, severity, and impact (depending on the PSA) accordingly.

This also means that if a ticket comes in that is considered a negative sentiment, we can then automatically escalate the ticket to the relevant person/team.

This Crate was built with various reasons in mind, but most notably to help with the following:

* **Quicker Response Times** - By automatically escalating tickets that are considered negative sentiment, you can ensure that you're responding to your customers quicker and more efficiently. This will help you to improve your customer satisfaction. Our experience shows that the faster you respond to a frustrated client, the more likely they are to be happy with the resolution.
* **Correct Prioritization** - By automatically updating the priority, severity, and impact of a ticket based on the sentiment, you can ensure that your techs are working on the right tickets at the right time. This will help you to improve your customer satisfaction, as well as identify any repeating issues that may be causing negative sentiment.
* **Another differentiator** - By using this Crate, you can ensure that you're differentiating yourself from your competitors. You can talk about how you're using AI not to respond using that AI, but to ensure that a human looks at the ticket quicker. Having an auto-escalation process in place will help you to stand out from the crowd.

### This sounds great but, I use \[Insert PSA] - can I use this?

Yes! This Crate is PSA agnostic, so it will work with any of the PSAs that we support and also have a trigger type that kicks off the automation.

This list is currently:

* ConnectWise Manage
* Datto PSA
* HaloPSA
* Kaseya BMS

If you're using a PSA that isn't on this list, please let us know and we'll look at whether it has the ability to trigger an automation based on a ticket being created.

### So what steps does the Crate actually take? What is the automation?

1. We identify the initial description/note on the ticket
2. We identify the PSA that the ticket came from, and convert the JSON payload we got sent into standard variables (such as ticket title, description, etc.)
3. We send this data to OpenAI with a prompt that we've configured. Note that this prompt is templatized, so you are able to configure/tweak it to your liking. This prompt takes the note and asks OpenAI to analyze the sentiment of the note, the urgency of the ticket, and the impact of the ticket - on a ranking of 1-5.
4. OpenAI then returns the sentiment, urgency, and impact of the ticket in a JSON object as well as the reason that it has determined this.
5. We then identify whether any of the variables are above the threshold configured by you. If they are, we then update the ticket priority, severity, and impact (depending on the PSA) accordingly. We also added a note to the ticket to say that the ticket has been updated based on the sentiment analysis.
6. If the sentiment threshold has also been met, we then escalate the ticket to the relevant person/team by amending the owner, team, or status of the ticket (depending on the PSA).
7. We ensure that for each action taken during the automation, we add a note to the ticket to say what has happened and why it has happened.

### What do I need to get started?

We have tried to make this as user-friendly and straightforward as possible to get started, so this crate is installable from the [Crate Marketplace](https://app.rewst.io/marketplace/crates/202aa56b-c1ff-46c7-8a34-bf1b4e49ecc4).

There are three steps to getting this crate up and running:

1. Set up the integration with OpenAI in your Rewst account.
2. Unpack the crate in the marketplace, answering the questions as you go,
3. Enjoy! [and tell us how awesome it is!](openai-ticket-sentiment-setup.md#feedback)

#### Step 1 - Set up the integration with OpenAI in your Rewst account

In order to use this crate, you'll need to have an OpenAI account.

Follow the instructions on the [OpenAI Integration Setup](../../documentation/integrations/ai/openai/openai-integration-setup.md) page to get this set up and then come back here!

Remember, you can also set up an Azure instance of OpenAI, and use that with this crate. If you want to do that, you'll need to follow the Azure OpenAI Integration Setup steps.

#### Step 2 - Unpack the crate in the marketplace

Find the crate in the marketplace, called "Open AI Ticket Sentiment Analysis". Alternatively, [click here](https://app.rewst.io/marketplace/crates/202aa56b-c1ff-46c7-8a34-bf1b4e49ecc4) to go straight to the crate.

and once you're in the crate, select your PSA from the dropdown and some other options around when you want the automation to run.

The OpenAI returns all of the data in a JSON object, including an integer for Sentiment, Urgency, and Impact. We then use the options you specify below to determine whether the ticket should be updated or not.

**Sentiment Threshold:**

This is the threshold that you want to set for the sentiment of the ticket. If the sentiment is below this threshold, the ticket will be considered a positive sentiment. If the sentiment is above this threshold, the ticket will be considered negative sentiment, and update the ticket accordingly.

**Urgency Threshold:**

This is the threshold that you want to set for the urgency of the ticket. If the urgency is below this threshold, the ticket will be considered low urgency. If the urgency is above this threshold, the ticket will be considered high urgency, and update the ticket accordingly.

**Impact Threshold:**

This is the threshold that you want to set for the impact of the ticket. If the impact is below this threshold, the ticket will be considered low impact. If the impact is above this threshold, the ticket will be considered high impact, and update the ticket accordingly.

**Error Reporting**

Set `Report errors in ticket when unable to utilise AI` to true if you want any workflow errors reported in the ticket.

On the following screen, you'll be asked to **disable the triggers that you don't need** for the PSAs that are not required (we'll make this easier soon!).

<figure><img src="../../.gitbook/assets/DisabledTriggers (1).png" alt=""><figcaption><p>Disabling Unused Triggers</p></figcaption></figure>

The trigger that will kick off the automation when a ticket is created, is the one left enabled. In our example, Halo PSA.

<figure><img src="../../.gitbook/assets/EnabledTrigger.png" alt=""><figcaption><p>Enabled Trigger</p></figcaption></figure>

That's it, hit "Unpack" and you're good to go! Go create a ticket in your PSA with a _somewhat frustrated_ description, and then watch the magic happen!

<figure><img src="../../.gitbook/assets/HaloPSANote (1).png" alt=""><figcaption></figcaption></figure>

### Useful Organization Variables (Optional)

These Organization Variables give you more control over the functionality of this workflow.
- ORG.VARIABLES.ticket_sent_max_tokens
    - Allows you to manually set the max tokens
- ORG.VARIABLES.ai_model_ticket_sent
    - Allows you to manually set the model

### Feedback

Genuinely, if you like this crate and have followed these instructions to get it up and running, we'd love to hear from you! We're always looking for feedback on how we can improve our crates, so please [click me](mailto:roc@rewst.io) and let us know what you think! If you'd like to only say thanks, that's cool too! You can [click me instead](https://engine.rewst.io/webhooks/custom/trigger/db81c9a8-13f7-458a-9306-287054605844/c47fdd7f-4075-47a8-ba92-94e790e67c06?crate=OpenAISentimentAnalysis) and we'll send an awesome gif to our internal Slack channel! 😁
