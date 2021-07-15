---
pagename: Routing Conversations by Intents
Keywords:
sitesection: Documents
categoryname: "Conversational AI"
documentname: Conversation Orchestrator
subfoldername: Dynamic Routing
permalink: conversation-orchestrator-dynamic-routing-routing-conversations-by-intents.html
indicator: messaging
---

### Getting intents into the Conversation Context Service

By storing a user’s intent as a variable within the Conversation Context Service, that variable’s value will be available for use within a dynamic routing policy.

#### High-level process

1. Create a namespace within Conversation Context Service to store intents.
2. Retrieve the intent using [botContext scripting functions](conversation-builder-scripting-functions-get-set-contextual-data.html#get-matched-intent).
3. Save the intent to the namespace within the Conversation Context Service using [botContext scripting functions](conversation-builder-scripting-functions-manage-the-conversation-context-service.html#set-a-variable).

#### Detailed process

In the Global Function’s ‘__initConversation’ function, create and register a namespace to house intent details. Additionally, save the namespace title as a bot variable that will be used when saving the intent name to the Conversation Context Service.

<img class="fancyimage" width="800" src="img/convorchestrator/co_dr_initconv.png">

```javascript
var intentRoutingNamespace = 'intentRouting';
botContext.registerContextNamespace(intentRoutingNamespace);
botContext.setBotVariable('intentRoutingNamespace', intentRoutingNamespace, true, false);
```

Next, use the [getDialogStarterIntent](conversation-builder-scripting-functions-get-set-contextual-data.html#get-matched-intent) scripting function in the pre/post process code of any interaction to retrieve the name of the most recently matched dialog starter intent.

<img class="fancyimage" width="800" src="img/convorchestrator/co_dr_getintent.png">

Then, save that intent name to the Conversation Context Services conversation scope, using the [setContextDataForConversation](conversation-builder-scripting-functions-manage-the-conversation-context-service.html#set-a-variable) function. Here, we’re demonstrating saving the intent under the chosen namespace with a key of “intent”.

<img class="fancyimage" width="800" src="img/convorchestrator/co_dr_saveintent.png">

```javascript
var intentTitle = botContext.getDialogStarterIntent();
 
var intentNamespace = botContext.getBotVariable('intentRoutingNamespace');
botContext.setContextDataForConversation(intentNamespace, 'intent', intentTitle);
```

{: .important}
This process is not limited to just saving the most recent intent for routing. Other variables that you save in your Conversation Builder bots can be preserved in the Context Session Store for the purpose of dynamic routing using the same high-level approach.

### Creating policies using intents

Having saved the intent names to the Conversation Context Service, you can now create policies that, when triggered by the Next Actions API, return skill information associated with that intent. 

#### High-level process

1. Create a new policy in Conversation Orchestrator which will correspond to the intent you plan to route to.
2. Within your newly created policy, set the condition for the policy to look for the ‘intent’ property of the namespace created above. Set this condition to equal the intent name that corresponds to this policy.
3. Set the Action of this policy to “Transfer to Skill” and select the corresponding skill for this intent from the dropdown.
4. Save and enable your policy. 
5. Complete the steps in the "Testing" section (farther below) to enable routing from your Conversation Builder bots.

#### Detailed process

1. From the Conversation Orchestrator welcome screen, select [Intents](intent-builder-intents.html) under the **Conversation Context Service** heading to see a list of intents that are available for use in your policies. This intent list is generated from all the domains that have been created for your account.

    <img class="fancyimage" width="800" src="img/convorchestrator/co_dr_intentlist.png">

2. Selecting **Intent & Context Policies** under the **Dynamic Routing** header gives access to create and manage the policies for your account. Here, you can view the usage statistics for policies, as well as a configurable list of all policies that have been created for the account.

    <img class="fancyimage" width="800" src="img/convorchestrator/co_dr_policies1.png">

3. To create a new policy, select the **Add Policy** button under the **Manage policies** heading to generate the add policy form to the right. This form contains two sections, one which outlines the conditions that will trigger this policy, and a second that dictates the action that will be sent back to Conversation Builder. Give your policy a name of your choosing. Our recommendation is to assign a name that is related to the intent you are using for routing (e.g., cancel order).

4. Under **Conditions**, assign the attribute using the “namespace.key” syntax. Using our example from the section above, name this attribute as “intentRouting.intent”. Keep the equality and data type dropdowns as their defaults (“=” and “string”), and select the desired intent from the **Enter a value** dropdown. Values can also be manually typed in. However, due to the specificity needed for strings, we recommend either choosing the intent from the dropdown or copying the intent name from the list of intents in step 1.

    <img class="fancyimage" width="800" src="img/convorchestrator/co_dr_conditions1.png">

5. Under **Actions**, define the rule and associated information you want to send back to the bot. For routing purposes, select the **Transfer to skill** option from the dropdown. Leave the second dropdown as the default **skill** choice, and from the final dropdown select the skill you would like this policy to transfer to. The list of skills that have been created for your account will display in that final dropdown menu.

    <img class="fancyimage" width="800" src="img/convorchestrator/co_dr_skilllist.png">

6. After saving, the policy is added to your list of available policies in a **disabled** status. To use the policy in your Conversation Builder bots, make sure to toggle the switch to **enabled** before navigating away from Conversation Orchestrator.

    <img class="fancyimage" width="600" src="img/convorchestrator/co_dr_enabled.png">

    With the policy enabled, you are ready to move back into Conversation Builder where you will complete the process of adding Intent Based Routing to your bot.

### Testing

Once an intent has been saved to the [Conversation Context Service](conversation-orchestrator-conversation-context-service-overview.html) and the policy has been created, you can call the [Next Actions API](conversation-orchestrator-next-actions-api-overview.html) to receive the appropriate action. The returned action will contain a skill ID that corresponds to a bot agent specialized to handle the user’s intent. By using that skill ID in an Agent Transfer integration in Conversation Builder, you will route the conversation appropriately and seamlessly for the user, displaying that the intent routing solution is working as expected.

#### Prerequisites

In order to test out routing by intents, you’ll need to deploy the bot that you are capturing the intent in. This is due to the fact that we are saving the intent to the Conversation Scoping of the Conversation Context Service, and only deployed bots will have a conversation ID associated with them. Additionally, you’ll need to have a bot that is deployed using a skill selected in Step 5 from the “Creating policies using intents” section above. 

For information on how to deploy bot agents in Conversational Cloud, please see our *Conversation Builder - Getting Started* section [here](tutorials-guides-getting-started-with-bot-building-deploy-the-bot.html).

#### askMaven & route to appropriate agent

Above in the *Getting Intents into the Conversation Context Service* section, you captured the intent from a user after triggering a dialog starter. In that same dialog, follow these steps:

First, create a new [Agent Transfer](conversation-builder-interactions-integrations.html#agent-transfer-interactions) interaction. To create a more seamless experience for the user, add the text content BLANK_MESSAGE.

<img class="fancyimage" width="600" src="img/convorchestrator/co_dr_transfer.png">

Then, in the pre-process code of this interaction, call the Next Actions API using the Conversation Builder scripting function, [askMaven](conversation-builder-scripting-functions-askmaven.html). This method returns a string representation of the matching policy, so you will also need to run the JSON.parse method to properly work with the result. An example of the returned JSON:

```
{
 "rule": {
   "id":"ae5418cf-ec4d-494e-8f2d-49c3e2b29a05",
   "name":"Request Refund",
   "actions":[
     {
       "type":"TRANSFER_TO_SKILL",
       "payload":{
         "skillId":"3078481530"
         }
       }
     ]
   }
}
```

Next, parse out the skill ID from the returned JSON using the following syntax. Save this value to a bot variable for use in the setting of your Agent Transfer integration.

<img class="fancyimage" width="600" src="img/convorchestrator/co_dr_code.png">

```javascript
var policy = JSON.parse(botContext.askMaven());
var skillId = policy.rule.actions[0].payload.skillId;
botContext.setBotVariable('skillId', skillId, true, false);
```

Once saved, click the setting wheel for the Agent Transfer integration. Navigate to the **Advanced** tab, and enter `{$botContext.skillId}` into the **Agent Skill Id** field.

<img class="fancyimage" width="600" src="img/convorchestrator/co_dr_intsettings.png">

Lastly, navigate to our messaging test page [here](https://developers.liveperson.com/web-messaging/emulator.html). Enter your account information, open the engagement for your bot, and trigger the dialog by entering an utterance that will match the intent. If successful, the bot will transfer the user to the correct bot to handle their request.

<img class="fancyimage" width="400" src="img/convorchestrator/co_dr_prodbot.png">

{: .important}
When using this feature in Production, it might be desirable to modify or disable the [automatic messages](https://knowledge.liveperson.com/contact-center-management-messaging-operations-automatic-messages-automatic-messages-overview.html) if you want to mask the transfers to and from each bot.
