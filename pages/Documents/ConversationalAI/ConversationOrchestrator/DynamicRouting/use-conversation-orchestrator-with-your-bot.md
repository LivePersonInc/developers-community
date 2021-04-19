---
pagename: Use Conversation Orchestrator with Your Bot
redirect_from:
  - maven-ai-powered-routing-use-maven-with-your-bot.html
  - maven-ai-ai-powered-routing-use-maven-with-your-bot.html
  - maven-ai-dynamic-routing-use-maven-with-your-bot.html
  - conversation-orchestrator-dynamic-routing-use-maven-with-your-bot.html
Keywords:
sitesection: Documents
categoryname: "Conversational AI"
documentname: Conversation Orchestrator
subfoldername: Dynamic Routing
permalink: conversation-orchestrator-dynamic-routing-use-conversation-orchestrator-with-your-bot.html
indicator: messaging
---

If you want more control and customization on your conversational experience, you may use the [Recommendation APIs](maven-askmaven-overview.html) from a concierge bot or LOB app to ask Conversation Orchestrator about the next best action for a set of conditions. This is appropriate if:

- You already have a concierge bot that handles branded greetings, intents, and dialogs

- You want to route by Intents, entities, and other attributes from a concierge bot

- You have deeper customization needs to use Conversation Orchestrator capabilities at runtime

This method is usually used alongside Conversation Context Service APIs to send intents and attributes. 

**Example**:

The following example shows how to use [Recommendation API](maven-askmaven-overview.html) and [Conversation Context Service](maven-context-warehouse-context-session-store.html) APIs from a concierge bot.

1. A concierge bot handles branded greetings and intents. 

2. It uses the Conversation Context Service APIs to store the value of the intent in the store

3. The bot then calls Recommendation APIs to get a routing decision. Because the intent has been set, Conversation Orchestrator can now use this information to evaluate a routing policy. 

<img class="fancyimage" width="750" src="img/maven/image_48.png">

### Recommendation API from Conversation Builder

#### Get The Conversation ID

The conversation id is required for using the Recommendation APIs if your policies use Inbox System Attributes. 

The variable can be used anywhere in conversation builder using the following variable name: 

{$botContext.conversationId}
 

#### Call Conversation Context Service APIs

The Conversation Context Service is useful in storing any context information gathered in a bot that you may want to use in a routing policy. For instance you may want to set the intent detected by a bot and then use it for any routing policy.

====> PLEASE UPDATE the below section on using Conversation Context Service API  from Conversation Builder. Why use an API Integration, if you can use the built-in scripting functions in CB for managing the Conversation Context Service?  See https://developers.liveperson.com/conversation-builder-scripting-functions-manage-the-conversation-context-service.html    <=====
You can call the Conversation Context Service API by setting up an [Integration](conversation-builder-integrations-api-integrations.html) with the [Conversation Context Service API](maven-context-warehouse-context-session-store.html) details. You may use the conversation id to store the session state, and pass the conversation id in the Recommendation API call. 

<img class="fancyimage" width="500" src="img/maven/Call Session Store APIs from CB.png">


#### Call Recommendation APIs

Recommendation APIs can be used in a Conversation Builder bot using [Integrations](conversation-builder-integrations-integration-basics.html).

1. Add API Integration to Conversation Builder

   <img class="fancyimage" width="500" src="img/maven/image_49.png">

2. Edit Integration Settings for Recommendation APIs. Use the appropriate URL based on your location
   1. Americas: https://z1.askmaven.liveperson.net
   2. EMEA: https://z2.askmaven.liveperson.net
   3. APAC: https://z3.askmaven.liveperson.net

   
   * **Conversation Orchestrator API key** is retrieved from Conversation Orchestrator.

   * **AccountID**: use your Conversational Cloud account ID. If you are not sure please contact support or your customer representative to get the account ID.

   * **Conversation ID**: This allows Conversation Orchestrator routing policy to retrieve conversation attributes to evaluate the policy. 

   <img class="fancyimage" width="700" src="img/maven/image_50.png">

3. Use response from Recommendation API to execute a transfer to Skill task

### Recommendation API from Google DialogFlow

#### Get The Conversation ID

The conversation id is required for using the Recommendation APIs. This ID is used by the policy to retrieve conversation and Conversation Context Service parameters. 

Inside **Dialogflow Fulfillment**, modify the sample code for the event handler for each request. 

Inside the request event handler function (i.e. the `functions.https.onRequest`), you can get the conversationId as the last part of the `request.body.session` string after the last `/`.  

In the following `request.body.session` example string, `ea15cd3f-561d-4acf-90ae-5eb14145d38d` is the conversationId.

* `projects/appointmentscheduler-69117/agent/sessions/ea15cd3f-561d-4acf-90ae-5eb14145d38d`

You can get the Conversational Cloud conversationId with this line of code:

```javascript
request.body.session.substring(request.body.session.lastIndexOf("/") + 1);
```

For debugging, you can see the logs by clicking the link **“View execution logs in the Firebase console”** inside the Dialogflow Fulfillment page.

#### Call Conversation Context Service APIs

Click `package.json` to include your favorite Node.js HTTP library. In the example, we include the axios HTTP library.

The Conversation Context Service is useful in storing any context information gathered in a bot that you may want to use in a routing policy. For instance you may want to set the intent detected by a bot and then use it for any routing policy. 

```javascript
const contextUrl = 'https://z1.context.liveperson.net/v1/account/55884191/namespace1/' + conversationId + '/properties';
 
var data = {
   'key1': 'val1',
   'key2': 'val2',
   'time': Date.now()
};

axios.patch(
   contextUrl, 
   data, 
   { headers: { 'Content-Type': 'application/json', 'maven-api-key': <MAVEN_API_KEY> } }
);
```

#### Call Recommendation API

Now that you have the conversation id, use it to call the Recommendation API as follows. 
 
```javascript 
const askMavenUrl = 'https://z1.askmaven.liveperson.net/v1/account/55884191/next-actions';
 
axios.get(
   askMavenUrl, 
   { headers: { 'Content-Type': 'application/json', 'maven-api-key': <MAVEN_API_KEY> } }
).then(function(response){
   const rule = response.rule;
   if (rule && rule.actions) {
      // You can inspect the actions and do something according to the actions
      //   e.g. transfer to an agent or skill, or send back a message.  
      //        Here we just log the actions to the console.
      console.log(rule.actions); 
   }
});
``` 
