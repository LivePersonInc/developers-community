---
pagename: IBM Watson Assistant
redirect_from:
  - bot-connectors-ibm-watson-assistant.html
sitesection: Documents
categoryname: "Conversational AI"
documentname: Third-Party Bots
permalink: third-party-bots-ibm-watson-assistant.html
indicator:
---

### Overview

The following documentation outlines the configuration for the connector and how to implement functions specifically for **IBM Watson**.

### Bot Configuration

{: .notice}
**IMPORTANT**: All the old bots that use **watsonplatform.net** domain for their workspace URL will fail to operate after **_26 May 2021_**. IBM has deprecated **watsonplatform.net** endpoints please update your bot configuration in Third-Party Bots if you do not want to disrupt the functioning of the bots. Official news on this announcement can be found [here](https://cloud.ibm.com/docs/watson?topic=watson-endpoint-change)

{: .important}
See the [Getting Started](bot-connectors-getting-started.html) guide first to complete pre-requisite steps.

{: .important}
**Please note** that Watson does not support processing newline, tab and carriage-return characters. These symbols will be removed from any query that is sent to Watson via the provided connector.

With watson there are two ways of authentication that currently our system support, these are UserPass and IAM (token based) authentication. You can choose one of them for your bot configuration.

#### UserPass authentication

You will be presented with following screen to complete the Vendor Settings in order to add bot connector using UserPass authentication.

<img class="fancyimage" style="width:600px" src="img/watsonassistant/userpass-based-auth.png">

Figure 1.1 Showing the configuration that needed to be filled using UserPass authentication

Following information needs to be completed for LivePerson:

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
    <td>Workspace URL</td>
    <td>Watson Assistant Workspace URL</td>
    <td>https://api.eu-de.assistant.watson.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>Workspace ID</td>
    <td>Watson Assistant Workspace ID</td>
    <td>8671e9a1-xxxx-xxxx-xxxx-xxxxf9dfcb74</td>
  </tr>
  <tr>
    <td>Conversation Username</td>
    <td>Username of the Watson Assistant conversation</td>
    <td>de0a48a5-9f4f-xxxx-xxxx-xxxxx9856751</td>
  </tr>
  <tr>
    <td>Conversation Password</td>
    <td>password for the Watson Assistant conversation which should be used for the bot</td>
    <td>Dxxxxxxxxxx1</td>
  </tr>
  <tr>
    <td>Version Date</td>
    <td>Version Date of the Watson API</td>
    <td>201X-xx-xx<br><br><br></td>
  </tr>
  </tbody>
</table>

#### IAM authentication

You will be presented with following screen to complete the Vendor Settings in order to add bot connector using IAM authentication.

<img class="fancyimage" style="width:600px" src="img/watsonassistant/token-based-auth.png">

Figure 1.2 Showing the configuration that needed to be filled using IAM authentication authentication

Following information needs to be completed for LivePerson:

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
    <td>Workspace URL</td>
    <td>Watson Assistant Workspace URL</td>
    <td>https://api.eu-de.assistant.watson.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>Workspace ID</td>
    <td>Watson Assistant Workspace ID</td>
    <td>8671e9a1-xxxx-xxxx-xxxx-xxxxf9dfcb74</td>
  </tr>
  <tr>
    <td>API key</td>
    <td>API key which will be used for the Bot's authentication in Watson</td>
    <td>xxxxxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxxxxZG</td>
  </tr>
  <tr>
    <td>Token endpoint url</td>
    <td>URL for creating/refreshing Watson Assistant tokens</td>
    <td>Dxxxxxxxxxx1</td>
  </tr>
  <tr>
    <td>Version Date</td>
    <td>Version Date of the Watson API</td>
    <td>201X-xx-xx<br><br><br></td>
  </tr>
  </tbody>
</table>

#### Test Connection

{: .important}
You have to agree to Data Disclaimer from now onward in order to use the services of bot connector. For that you can click on the checkbox "I agree to the Data Disclaimer

For validation of the credentials provided, you can now perform a test connection request to see if everything that you have provided is working and reachable. You can click on the button "Test Connection" to see if connection succeed or fail. For UserPass authentication see in Figure 1.3 and 1.4. For IAM authentication see in Figure 1.5 and 1.6.

<img class="fancyimage" style="width:600px" src="img/watsonassistant/userpass-connection-success.png">

Figure 1.3 Showing the success case of the valid credentials for UserPass authentication

<img class="fancyimage" style="width:600px" src="img/watsonassistant/userpass-connection-failed.png">

Figure 1.4 Showing the fail case of the invalid credentials for UserPass authentication
<img class="fancyimage" style="width:600px" src="img/watsonassistant/token-connection-success.png">

Figure 1.5 Showing the success case of the valid credentials for IAM authentication

<img class="fancyimage" style="width:600px" src="img/watsonassistant/token-connection-failed.png">

Figure 1.6 Showing the fail case of the invalid credentials for IAM authentication

<div class="notice">
Please be careful while providing credentials that you have selected the right workspace URL. Selecting the wrong Watson Assistant gateway causes connection failure.
</div>

Once you are done with providing configuration you can save it by pressing on "Done". **_Congratulations!_** You have completed the configuration of the Watson Assistant bot.

Please note that your bot should be capable of handling unsupported messages either via fallback intents or [as your design pleases](https://cloud.google.com/dialogflow/es/docs/intents-default). This will ensure the success of the call to the API of Lex for testing the connection.

{: .important}
Following guide is going to present customization for the Watson Assistant on how to implement functions specifically for **IBM Watson**. It is intended for users who are familiar with IBM Watson cloud dashboard. Continue if you are familiar and have access to IBM Watson cloud dashboard.

### Sending Native Content

Watson Assistant allows the user to define native response types to the dialog nodes. The supported Watson Assistant native types include Image, List, Pause, and Text. Users can define single or multiple native content per dialog. The native content types can be defined with Watson wizard or using the JSON editor (Figure 2.1 shows how to access both ways in IBM Watson website).

<img class="fancyimage" style="width:100%" src="img/watsonassistant/watson-json-editor.png">

Figure 2.1 IBM Watson Native Rich Content Wizard and JSON Editor

{: .important}
**Please note** that Watson assistant API version of `2018-09-20` is used to support the native content response in Third-Party Bots.

If you use **JSON Editor** then the usual body of the native content is as follows:

```javascript
{
  "output": {
    "generic": [
      // Here comes array of objects of different Watson native contents that you can define.
    ]
  }
}
```

#### Image

User can define Image type using the IBM watson assistant dashboard. To do this, dialog node will need to selected that will hold image response. Click on the "Add response type" and select Image from the select box as shown in Figure 2.1.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Image-Select-Response.png">

Figure 2.1 Response type of Image is highlighted

Once image is selected you will be asked to fill the information. "Image Source" url must be provided. You can also describe the image title and description (example filled form is shown in the Figure 2.2).

{: .important}
If Images are sent in Rich content, then their URLs must be added to a whitelist via internal LivePerson configuration (Houston: `messaging.rich.content.valid.urls`). Please note that you must add all possible domains to this list manually as wildcards are not supported. Moreover, All domains must be HTTPS secure.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Image-Fields-Response.png">

Figure 2.2 Image fields filled example

If you are using **JSON editor** you can add a Image type by posting following JSON. Please make sure to change **"source"**, **"title"** and **"description"** property with your data.

```json
{
  "output": {
    "generic": [
      {
        "source": "https://images.pexels.com/photos/699122/pexels-photo-699122.jpeg",
        "title": "iPhone 8 Concept",
        "description": "iPhone 8 concept image showing initial details about phone",
        "response_type": "image"
      }
    ]
  }
}
```

#### List

User can define List type using the IBM watson assistant dashboard. To do this, dialog node will need to selected that will hold list response. Click on the "Add response type" and select Option from the select box as shown in Figure 2.3.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Option-Select-Response.png">

Figure 2.3 Response type of List is highlighted

Once the "Option" is selected the form need to be filled will be shown. You must provide "Title" and also "Description". Furthermore, different choices of options can be added via clicking "Add option" button. Once the button is clicked you will be asked to put a label of option and value. Make sure you fill both of them (example filled form shown in Figure 2.4).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Option-Fields-Response.png">

Figure 2.4 List fields filled example

If you are using **JSON Editor** then you have following structure of List. Note that **"options"** property is array of objects which holds the items for choosing are presented to user.

```javascript
{
  "output": {
    "generic": [
      {
        "title": "",
        "description": "",
        "options": [
          // Here comes the list of options you want to present to user
        ],
        "response_type": "option"
      }
    ]
  }
}
```

An example list filled with two options can be seen below. Please note that within options object, "text" **(value->input->text)** is the value that you set for an option.

```json
{
  "output": {
    "generic": [
      {
        "title": "Choose your Phone",
        "description": "Select the phone you like",
        "options": [
          {
            "label": "iOS",
            "value": {
              "input": {
                "text": "1"
              }
            }
          },
          {
            "label": "Android",
            "value": {
              "input": {
                "text": "2"
              }
            }
          }
        ],
        "response_type": "option"
      }
    ]
  }
}
```

#### Pause/Delay

Users can define Pause type if they want to send some delay in responding. For adding this content type, the dialog node will need to select that will hold pause response. Click on the "Add response type" and select Pause option as shown in Figure 2.5

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Pause-Select-Response.png">

Figure 2.5 Response type of Pause is highlighted

Once the "Pause" is selected the form will ask you to provide the duration (unit is in milliseconds). This allows the conversation to be paused for the amount of time defined in "Duration" field. Moreover, If you want to show user a indication of typing you can select choose that with Typing Indicator radio box. (example filled form is shown in Figure 2.6). This will show a indication like "Agent is typing..." for the amount of time of delay that is set in "Duration".

**Note:** using the delay as a single/sole response from the bot to the consumer, is effectively a ‘no response’ action. Using this allows the bot to receive a consumer message without responding to the consumer.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Pause-Fields-Response.png">

Figure 2.6 Pause fields filled example

If you are using **JSON Editor** you can use the following JSON structure to define a Pause content type. This example will pause for 5 milliseconds with typing indication on.

```json
{
  "output": {
    "generic": [
      {
        "time": 5,
        "typing": true,
        "response_type": "pause"
      }
    ]
  }
}
```

#### Text

Users can define a Text type to send some textual response. For adding this type dialog node will need to select that will hold text response. Click on the "Add response type" and select "Text" option as shown in Figure 2.7

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Text-Select-Response.png">

Figure 2.7 Response type of Text is highlighted

Once the "Text" is selected the form will allow you to add the response texts. You can add multiple responses variation (example filled form is shown in Figure 2.8).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Text-Fields-Response.png">

Figure 2.8 Text fields filled example

If you are using **JSON Editor** you can use following JSON structure to create text responses. The example below shows two text responses defined that will come sequentially.

```json
{
  "output": {
    "generic": [
      {
        "response_type": "text",
        "values": [
          {
            "text": "Hi Good Morning!"
          },
          {
            "text": "Hi Good Evening!"
          }
        ],
        "selection_policy": "sequential"
      }
    ]
  }
}
```

#### Defining multiple responses with Watson Native content

Users can define a response with various content types. The following example shows a similar case using **JSON Editor**. The response will First send the text. afterwards, it will make a pause for 5 seconds and then finally sends an image.

```json
{
  "output": {
    "generic": [
      {
        "values": [
          {
            "text": "Hi Good Morning!"
          },
          {
            "text": "Hi Good Evening!"
          }
        ],
        "response_type": "text",
        "selection_policy": "sequential"
      },
      {
        "time": 5000,
        "typing": true,
        "response_type": "pause"
      },
      {
        "title": "iPhone 8",
        "source": "https://cdn.bgr.com/2016/08/iphone-8-concept.jpg",
        "description": "iPhone 8 concept",
        "response_type": "image"
      }
    ]
  }
}
```

### Sending Rich Content (Structured Content)

{: .important}
**Please note** that Watson assistant API version of `2018-09-20` is used to support the rich content response in Third-Party Bots.

The core Conversational Cloud platform supports the use of rich/structured content. For more information on the format and functionality available, please refer to the documentation found [here](getting-started-with-rich-messaging-introduction.html). As a result, the Bot Connector also supports this.

To send structured content via Watson Assistant you will need send custom JSON. To do this, you will need to select the dialog node that will hold the structured content (Figure 3.1).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/dialognode.png">

Figure 3.1 Watson Dialog Node

From there, under the section Then respond with: Click the three vertical dots and select Open JSON Editor (Figure 3.2)

<img class="fancyimage" style="width:500px" src="img/watsonassistant/dialogjsoneditor.png">

Figure 3.2 Watson Assistant Dialog JSON Editor

In the JSON Editor you will need to add your custom JSON response (Figure 3.3).

<img class="fancyimage" style="width:500px" src="img/watsonassistant/jsoneditor.png">

Figure 3.3 Watson Assistant JSON Editor

There is a strict JSON structure for the response that must be used. The JSON structure can be found below in **Figure 3.4**. An example with a sample JSON that uses a standard Structured Content card with a button option in can be seen in **Figure 3.5**.

```json
{
  "output": {
    "text": {
      "values": [
        {
          "metadata": [
            {
              "id": "1234",
              "type": "ExternalId"
            }
          ],
          "structuredContent": {}
        }
      ],
      "selection_policy": "sequential"
    }
  }
}
```

Figure 3.4 Structured Content Watson JSON Structure (JSON Editor should contain this object structure for Rich Content)

```json
{
  "output": {
    "text": {
      "values": [
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
          }
        }
      ],
      "selection_policy": "sequential"
    }
  }
}
```

Figure 3.5 Structured Content Watson JSON Example (JSON Editor should contain this object structure for Rich Content)

For new IAM workspaces that have a new Watson response, _Then respond with_ "text" should be used:

<img class="fancyimage" style="width:400px" src="img/watsonassistant/image_5.png">

Put the structured content objects that is shown in Figure 3.6 with the metadata in the text field. Figure 3.7 shows the final picture of how it should look like.

```json
{
  "metadata": [{ "id": "1234", "type": "ExternalId" }],
  "structuredContent": {
    "type": "vertical",
    "elements": [
      {
        "type": "button",
        "click": {
          "actions": [
            { "text": "Recommend me a movie, please", "type": "publishText" }
          ]
        },
        "title": "Recommend a movie"
      }
    ]
  }
}
```

Figure 3.6 Structured Content Watson JSON Example (IAM)

### Sending Quick Replies (Structured Content)

{: .important}
**Please note** Quick Replies are only supported in Messaging Conversations.

Quick Replies are a special kind of the Structured Content.
The content should be added to the quickReplies property of the structuredContent object and there also a message be included in the structuredContent object.
This message will be sent to the customer along with the Quick Replies.
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
    "message": "Message to send before sending QuickReplies content"
  },
  "metadata": [
    {
      "id": "1234",
      "type": "ExternalId"
    }
  ]
}
```

Figure 3.7 Quick Replies StructuredContent example.

### Change Time To Response of Conversation

Change the TTR of a conversation based on the action response of Watson. There have 3 different types. "URGENT", "NORMAL", "PRIORITIZED". The time values of these are defined in the Agent Workspace.


```json
{
  "output": {
    "text": {
      "values": ["Sure thing! Change the TTR to Urgent."],
      "selection_policy": "sequential"
    }
  },
  "actions": [
    {
      "name": "CHANGE_TTR",
      "type": "CLIENT",
      "parameters": {
        "ttrType": "URGENT"
      },
      "result_variable": "none"
    }
  ]
}
```

Figure 4.1 Watson JSON response for changing TTR

### Transfer/Escalations

<div class="notice">
<strong>Naming Conventions:</strong> Before going into <strong>actions</strong> and <strong>skills</strong> is the naming convention between each.

All non-escalation actions are defined by using underscores. For example, in the case of closing a conversation, the action name returned by <strong>Watson</strong> needs to be <strong>CLOSE_CONVERSATION</strong>. Further down the line, if any additional functionality is added that can be called by an action from the AI, it will follow the same naming convention.

For escalations, the naming convention for these skills should use a "-" instead of "\_". Furthermore, if transferring to a skill, specifically assigned to bots, it’s best practice to prefix the skill name with "BOT-" within Conversational Cloud.

</div>

#### Transfer To Skill

This option transfers the conversation to the next available agent using the provided skill. 

At the beginning of a chat session or when a messaging bot logs in, all the list of enabled skills on the account are retrieved, keyed by name and stored. When a transfer is requested by the bot, the target skill's name is searched inthe stored list and its ID is retrieved and escalated to. In regards to **Watson Assistant**, this should be configured in the following way:

Parameters: ‘skill’ **(Case sensitive)** with ‘value’ of skill name (case sensitive) in Conversational Cloud.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/image_6.png">

Figure 4.1

```json
{
  "output": {
    "text": {
      "values": ["Escalating to a human"]
    }
  },
  "actions": [
    {
      "name": "TRANSFER",
      "type": "client",
      "parameters": {
        "skill": "human_skill"
      },
      "result_variable": "none"
    }
  ]
}
```

In the example above, you can see the `actions` array. Inside the array, we defien an escalation skill name in the `skill` parameter. This will be sent in an object to the chat/messaging connector, which will grab the `skillId` from a previously stored array based on the name, and escalate.

#### Transfer to Agent

{: .important}
This feature is depending on [permissions](contact-center-management-messaging-operations-transfer-to-agent.html)

This option transfers the conversation to the particular agent matching the provided agentId and skill. If the agent is not available, the conversation will be transfered to an available agent with the same skill

Parameters: ‘skill’ **(Case sensitive)** with ‘value’ of skill name (case sensitive) in Conversational Cloud.
‘agentId **(Case sensitive)** with ‘value’ of agentId in Conversational Cloud.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/image_7.png">

Figure 4.2

In the _Then respond with:_ JSON editor block, use the following:

```json
{
  "output": {
    "text": {
      "values": ["Escalating to an agent"]
    }
  },
  "actions": [
    {
      "name": "TRANSFER",
      "type": "client",
      "parameters": {
        "skill": "human_skill",
        "agentId": "4129463410"
      },
      "result_variable": "none"
    }
  ]
}
```

### Close Chat/Conversation

To close a chat or messaging conversation, we utilize the action object as we did for a transfer (see **Figure 5.1**). In **Figure 6.1** below, the **Watson Assistant** JSON response should be mirrored as follows:

```json
{
  "output": {
    "text": {
      "values": ["Thanks for chatting with us today!"],
      "selection_policy": "sequential"
    }
  },
  "actions": [
    {
      "name": "CLOSE_CONVERSATION",
      "type": "client",
      "result_variable": "none"
    }
  ]
}
```

Figure 6.1 Watson Assistant JSON response for closing chat/conversation

To close a conversation without triggering a post conversation survey, see the example below:

```json
{
  "output": {
    "text": {
      "values": ["Thanks for chatting with us today!"],
      "selection_policy": "sequential"
    }
  },
  "actions": [
    {
      "name": "CLOSE_CONVERSATION",
      "type": "client",
      "parameters": {
        "withoutPcs": true
      },
      "result_variable": "none"
    }
  ]
}
```

Figure 6.2 Watson Assistant JSON response for closing conversations without pcs

### Invoke LivePerson Function

During a conversation, it is possible to trigger a LivePerson Function that is deployed to the [LivePerson Functions](liveperson-functions-overview.html) (Function as a Service) platform. This provides a way to run custom logic with a bot.

To invoke a LivePerson Function, we utilize the action object as we did for a transfer (see **Figure 5.1**). In **Figure 7.1** below, the **Watson Assistant** JSON response should be mirrored as follows:

```json
{
  "output": {
    "text": {
      "values": [
        "Trigger LivePerson Function"
      ]
    }
  },
  "actions": [
    {
      "name": "INVOCATION",
      "type": "client",
      "parameters": {
        "lambdaUuid": "4ec49ffc-080b-4e59-b302-18d6b826191b",
        "payload": "{ "some": "stuff"}",
        "failOnError": true

      },
      "result_variable": "none"
    }
  ]
}
```

Figure 7.1 Watson Assistant JSON response for invoking LivePerson Function

To retrieve the **_lambdaUuid_** of your LivePerson Function follow [this guide](liveperson-functions-external-invocations-client-credentials.html#step-4-get-the-lambda-uuid-from-functions)

In addition, it is possible to send your own payload to the function. Set your content inside the **payload** parameter

The bot does not escalate on a failed invocation by default. To enable this, set the additional parameter **failOnError** to **true**

### Engagement attributes as context

Third-Party bots allows the collection of engagement attributes (more information can be found [here](engagement-attributes-types-of-engagement-attributes.html)) if `Engagement Attributes` option is checked in the `Conversation Type` step as shown in Figure 8.1.

<img class="fancyimage" style="width:750px" src="img/engagement_attr_select.png">
Figure 8.1 Conversation Type step in creation/modification of bot configuration.

These attributes are **only** collected at the start of a conversation. Third-Party bots leverage the LivePerson Visit Information API to collect the engagement attributes, Further information Visit Information API can be found [here](visit-information-api-visit-information.html). Moreover, Engagement attributes are not updated throughout the life cycle of a conversation and only passed along with each message request. In Watson Assistant V1 these engagement attributes are added to the property `lpSdes`. For the preservation of these attributes within a conversation, `context` property is used (further information about `context` can be found [here](https://cloud.ibm.com/apidocs/assistant-v1#get-response-to-user-input)). An example of the request body can be seen below:

```javascript
{
  "message": "Some Message",
  "context": {
    // ... contains some more information about conversation as well
    "lpEvent": {}, // Holds LP Events
    "lpSdes": {}
  }
}
```

### Sending Encoded Metadata

Conversational Cloud Messaging platform provides a new metadata input type (“encodedMetadata”) for passing a base64 encoded metadata on a conversation. The new metadata input type is in addition to the existing [conversation metadata](messaging-agent-sdk-conversation-metadata-guide.html) input field. Third-party Bot also supports this property and this section will cover the information needed for you to send encoded metadata within your conversations. Before sending encoded metadata you must ensure the following conditions in order to successfully send the data.

<ul>
  <li><b>Common.EncodedMetadata</b> AC feature is ON</li>
  <li>Content is base64 encoded</li>
  <li> Metadata size is limited to 5k</li>
</ul>

{: .important}
Failing to comply with the above validation points will cause the message to be dropped. This feature is only available for the messaging conversations not for chat conversations

Encoded Metadata can be sent with simple Text, Rich Content (structured content) and Multiple responses. The `encodedMetadata` can be defined with context editor or using the JSON editor(Figure 9.1). In both ways, Third-Party Bot leverages the context variables to send the encoded metadata. The encoded metadata is passed throughout the conversation responses unless it is overwritten by upcoming `encodedMetadata`. Then the upcoming `encodedMetadata` will be passed along the responses.

  <img class="fancyimage" style="width:800px" src="img/watsonassistant/context_adding_choices.png">
  Figure 8.1 Showing context editor with the encoded metadata.

{: .important}
Be careful with the camel-case characters `encodedMetadata` you must provide it exactly the same.

#### Sending Watson Native Content with Encoded Metadata

Sending encoded metadata with the Native Content (Text, Image and Options) is possible using Watson `context editor` or also through the `JSON editor`. An example response definition for both ways can be seen below:

  <img class="fancyimage" style="width:800px" src="img/watsonassistant/watson_encoded_metadata_context_editor.png">
  Figure 9.2 Showing context editor with the encoded metadata.

<br />

Example response body for `JSON editor`:

```json
{
  "output": {
    "generic": [
      {
        "values": [
          {
            "text": "This is text with encoded metadata"
          }
        ],
        "response_type": "text",
        "selection_policy": "sequential"
      }
    ]
  },
  "context": {
    "encodedMetadata": "ewoiaWQiOiAidGV4dCIKfQ=="
  }
}
```

#### Sending Rich Content (structured content) with Encoded Metadata

Sending encoded metadata with the Native Content is possible using Watson `context editor` or also through the `JSON editor`. An example response definition for both ways can be seen below:

  <img class="fancyimage" style="width:800px" src="img/watsonassistant/watson_encoded_metadata_with_structured_content.png">
  Figure 9.3 Showing context editor with the encoded metadata.

<br />

```json
{
  "output": {
    "text": {
      "values": [
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
          }
        }
      ],
      "selection_policy": "sequential"
    }
  },
  "context": {
    "encodedMetadata": "ewoiaWQiOiAic2MiCn0="
  }
}
```

If you have a different context for multiple dialogs in a conversation that are responding with structure content, then you can define the `encodedMetadata` for each of the dialog separately. In that case, you will not define `encodedMetadata` via context editor or inside `context` property if using JSON editor. Below example shows where `encodedMetadata` property should be placed in structured content. Please note you will have to use JSON editor for defining such case:

```json
{
  "output": {
    "text": {
      "values": [
        {
          "encodedMetadata": "ewoiaWQiOiAic2MiCn0=",
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
          }
        }
      ],
      "selection_policy": "sequential"
    }
  },
  "context": {}
}
```

### Sending Private Text Message

It is possible to send a private text message from the Live Engage (LE-UI) via agent workspace. This feature can now be used via the Third-Party bots as well. This will allow Brands to define private message text within the conversational flow of the bot. These messages are published into the conversation for other Agent/Manger participants. This enables Brands to customize messages giving more insight, summarizing actions taken by the bot, or also advising on next actions the handover agent should take.

{: .important}
Please note If you have not migrated to new Agent Workspace you will not be able to see the `Private` message indicator in the conversation window. Nevertheless, private text messages will not be shown to the consumer and only remain visible to Agents and Managers.

Please note private text message will never be shown to the consumer and will be visible only inside the conversation window of agent workspace. The private text message can be added via Watson's `JSON editor` (as shown in Figure 9.1). There are two properties, `text` and `messageAudience` required for sending a private text message.

| key             | value                                 | notes                     |
| --------------- | ------------------------------------- | ------------------------- |
| text            | any string value                      | mandatory                 |
| messageAudience | value should be "AGENTS_AND_MANAGERS" | case sensitive, mandatory |

<br />

<img class="fancyimage" style="width:800px" src="img/watsonassistant/context_adding_choices.png">
Figure 10.1 Showing JSON editor option access via Watson Assistant.

It is possible to send only a private text message response. The example payload of such response is below (also Figure 9.2 `JSON Editor` view):

```json
{
  "output": {
    "text": {
      "values": [
        {
          "text": "This is a private text",
          "messageAudience": "AGENTS_AND_MANAGERS"
        }
      ],
      "selection_policy": "sequential"
    }
  }
}
```

<img class="fancyimage" style="width:800px" src="img/watsonassistant/private_message_response_custom_payload.png">
Figure 10.2 Showing single private text message definition inside `JSON Editor`

It is also possible to send a private text message with the action (e.g. Transfer / Escalations). Example payload of such a case (Private Text Message - Action) will be as below:

```json
{
  "output": {
    "text": {
      "values": [
        {
          "text": "This is a private text",
          "messageAudience": "AGENTS_AND_MANAGERS"
        }
      ]
    }
  },
  "actions": [
    {
      "name": "TRANSFER",
      "type": "client",
      "parameters": {
        "skill": "human_skill"
      },
      "result_variable": "none"
    }
  ]
}
```

### Watson Discovery

Discovery Search is a tool that uses the knowledge of websites, documents and other data, to generate an answer the Watson Bot is able to send within a conversation. If enabled, the bot searches for matching parts of the provided information on specified intents or in case no machtching intent was found.

To use Watson Discovery the Watson Assistant Bot needs to have a s[search skill](https://www.ibm.com/cloud/architecture/content/course/integrate-ibm-watson-assistant-and-watson-discovery/create-a-search-skill) linked to a [Watson Discovery Instance](https://www.ibm.com/cloud/architecture/content/course/integrate-ibm-watson-assistant-and-watson-discovery/create-a-watson-discovery-instance)

### Limitations

<ul>
  <li>Currently IBM Watson allows <b>only 5</b> response types per node.</li>
</ul>
