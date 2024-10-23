# Deploying Agent Smith with ImmyBot

{% hint style="info" %}
This was shared during a recent open mic: [Feb 2nd, 2024 - Inside the Eye of the Brainstrom](https://docs.rewst.help/updates/roc-open-mics/feb-2nd-2024-inside-the-eye-of-the-brainstrom).&#x20;

**Shout out to Kewp Member Logan for submitting this guide!**
{% endhint %}



[Immybot](../../documentation/integrations/rmm/immybot/) is an extremely powerful DSC platform that utilizes integrated agents to spawn an 'ephemeral' agent. This agent is then capable of running scripts such as the ones provided in this directory while being fueled by Immy's amazing PS Functions.

One important thing to know if you've never used Immy, is that `Invoke-ImmyCommand` is essentially the same as `PSRemote`'s `Invoke-Command`.

## Setup

### High-level overview

1. Create the [`software`](deploying-agent-smith-with-immybot.md#software) object in Immy
   * Immy uses software objects to interpret an application that should be deployed and how to do so.
   * The scripts [here](https://github.com/BezaluLLC/Project-Foghorn/tree/main/ImmyBot%20Integration) should be entered in the corresponding blank script fields
   * The PowerShell scripts handle:
     * Detection of the agent
     * Installation of the agent
     * Uninstallation of the agent
     * Dynamically acquiring the latest version of the agent
     * Comparing the existing version vs. the latest version and applying the desired state.
2. Create and assign a [`configuration task`](deploying-agent-smith-with-immybot.md#configuration-task) to the software object.
   * Configuration tasks can run post-install/update/detection scripts typically intended for ensuring running compliance with your configured settings.
   * Configuration tasks also store parameters for the software object. This allows for using variables in every other script for the software object, even without scripts being set on the task.
3. Create and define a [`Deployment`](deploying-agent-smith-with-immybot.md#deployment)
   * Deployments are where the magic happens- this is where you tell Immy where and if you want your software present.
   * Select `Agent Smith` for the software in question, fill in the parameters
4. Using Agent Smith for Immy script execution (_coming soon_:tm:)

### Software

1. To set up a software in Immy for Agent Smith, start in the left menu, then `Library > Software > New`.\
   ![image](https://github.com/BezaluLLC/Project-Foghorn-agent/assets/2997336/ea8f749a-47cf-4a05-af40-c461a9a17839)
2. This will bring you to a setup page that asks for an installer. Go ahead and indicate `none` here. ![image](https://github.com/RewstApp/docs.rewst.help/assets/2997336/48ccca1a-dd66-49c1-b807-bd6ab0535666)
3. Next, it will ask for a software to add the version to. Select `Add version to new software`. ![image](https://github.com/RewstApp/docs.rewst.help/assets/2997336/6eceb9ff-bb22-410b-95b8-c3a40e2897e8)
4. After selecting `new software`, you should be on the actual setup page now. Enter a name, logo, and description for your agent
5.  Begin loading the PowerShell scripts into each corresponding field.

    * The names of the scripts I provide in this directory indicate where they should be used on this page.
    * The image below should also serve as a handy guide:&#x20;



    <div align="left">

    <figure><img src="https://github.com/BezaluLLC/Project-Foghorn-agent/assets/2997336/fb95e366-9315-4d20-8dbc-37e641aa58ab" alt="" width="375"><figcaption></figcaption></figure>

    </div>

### Configuration Task

You will also need to set up a `Configuration Task` in order to pass parameters into the script.\
The way Immy handles this is by loading said parameters into a `Configuration Task`, then filling in your parameters:

&#x20;

<div align="left">

<figure><img src="https://github.com/BezaluLLC/Project-Foghorn-agent/assets/2997336/8f5bff3b-8b2a-4028-a777-2cc511eb2faa" alt="" width="375"><figcaption></figcaption></figure>

</div>

Once parameters are all set, set `Scripts` to `Use separate scripts` and disable the `Test`, `Get`, and `Set` scripts, as we do not need to do any post-install configuration.&#x20;

<div align="left">

<figure><img src="https://github.com/BezaluLLC/Project-Foghorn-agent/assets/2997336/42a9ed06-bab8-456b-8cb0-ea15eec2a122" alt="" width="375"><figcaption></figcaption></figure>

</div>

### Deployment

Once the rest is completed, all you need to do is deploy!

&#x20;

<div align="left">

<figure><img src="https://github.com/BezaluLLC/Project-Foghorn-agent/assets/2997336/47c630f1-6511-4eb1-a744-69bae7de8d7e" alt="" width="375"><figcaption></figcaption></figure>

</div>

Fill in all parameters, select your targets, and you're done! :tada:\
If you have any troubles, the people in the [#v-immybot](https://discord.com/channels/801971115013963818/882364989057433680) channel in the [MSPGeek discord](https://discord.gg/mspgeek) has a ton of brilliant people willing to help :)
