# Create a Workflow to utilise in your App



***

## Hello World - Workflow Creation

***

> #### 💡 The Power
>
> One of the most powerful aspects of Apps in Rewst, is that the data within can all be made dynamic by utilising Workflows and Jinja as the backend. If you have no idea what these are, make sure you go run through the Cluck U - Foundation series to get a basic understanding. When you come back, we'll make a simple workflow that utilises Rewst's API!

#### 1. Navigate to the Rewst Platform

Start pretty simply, load up the Rewst platform and you'll see the dashboard

![](https://dubble-prod-01.s3.amazonaws.com/assets/dcc929bc-97c5-4ff6-b6ed-d40d0e1fbbb8.png?0)

#### 2. Click on Automations

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/0adf19da-6d60-4920-88a9-efbb00adc44f/2.5/2.2693606773912/13.073701201674?0)

#### 3. Click on Workflows

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/495649de-c084-40ee-be46-a6a15e6d2128/2.5/3.3577532966681/23.011634780099?0)

#### 4. Click on Create

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/9292ed8b-8158-48ef-8d3f-b25f42e550db/2.5/92.548384712543/16.061567657391?0)

#### 5. Give the workflow a name

Give the workflow a name, something that you'll understand. You can also give it a tag, which we recommend doing to ensure your workflows are grouped together.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/6f6620ef-ba27-4c8d-b6da-8f51083e060b/2.5/50.000998652147/42.015659694788?0)

#### 6. The Start

We'll start by creating a noop action, which is an action that does nothing.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/2ac4dd18-cac3-4a4c-a527-35c068a80bb3/1/65.506212347543/52.570494674244?0)

#### 7. Click on the noop, then the pencil on the right hand menu

Change the name of the action to BEGIN, which allows other users reviewing the workflow to clearly identify the "top" of a workflow.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/ee8a294e-6809-43da-95b6-f522fcd5629a/2.5/69.357908328274/6.7974073947152?0)

#### 8. List Forms with Granular Permissions

Next, grab the "List Forms with Granular Permissions" action, which you caan search for. This action is a prebuilt Rewst action that utilises our GraphQL backend to return the requested data.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/14a011bf-8ffa-4324-93f0-a769c5c03596/2.5/5.5676903229594/18.878180479733?0)

#### 9. Connect the BEGIN > list\_forms action

Connect the two actions together from BEGIN > the new action

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/6e4bc9ce-a86e-4644-9553-ef32aafa9d58/1/65.506212347543/52.570494674244?0)

#### 10. Publish Result

In the new action, add `all_available_forms` as the Publish Results As variable name. This ensures that the output of the action gets added to this variable.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/69d53102-8ba4-4d7e-93da-ec61c194a1c1/2.4153988716738/98.657144463929/38.955140384052?0)

#### 11. Code Editor

Under the params on the action, click the "Edit Code" icon highlighted in the image below

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/d5b46956-d1ea-4213-adc9-120d88307001/2.5/94.829629398585/64.303357058644?0)

#### 12. Enter Jinja referencing the running user

In Jinja, we can use \{{ [CTX.user.id](http://ctx.user.id) \}} which uses the ID of the running user, ensuring we always get the right forms based on the logged in user.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/0c27ed0c-8d35-4eb6-8e64-08959f2c46f1/2.1142858896301/51.047481554504/36.090524236119?0)

#### 13. Advanced Tab

On the Advanced tab, we can amend the "Run as Org" which works in the same way as the Run As User, and ensures that we always run as the org we are logged into. If you have a form that is only enabled for certain orgs, this is how we return the correct ones.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/0560b5c8-52ae-4748-b138-ed30f6a18995/2.5/78.076518228346/48.017990225382?0)

#### 14. Jinja in Run as Org

We add \{{ [ORG.ATTRIBUTES.id](http://org.attributes.id) \}} into the Run as Org box under the Advanced tab.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/30a89a45-0058-4bfc-aebe-9b63df8e43be/2.5/50.984305421461/34.398740919757?0)

#### 15. And another noop...

Let's add another noop and connect our list\_forms action to it. We can name this one `set_form_output` to make it clear what we're going to do.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/e5082cb9-955f-4da3-9e55-0b0e33bef9f7/1/65.506212347543/52.570494674244?0)

#### 16. Add a Data Alias

On the noop, we're going to create a new data alias called `form_output`

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/87d3965c-567a-4831-9953-130914869491/2.5/98.657139012071/45.069695017914?0)

#### 17. Code Editor

Once again, click the code editor icon next to your new data alias

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/e2a7c13f-af58-4125-8da5-8adead293264/2.5/87.237153568404/56.866768701449?0)

#### 18. The Jinja

We wont go fully into the Jinja here, but feel free to reach out to the ROC if you'd like to understand more what's happening here. The jist of it is that we are looking at all the returned forms, and creating a new key/value dict with name, tags, view and triggerId key. Eventually we'll display the name and tags to the user and use the view key to allow an action for the user - in our case, to go directly to the form. The Jinja can be copied below.

```
{#- Assumes single trigger per form -#}
{{ [
    {
      "name": form.name,
      "tags": form.tags,
      "view": "https://app.rewst.io/form/"~form.triggers[0].id | d,
      "triggerId": form.triggers[0].id | d
    } for form in CTX.all_available_forms if form.triggers|length > 0
] }}
```

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/f58dee63-48f2-4c77-8c4e-53309def4233/2.5/50.984305421461/34.398740919757?0)

#### 19. Final Noop

Add one more noop into the workflow and call it "END", and connect it to the 3rd action as per the image.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/cfd20285-c098-4e70-bd1a-bc467f7edf48/1/65.506212347543/52.570494674244?0)

#### 20. Set Workflow Outputs

Next, we need to ensure that the data alias we created actually gets output when the form runs. Click the pencil in the top right of the Workflow Builder, as shown in the image below

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/e7a084d1-6fa2-4191-ae35-48adb974320d/2.5/85.498228870855/1.3933863552529?0)

#### 21. Add Output Configuration

Click the + next to the Output Configuration and call it `form_output` (we can call this whatever we want). In the Jinja, enter \{{ CTX.form\_output \}} - this references the Jinja we made earlier on in the 3rd noop. Remember that one we called `set_form_output` ?

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/eedb0c79-75fe-4dc9-b659-0ecf47f48cbf/2.5/56.535105887658/71.406511607748?0)

#### 22. Click on Submit

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/e26fe2dd-5059-45a1-88e8-7823c80b2bdb/2.5/79.906770530595/78.771738187063?0)

#### 23. Click on Publish

Save the workflow!

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/8e575d46-9a37-4747-8bac-2d31d3038ee1/2.5/100.00199249383/0?0)

#### 24. Marvel in Rewsty

Click the Rewsty Robo-head and marvel at how we utilise AI to identify the changes made in the Workflow Builder to generate the commit notes.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/8db705d2-3447-4c72-8393-90a45ca3d8db/2.5/65.13647999068/38.448484731739?0)

#### 25. Click on Submit

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/4ae59b8d-1cce-476b-a0e8-dc3d8a87cf2d/2.5/68.380444187134/96.504334813112?0)

#### 26. Click on Test

Finally, let's make sure it actually works!

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/d94dd980-e60f-4fd4-85b6-d8b14cc65def/2.5/96.496620194258/0?0)

#### 27. Click on Test

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/d694456b-9c5a-40fa-9a00-b7557886e0af/2.5/74.885777477058/54.958326544259?0)

#### 28. Click on View Results

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/6620cc93-6a1f-417c-9ead-9cdfead3d832/2.5/59.405584283214/7.7570362307242?0)

#### 29. Click on END

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/8fa2cc87-fbcc-4887-8fff-86c45a98c69a/2.0619180396/36.369196092847/60.363212791649?0)

#### 30. Click on output

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/543b30ed-75ad-422c-9a29-0e3336a7e775/2.5/72.376844992203/74.921114920738?0)

#### 31. Click on form\_output

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/c111fba0-f0ec-4344-a1fa-642459980d37/2.5/74.887025631892/77.01249226551?0)

#### 32. Click on ...

You'll see very similar to the below, where you'll see a list of the forms that have been output! You may not have three, that's fine as it just shows what you have access to.

![](https://d3q7ie80jbiqey.cloudfront.net/media/image/zoom/171467b7-07ba-4008-8be6-d732ccd6bcc6/2.5/72.452533099771/78.730221759161?0)

> #### ⚠️ Ooooft!
>
> Okay, that was a lot. Building a workflow can be daunting, but if you ever have a problem know that everyone at Rewst wants to help you succeed! If you have had any issues with this, make sure you utilise your Discord private channel and tag ROC Support.
