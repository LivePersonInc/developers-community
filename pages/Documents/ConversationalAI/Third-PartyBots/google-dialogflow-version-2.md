---
pagename: Google Dialogflow Version 2
redirect_from:
  - bot-connectors-google-dialogflow-version-2.html
sitesection: Documents
categoryname: "Conversational AI"
documentname: Third-Party Bots
permalink: third-party-bots-google-dialogflow-version-2.html
indicator:
---

### Overview

The following documentation outlines the configuration for the connector and how to implement functions specifically for **Google Dialogflow Version 2**.

### Bot Configuration

{: .important}
See the [Getting Started](bot-connectors-getting-started.html) guide first to complete pre-requisite steps.

You will be presented with following screen to complete the Vendor Settings in order to add bot connector.

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/wizard.png">

Figure 1.1 Showing the configuration that needed to be filled

The following Dialogflow V2 information should be provided to LivePerson:

<table>
  <thead>
  <tr>
    <th>Item</th>
    <th>Description</th>
    <th>Example</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>Language code</td>
    <td>Language code for Dialogflow</td>
    <td>en-US</td>
  </tr>
  <tr>
    <td>Project ID</td>
    <td>Dialogflow project id</td>
    <td>bxx-xxxxxxx-xxx-dialogflow-v2</td>
  </tr>
  <tr>
    <td>User email address</td>
    <td>Email address of the Google Service account</td>
    <td>dialogflow-xxxxxx@bxx-xxxxxxx-xxx-dialogflow-v2.iam.gserviceaccount.com</td>
  </tr>
   <tr>
    <td>Service location</td>
    <td>Location of the Dialogflow API Backend</td>
    <td>us-dialogflow.googleapis.com</td>
  </tr>
  <tr>
    <td>User private key</td>
    <td>Private key of the IAM Account, please keep the formatting as provided by Google</td>
    <td>
            -----BEGIN PUBLIC KEY-----<br />
            MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC/HqnexoEA38Gl1Oqpdmx8vTpb
            /cck+/OQddeak8cwMM0GJB7ueNQICw9O1jSR5nMb5qCGheEYW3akz9b2cucGzx2t
            ZiyZpyOxtkvBNiD0eoB1L5arCyy4Foa2z1vfq6TSwnJFehn5DeCFpAviUS2jIDPU
            cyADqtL+DnALuNDy8wIDAQAB
            <br />-----END PUBLIC KEY-----
    </td>
  </tr>
  <tr>
    <td>Google Cloud scopes</td>
    <td>Authentication scopes of the used IAM role</td>
    <td>https://www.googleapis.com/auth/cloud-platform</td>
  </tr>
  </tbody>
</table>

**NOTE**: Dialogflow V2 adheres to Google’s oAuth2 unlike the V1 implementation. Some degree of familiarity with Google IAM policies and IAM console is necessary for setting up a valid Dialogflow V2 client with _Read Only API access_. A _service account_ is a **prerequisite** for setting up the above config. Documentation available [here](https://dialogflow.com/docs/reference/v2-auth-setup).

The expected output of a service account setup is a JSON file, example below:

**Format of JSON file containing credentials**

```json
{
  "type": "service_account",
  "project_id": "[PROJECT-ID]",
  "private_key_id": "[KEY-ID]",
  "private_key": "-----BEGIN PRIVATE KEY-----\n[PRIVATE-KEY]\n-----END PRIVATE KEY-----\n",
  "client_email": "[SERVICE-ACCOUNT-EMAIL]",
  "client_id": "[CLIENT-ID]",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "Client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/[SERVICE-ACCOUNT-EMAIL]"
}
```

Figure 1.2

**NOTE**: The config wizard expects each of the pieces of auth data to be copied from the JSON file, without quotes. For the private_key especially, do not modify the string, do not remove any of the newline characters. Just copy and paste directly.

{: .important}
You have to agree to Data Disclaimer from now onward in order to use the services of bot connector. For that you can click on the checkbox "I agree to the Data Disclaimer"

For validation of the credentials provided, you can now perform a test connection request to see if everything that you have provided is working and reachable. You can click on the button "Test Connection" to see if connection succeed or fail as shown in Figure 1.4 and 1.5 respectively. Please note that your bot should be capable of handling unsupported messages either via [fallback intents](https://cloud.google.com/dialogflow/es/docs/intents-default) or as your design pleases. This will ensure the success of the call to the API of Lex for testing the connection.

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/wizard_success.png">

Figure 1.4 Showing the success case of the valid credentials

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/wizard_failed.png">

Figure 1.5 Showing the fail case of the invalid credentials

Once you are done with providing configuration you can save it by pressing on "Done". **_Congratulations!_** You have completed the configuration of the Google DialogFlow V2 bot.

{: .important}
Following guide is going to introduce how to implement functions specifically for **Dialogflow V2** using [Dialogflow console](https://console.dialogflow.com/api-client/). Continue if you are familiar and have access to [Dialogflow console](https://console.dialogflow.com/api-client/).

### Limitations

#### Dialogflow V2 Query length Limit

<div class="notice">
The Dialogflow V2 service has a <a href="https://dialogflow.com/docs/reference/agent/query" target="_blank">limitation</a> on the length of the ‘query’ property. Any query longer than 255 characters will invoke a custom event in Dialogflow.
To handle this gracefully, we recommend building a simple intent that handles a ‘DIALOGFLOW_CHAR_LIMIT’ *event*.
</div>

1. Create an intent with an event using the string: DIALOGFLOW_CHAR_LIMIT

   <img style="width:600px" src="img/dialogflowversion2/image_7.png">

   Figure 2.1

2. Do not forget to add a custom response in the **Text response** section.

   <img style="width:700px" src="img/dialogflowversion2/image_8.png">

   Figure 2.2

### Welcome Event

The behaviour of the welcome event is different depending on whether the bot is for chat and messaging. This divergence comes down to the way that each individual Liveperson product works..

A Messaging conversation qualifies as "initiated" from a Conversational Cloud perspective only after the consumer sends their first message. The consumer is prompted for their initial message in the channel they have chosen to initiate the conversation. As a result, the consumer’s first message is something that can be parsed by Dialogflow V2 and an intent determined.

The below documents cover where to configure the initial message on a given platform.

<table>
  <thead>
    <tr>
      <th>Platform</th>
      <th>Docs</th>
      <th>Attribute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>iOS</td>
      <td>https://developers.liveperson.com/consumer-experience-ios-sdk-localizationkeys.html</td>
      <td>hiMessage</td>
    </tr>
    <tr>
      <td>Android</td>
      <td>https://developers.liveperson.com/android-modifying-string.html#resultOverlayRecordTemplate</td>
      <td>lp_first_message</td>
    </tr>
    <tr>
      <td>Web</td>
      <td>N/A</td>
      <td>Default LP Message</td>
    </tr>
    <tr>
      <td>Other</td>
      <td>N/A</td>
      <td>N/A</td>
    </tr>
  </tbody>
</table>

A Chat conversation is considered started when the chat is routed to an agent. Best practice is for the agent to provide the first response.
In this scenario, there is no text from the consumer to parse, thus the default ‘WELCOME’ event is utilised as a start point for the bot to prompt the user to provide input and progress the conversation.

Ensure you have an ‘entry point’ intent that utilises the default ‘WELCOME’ event.

<img class="fancyimage" style="width:550px" src="img/dialogflowversion2/image_6.png">

Figure 3.1

### Change Time To Response of Conversation

Change the TTR of a conversation based on the **action** value in the response object.

LivePerson Messaging uses 3 different types of priorities:
"URGENT",
“NORMAL”
“PRIORITIZED”

The time values of these are defined in the Agent Workspace.

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/image_9.png">

Figure 3.2

### Transfer / Escalations

If the bot needs to transfer the conversation to a human agent, or the conversation flow indicates that another bot is better suited for the identified intent, you will need to tell the connector to transfer the conversation to a given skill.

This is achieved using the built in "Actions and Parameters" section of the Dialogflow console.

Multiple scenarios for transfer/escalations exist triggered by the transfer action object.

1. Explicit request from visitor to transfer to an agent (Eg, action : transfer)

2. If the Bot does not have an appropriate answer, it should recognise this as a scenario for a transfer.
   Depending on the connector configuration or the decision making capacity of the bot, the bot will transfer to a particular agent, skill or default skill.

3. If there is a internal error or the bot service cannot be reached the connector will transfer to a default skill set up during configuration.

Transfers and escalations rely on the _action_ item in the response object.

Action: **TRANSFER (Case sensitive)**

#### Transfer To Skill

This option transfers the conversation to the next available agent using the provided skill. 

Parameters: ‘skill’ **(Case sensitive)** with ‘value’ of skill name (case sensitive) in Conversational Cloud.

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/image_10.png">

Figure 4.1

#### Transfer to Agent

{: .important}
This feature is depending on [permissions](contact-center-management-messaging-operations-transfer-to-agent.html)

This option transfers the conversation to the particular agent matching the provided agentId and skill. If the agent is not available, the conversation will be transfered to an available agent with the same skill

Parameters: ‘skill’ **(Case sensitive)** with ‘value’ of skill name (case sensitive) in Conversational Cloud.
‘agentId **(Case sensitive)** with ‘value’ of agentId in Conversational Cloud.

<img class="fancyimage" style="width:600px" src="img/dialogflowversion2/image_14.png">

Figure 4.2

### Sending Rich Content (Structured Content)

Structured Content/Rich Content is supported by the core LivePerson platform. Documentation for the feature can be found [here](getting-started-with-rich-messaging-introduction.html).

To send Structured Content via Dialogflow V2, send a _custom payload_ option via an intent.

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/image_11.png">

Figure 5.1

{: .important}
If Images are sent in Rich content, then their URLs must be added to a whitelist via internal LivePerson configuration (Houston: `messaging.rich.content.valid.urls`). Please note that you must add all possible domains to this list manually as wildcards are not supported. Moreover, All domains must be HTTPS secure.

This should contain valid structured content, along with any optional metadata required for the structured content (as seen in Figure 5.1). Always validate your structured content using [this tool](https://livepersoninc.github.io/json-pollock/editor/) before entering into the Dialogflow console.

**NOTE:** Caution when creating a custom payload. Delete the existing text response before saving the intent. If not Conversational Cloud will receive a blank text response followed by rich content payload.

Example Metadata

```javascript
{
  "metadata": [
    {
      //Mandatory
      "type": "ExternalId", //Mandatory
      "id": "ABCD1234" //Mandatory
    }
  ],
  "structuredContent": {
    //Mandatory
    "type": "vertical",
    "elements": [
      {
        "type": "image",
        "url": "https://i.ytimg.com/vi/zmeByDJ02mQ/hqdefault.jpg",
        "tooltip": "image tooltip"
      },
      {
        "type": "text",
        "text": "product name (Title)",
        "tooltip": "product name (Title)"
      },
      {
        "type": "text",
        "text": "product category (type)",
        "tooltip": "product category (type)"
      },
      {
        "type": "text",
        "text": "$155.99",
        "tooltip": "$155.99"
      }
    ]
  }
}
```

Figure 5.2 Dialogflow Example Custom Payload

### Sending Quick Replies (Structured Content)

{: .important}
**Please note** Quick Replies are only supported in Messaging Conversations.

Quick Replies is a special type of Structured Content. It is a message sent along with predefined answers.
For detailed information on Quick Replies check out the documentation for the specific channel ([Mobile SDK and Web](mobile-sdk-and-web-templates-quick-replies-template.html), [Facebook Messenger](facebook-messenger-templates-quick-replies-template.html), [Google RCS Business Messaging](google-rcs-business-messaging-templates-quick-replies-template.html)).

```json
{
  "structuredContent": {
    "quickReplies": {
      "type": "quickReplies",
      "itemsPerRow": 8,
      "replies": [
        {
          "type": "button",
          "tooltip": "yes i do",
          "title": "yes",
          "click": {
            "actions": [
              {
                "type": "publishText",
                "text": "yep"
              }
            ],
            "metadata": [
              {
                "type": "ExternalId",
                "id": "Yes-1234"
              }
            ]
          }
        },
        {
          "type": "button",
          "tooltip": "No!",
          "title": "No!",
          "click": {
            "actions": [
              {
                "type": "publishText",
                "text": "No!"
              }
            ],
            "metadata": [
              {
                "type": "ExternalId",
                "id": "No-4321"
              }
            ]
          }
        }
      ]
    },
    "message": "Do you like Bots?"
  },
  "metadata": [
    {
      "id": "1234",
      "type": "ExternalId"
    }
  ]
}
```

Figure 6.1 QuickReplies Structured Content example

### Sending Encoded Metadata

Conversational Cloud Messaging platform provides a new metadata input type (“encodedMetadata”) for passing a base64 encoded metadata on a conversation. The new metadata input type is in addition to the existing [conversation metadata](messaging-agent-sdk-conversation-metadata-guide.html) input field. Third-party Bot also supports this property and this section will cover the information needed for you to send encoded metadata within your conversations. Before sending encoded metadata you must ensure the following conditions in order to successfully send the data.

<ul>
  <li><b>Common.EncodedMetadata</b> AC feature is ON</li>
  <li>Content is base64 encoded</li>
  <li> Metadata size is limited to 5k</li>
</ul>

{: .important}
Failing to comply with the above validation points will cause the message to be dropped. This feature is only available for the messaging conversations not for chat conversations

Encoded Metadata can be sent with simple Text, Rich Content (structured content) and Multiple responses. For sending encoded metadata as a Text or Rich Content message you must use `Custom Response` type for your relevant intent as shown in Figure 7.1 below

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/dialogflow_encoded_metadata.png">
Figure 7.1

#### Sending Text Message with Encoded Metadata

Please note that the default `Text Response` option in Dialogflow will not work with encoded metadata feature. You have to use Custom Response with the properties `textResponse` and `encodedMetadata`. Be careful with the camel-case characters you must provide it exactly the same.

<ul>
  <li> <b>textResponse</b>: This is the text that will be sent to the user.</li>
  <li><b>encodedMetadata</b>: this is the property that will contain encoded metadata</li>
</ul>

An example of the custom payload text message response is below:

```json
{
  "textResponse": "Hello I am a text response with encoded metadata!",
  "encodedMetadata": "ewoic29tZUluZm8iOiAiSSB3YXMgZW5jb2RlZCIKfQ=="
}
```

<br />

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/dialogflow_encodedmetadata_text.png">
Figure 7.2 
 
#### Sending Rich Content (structured content) with Encoded Metadata

You need to add another property of `encodedMetadata` with your rich content object that you have created. An example of the simple Rich Content `JSON` can be seen below:

```json
{
  "metadata": [
    {
      "id": "1234",
      "type": "ExternalId"
    }
  ],
  "structuredContent": {
    "type": "vertical",
    "elements": [
      {
        "type": "button",
        "click": {
          "actions": [
            {
              "text": "Recommend me a movie, please",
              "type": "publishText"
            }
          ]
        },
        "title": "Recommend a movie"
      }
    ]
  },
  "encodedMetadata": "ewoic29tZUluZm8iOiAiSSB3YXMgZW5jb2RlZCIKfQ=="
}
```

<br />

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/dialogflow_encodedmetadata_structuredcontent.png">
Figure 7.3

### Sending Pause/Delay Message

It is possible to send an event of type "delay" before regular content events and actions. This specifies the time the bot will wait before displaying the next message. The delay message can be added via the Custom Payload response in intent definition (as shown in Figure 8.1). There are two properties, `delay` and `typing`, which are a part of the Custom Payload response.

<ul>
  <li> <b>delay</b>: This is the number of seconds the bot will wait. These are expected to be only whole numbers for example for one second delay you will write 1 as a value</li>
  <li><b>typing</b>: This property will enable/disable the typing indicator while delay is happening. It is optional; if not provided then the value will be considered as true.</li>
</ul>

<br />

Setting a delay in between multiple messages is possible and an example of such a case (Message - Delay - Message) can be seen in Figure 8.1.

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/dialogflow_message_delay_message.png">
Figure 8.1 An example of Message - Delay - Message  configuration in the Dialogflow console's intent editor

It is possible to send only a single delay response. The example payload of such response is below:

```json
{
  "delay": 8,
  "typing": false
}
```

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/delay_response_custom_payload.png">
Figure 8.2 showing the Custom Markup message for delay message

**Note:** using the delay as a single/sole response from the bot to the consumer, is effectively a ‘no response’ action. Using this allows the bot to receive a consumer message without responding to the consumer.

### Sending Private Text Message

It is possible to send a private text message from the Live Engage (LE-UI) via agent workspace. This feature can now be used via the Third-Party bots as well. This will allow Brands to define private message text within the conversational flow of the bot. These messages are published into the conversation for other Agent/Manger participants. This enables Brands to customize messages giving more insight, summarizing actions taken by the bot, or also advising on next actions the handover agent should take.

{: .important}
Please note If you have not migrated to new Agent Workspace you will not be able to see the `Private` message indicator in the conversation window. Nevertheless, private text messages will not be shown to the consumer and only remain visible to Agents and Managers.

Please note private text message will never be shown to the consumer and will be visible only inside the conversation window of agent workspace. The private text message can be added via the Custom Payload response in intent definition (as shown in Figure 9.1). There are two properties, `text` and `messageAudience`, which are part of the Custom Payload response.

| key             | value                                 | notes                     |
| --------------- | ------------------------------------- | ------------------------- |
| text            | any string value                      | mandatory                 |
| messageAudience | value should be "AGENTS_AND_MANAGERS" | case sensitive, mandatory |

<br />

Setting a private text message between multiple messages is also possible. Moreover, it is also possible to send a private text message with the combination of actions(e.g. Transfer / Escalations) as well. Example of such a case (Message - Private Text Message - Action) can be seen in Figure 9.1.

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/private_message_response_custom_payload.png">
Figure 9.1 An example of transfer action with a simple text message and private text message in the Dialogflow console's intent editor

It is possible to send only a private text message response. The example payload of such response is below:

```json
{
  "messageAudience": "AGENTS_AND_MANAGERS",
  "text": "This is a private message for agent from DialogFlow"
}
```

### Close Chat/Conversation

In the bot’s flow, there will be times when it is appropriate to end the conversation without escalating to a live agent.
If a query has been answered, or the brand has determined that no escalation is required for a given query, then it is best practice to have the bot end the conversation.

The method for closing a conversation is similar to the transfer action in that the same "Actions and Parameters" field is utilised in the Dialogflow console.

The action field needs to be set to **CLOSE_CONVERSATION** to instruct the connector to close the conversation.

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/image_12.png">
Figure 10.1

To close a conversation without triggering a post conversation survey, please add the parameter with the name `withoutPcs` and the value `true` to the action parameters.

### Invoke LivePerson Function

During a conversation, it is possible to trigger a LivePerson Function that is deployed to the [LivePerson Functions](liveperson-functions-overview.html) (Function as a Service) platform. This provides a way to run custom logic with a bot.

The method for triggering an invocation is similar to the transfer action in that the same "Actions and Parameters" field is utilised in the Dialogflow console.

The action field needs to be set to **INVOCATION** to instruct the connector to invoke the sepecified LivePerson Function

It is also required to provide the **lambdaUuid** of the function that should be invoked in parameters.
To retrieve the Lambda UUID of your LivePerson Function follow [this guide](liveperson-functions-external-invocations-client-credentials.html#step-4-get-the-lambda-uuid-from-functions)

In addition, it is possible to send your own payload to the function. Set your content inside the **payload** key.

The bot does not escalate on a failed invocation by default. To enable this, set the additional parameter **failOnError** to **true**

<img class="fancyimage" style="width:800px" src="img/dialogflowversion2/image_13.png">
Figure 11.1

### Engagement attributes as context

Third-Party bots allows the collection of engagement attributes (more information can be found [here](engagement-attributes-types-of-engagement-attributes.html)) if `Engagement Attributes` option is checked in the `Conversation Type` step as shown in Figure 12.1.

<img class="fancyimage" style="width:750px" src="img/engagement_attr_select.png">
Figure 12.1 Conversation Type step in creation/modification of bot configuration.

These attributes are **only** collected at the start of a conversation. Third-Party bots leverage the LivePerson Visit Information API to collect the engagement attributes, Further information Visit Information API can be found [here](visit-information-api-visit-information.html). Moreover, Engagement attributes are not updated throughout the life cycle of a conversation and only passed along with each message request. For DialogFlow V2 these engagement attributes are added to the property `lpSdes` that is sub-property of the `payload` (more information about `payload` parameter can be found [here](https://googleapis.dev/nodejs/dialogflow/latest/google.cloud.dialogflow.v2.html#.QueryParameters)). An example of the request body can be seen below:

```javascript
{
  "session": "SomeSession",
  "queryParams": {
    "payload": {
      "lpEvent": {}, // Holds LP Events
      "lpSdes": {}
    }
  }
}
```

### Limitations

- Currently, We send all the intents received from Dialogflow V2 via `alternativeQueryResults`. This is only possible if Knowledge Connectors are enabled and set up, otherwise, this field will be empty until multiple responses for regular intents are supported. For more information, you can refer to the official documentation [here](https://cloud.google.com/dialogflow/es/docs/reference/rest/v2beta1/DetectIntentResponse)
