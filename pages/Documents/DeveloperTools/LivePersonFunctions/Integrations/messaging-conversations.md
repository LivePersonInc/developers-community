---
pagename: Messaging Conversations
keywords:
sitesection: Documents
categoryname: "Developer Tools"
documentname: LivePerson Functions
subfoldername: Integrations
permalink: liveperson-functions-integrations-messaging-conversations.html
indicator: messaging
redirect_from:
  - liveperson-functions-liveperson-integrations-messaging-conversations.html
  - function-as-a-service-use-cases-messaging-conversations-with-functions.html
---

This guide explains how to enable LivePerson Functions for messaging.

With **Functions for messaging** you are able to invoke `lambdas` from standard messaging events. For example, a new conversation start event could be chosen as the trigger to invoke a pre-created function.

Along with the invocation, the function is sent a payload containing metadata related to the conversation which invoked the function. This payload can then be used in the function for further processing and referencing.

<div class="important"> It is required that your account has the Controller Bot permissions enabled; please contact your account team in order to do this.</div>

### Best Practices

Functions for messaging listens for messaging events asynchronously. As a consequence this can cause race conditions with other parts of the platform. Therefore, it is considered best practice to use bots instead of Functions for implementing routing logic. Functions is a good option to sync data with third-party systems like CRMs or to save data in the [Conversation Context Service](maven-context-warehouse-overview.html) in order to use it within Conversation Orchestrator. Routing via Functions makes sense whenever a conversation is in a stagnant state (i.e. not in process of being routed), e.g. a conversation is idle or a message line has been sent in off-hours. Otherwise, the asynchronous nature of its events might interfere with the proper flow of a "dynamic" conversation.


<div class="important">if the authenticated consumer's previous conversation was auto-closed, and the new one opened within 48 hours of that, the new conversation event won't be triggered.</div>

### Messaging events for Function Invocation

Conversational Cloud messaging uses a series of "Conversation State Change Events" which are fired when specific actions or events occur within the conversation. You are able to use these events to trigger your functions.



### Callback commands

You have the option to send callback commands back to the invoker. You can add multiple commands to the response as the functions itself can return an array or a single object.

With the controller bot as the invoker, as is the case for messaging events, you have the option to execute the following callback commands:

* Send a message

<div class="important">
  <ul>
    <li></li>
    <li>If no message is set in the result of the function (which it returns to the invoker, for example: <code>callback();</code> ), the default automatic message for the account will be triggered.</li>
    <li>The default automatic message can be overwritten with
        <code>{
            type: "systemMessage",
            text: "your message"
        }</code>. To set the message empty just pass <code>[]</code> as text.</li>
  </ul>
</div>

* Transfer Conversation to a different Skill

* Transfer Conversation to a different Agent (to configure this feature see [here](https://knowledge.liveperson.com/contact-center-management-messaging-operations-transfer-to-agent.html))

* Close the Conversation

<div class="important">Using callback commands is <b>not</b> mandatory. If you only wish to use the events listed above to trigger functions and nothing else, there's no reason for you to pass callback commands back.</div>

If you add more than one command of a certain type (e.g. 2 messages) **only the first command** of this type will be processed.

Please have a look at [this page](function-as-a-service-developing-with-faas-events-templates.html) for further insight into the available events and their related templates. You can also have a look at the related templates per messaging-event within the LivePerson Functions application itself.


#### Step 1 - Create function

Create a new function using one of the messaging templates.

Currently, only one function per template type can be created. If there are multiple types of functionality needed that stem from the same event invocation, these should be coded into the same `lambda`.

Once you have selected a "messaging conversations" event you can further specify its criteria to be invoked by one or more skills. A lambda with a set amount of skills will only be triggered if the conversation had this specific skill is attached to it. The set of skills can be changed at any given time.

<img src="img/faas-select-skill.png" alt="Functions select skill" style="width:100%;"/>

<div class="important">By default no skill is selected. This will cause the lambda to react to all invocations regardless of skill. The maximum number of skills which can be specified is <b>10</b>. Changing the skills of a lambda does not require a redeployment. The change is reflected within 5 minutes after saving.</div>

Specifying a skill has the advantage of reducing the complexity of the lambda's code. Furthermore, it reduces the number of unnecessary invocations.
#### Step 2 - Edit the Function

Adjust the coding from the template according to your needs by modifying the function. On the right side you can see an example of the payload (in the sidebar, which you might need to open):

As mentioned above, the function can return a series of commands back to the invoker. In the template code you can see the current available commands.

Here's an example of a response sent back to the invoker using a few of those commands:

```javascript
let result = [
   {
       type: "systemMessage", // Returns a system message into the conversation
       text: "your message"
   },
   {
       type: "transfer", // Transfers the conversation.
       skillId: "123456", // Transfer to different skill.
       agentId: "123456" // Propose an agent.
   },
   {
       type: "closeConversation" // Closes the conversation
   }
]
callback(null, result);
```

#### Step 3 - Deploy the function

Just like any other function, this function must be deployed before it can be used. [Please see this document](function-as-a-service-deploying-functions.html) for more information on how to deploy your function. At this point, you can also test your function.

<div class="important">Try to deploy functions with a runtime of less than one second. If the runtime is longer, you may get a bad user experience because of race conditions within the server. For example, if you create a function based on the <b> Participants Change</b> event and an agent joins the conversation, the consumer may see the resulting `systemMessage` <b>after the agent already responded to the consumer themselves</b>.</div>

### Payload Details

<table>
<thead><tr><th>1. level</th><th>2. level</th><th>3. level</th><th>description</th><th>type</th><th>example</th></tr></thead><tbody>
 <tr><td>end</td><td>closeReason</td><td>&nbsp;</td><td>which role closed conversation</td><td>STRING</td><td>AGENT/CONSUMER/SYSTEM</td></tr>
 <tr><td>general</td><td>type</td><td>&nbsp;</td><td>notification type</td><td>STRING</td><td>UPSERT</td></tr>
 <tr><td>general</td><td>convId</td><td>&nbsp;</td><td>ID of conversation</td><td>STRING</td><td>c840e51e-5f65-4ad4-8d34-5c82b99a2200</td></tr>
 <tr><td>general</td><td>dialogId</td><td>&nbsp;</td><td>ID of dialog</td><td>STRING</td><td>c840e51e-5f65-4ad4-8d34-5c82b99a2200</td></tr>
 <tr><td>general</td><td>sessionId</td><td>&nbsp;</td><td>ID of session</td><td>NUMBER</td><td>1528463744580</td></tr>
 <tr><td>general</td><td>startTs</td><td>&nbsp;</td><td>conversation start time as timestamp</td><td>NUMBER</td><td>1528463744663</td></tr>
 <tr><td>general</td><td>effectiveTTR</td><td>&nbsp;</td><td>timestamp when agent should be available</td><td>NUMBER</td><td>1528464044687</td></tr>
 <tr><td>general</td><td>oldConvState</td><td>&nbsp;</td><td>previous state of the dialog</td><td>STRING</td><td>CLOSE</td></tr>
 <tr><td>general</td><td>newConvState</td><td>&nbsp;</td><td>current state of the dialog</td><td>STRING</td><td>OPEN</td></tr>
 <tr><td>general</td><td>contexttype</td><td>&nbsp;</td><td>type of cotext</td><td>STRING</td><td>SharkContext</td></tr>
 <tr><td>general</td><td>campaignInfo</td><td>id</td><td>ID of campaign</td><td>NUMBER</td><td>2327699812</td></tr>
 <tr><td>general</td><td>campaignInfo</td><td>engangementId</td><td>ID of engangement </td><td>NUMBER</td><td>2327699912</td></tr>
 <tr><td>general</td><td>clientLanguage</td><td>&nbsp;</td><td>language of the client device</td><td>STRING</td><td>en-US</td></tr>
 <tr><td>general</td><td>clientFeatures</td><td>&nbsp;</td><td>list of supported client features</td><td>ARRAY</td><td>["AUTO_MESSAGES", "MULTI_DIALOG"]</td></tr>
 <tr><td>general</td><td>inOffHours</td><td>&nbsp;</td><td>shift-status of the contact center</td><td>BOOLEAN</td><td>TRUE/FALSE</td></tr>
 <tr><td>general</td><td>visitorId</td><td>&nbsp;</td><td>ID of visitor</td><td>NUMBER</td><td>1528463744580</td></tr>
 <tr><td>general</td><td>originatorId</td><td>&nbsp;</td><td>ID of originator</td><td>NUMBER</td><td>37607275.23</td></tr>
 <tr><td>general</td><td>originatorPid</td><td>&nbsp;</td><td>Pid of originator</td><td>STRING</td><td>f39fbc5f-da77-5417-8bc7-7584efdd1a5e</td></tr>
 <tr><td>general</td><td>originatorMetadata</td><td>id</td><td>Pid of originator of metadata change</td><td>STRING</td><td>f39fbc5f-da77-5417-8bc7-7584efdd1a5e</td></tr>
 <tr><td>general</td><td>originatorMetadata</td><td>role</td><td>Role of originator of metadata change</td><td>STRING</td><td>CONTROLLER</td></tr>
 <tr><td>general</td><td>serverTimestamp</td><td>&nbsp;</td><td>timestamp of the server</td><td>NUMBER</td><td>1528463781807</td></tr>
 <tr><td>general</td><td>clientIpAdress</td><td>&nbsp;</td><td>IP Address of client</td><td>STRING</td><td>172.26.138.38</td></tr>
 <tr><td>general</td><td>manualETTR</td><td>&nbsp;</td><td>time to response manually updated by agent</td><td>STRING</td><td>1541152938069</td></tr>
 <tr><td>general</td><td>lastMessageComposer</td><td>&nbsp;</td><td>the role of the last composer</td><td>STRING</td><td>CONSUMER</td></tr>
 <tr><td>general</td><td>lastMessageTs</td><td>&nbsp;</td><td>timestamp of last message</td><td>NUMBER</td><td>1541152938069</td></tr>
 <tr><td>general</td><td>lastAgentMsgTs</td><td>&nbsp;</td><td>timestamp of last agent message</td><td>NUMBER</td><td>1541152938069</td></tr>
 <tr><td>general</td><td>backToQueueTs</td><td>&nbsp;</td><td>timestamp when the conversation was returned to queue</td><td>NUMBER</td><td>1541152938069</td></tr>
 <tr><td>idle</td><td>lastConsumerMsgTs</td><td>&nbsp;</td><td>timestamp of last consumer message</td><td>NUMBER</td><td>1541152938069</td></tr>
 <tr><td>idle</td><td>agentNonResponsive</td><td>time</td><td>time that should pass after consumer's last message in order the agent to be non-responsive</td><td>NUMBER</td><td>30</td></tr>
 <tr><td>idle</td><td>agentNonResponsive</td><td>timeUnits</td><td>time units in which agent non-responsive time should be calculated</td><td>STRING</td><td>minutes</td></tr>
 <tr><td>idle</td><td>consumserNonResponsive</td><td>time</td><td>time that should pass after agent's last message in order the consumer to be non-responsive</td><td>NUMBER</td><td>30</td></tr>
 <tr><td>idle</td><td>consumserNonResponsive</td><td>timeUnits</td><td>time units in which consumer non-responsive time should be calculated</td><td>STRING</td><td>minutes</td></tr>
 <tr><td>idle</td><td>convNotTakenTime</td><td>time</td><td>time units in which conversation idle time should be calculated</td><td>STRING</td><td>minutes</td></tr>
 <tr><td>idle</td><td>convNotTakenTime</td><td>timeUnits</td><td>how long should the conversation stay in queue in order to be idle</td><td>NUMBER</td><td>30</td></tr>
 <tr><td>mid</td><td>openedInOffHours</td><td>&nbsp;</td><td>indicator if the conversation was opened in off hours</td><td>BOOLEAN</td><td>TRUE/FALSE</td></tr>
 <tr><td>participantChange</td><td>oldParticipants</td><td>&nbsp;</td><td>array of the participants of the previous state</td><td>ARRAY</td><td>[{"id": "f9d58c57-c489-45f5-bae4-c5ebd52b3972","role": "ASSIGNED_AGENT"}]</td></tr>
 <tr><td>participantChange</td><td>newParticipants</td><td>&nbsp;</td><td>array of the participants of the current state</td><td>ARRAY</td><td>[{"id": "f9d58c57-c489-45f5-bae4-c5ebd52b3972","role": "ASSIGNED_AGENT"}, {"id": "f9d58c57-c489-45f5-bae4-c5ebd52b3972","role": "AGENT"}]</td></tr>
 <tr><td>routing</td><td>oldSkillId</td><td>&nbsp;</td><td>previous skillId of conversation</td><td>STRING</td><td>563268</td></tr>
 <tr><td>routing</td><td>newSkillId</td><td>&nbsp;</td><td>current skillId of conversation</td><td>STRING</td><td>563267</td></tr>
 <tr><td>start</td><td>firstConversation</td><td>&nbsp;</td><td>if this is the frist conversation of the consumer ever</td><td>BOOLEAN</td><td>TRUE/ FALSE</td></tr>
 <tr><td>ttr</td><td>oldTtr</td><td>ttrType</td><td>type of ttr of the previous state</td><td>STRING</td><td>NORMAL</td></tr>
 <tr><td>ttr</td><td>oldTtr</td><td>value</td><td>value of ttr of the previous state</td><td>NUMBER</td><td>600</td></tr>
 <tr><td>ttr</td><td>newTtr</td><td>ttrType</td><td>type of ttr of the new state</td><td>STRING</td><td>URGENT</td></tr>
 <tr><td>ttr</td><td>newTtr</td><td>value</td><td>value of ttr of the new state (after change for example to URGENT)</td><td>NUMBER</td><td>300</td></tr>
</tbody></table>
