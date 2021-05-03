---
pagename: IBM Watson Assistant Version 2
redirect_from:
sitesection: Documents
categoryname: "Conversational AI"
documentname: Third-Party Bots
permalink: third-party-bots-ibm-watson-assistant-version-2.html
indicator:
---

### Overview

The following documentation outlines the configuration for the bot connector and how to implement functions specifically for **IBM Watson Assistant Version 2**.

### Bot Configuration

{: .notice}
**IMPORTANT**: All the old bots that use **watsonplatform.net** domain for their workspace URL will fail to operate after **_26 May 2021_**. IBM has deprecated **watsonplatform.net** endpoints please update your bot configuration in Third-Party Bots if you do not want to disrupt the functioning of the bots. Official news on this announcement can be found [here](https://cloud.ibm.com/docs/watson?topic=watson-endpoint-change)

{: .important}
See the [Getting Started](bot-connectors-getting-started.html) guide first to complete pre-requisite steps.

{: .important}
**Please note** that Watson does not support processing newline, tab and carriage-return characters. These symbols will be removed from any query that is sent to Watson via the provided connector.

{: .notice}
**IMPORTANT**: In case of inactivity, the Watson Assistant session only last 5 minutes for the Lite/Standard plans and up to 60 minutes for Plus/Premium plans. Because of the asynchronous nature of messaging, it could take longer until the user replies to the bot agent. In case the Watson session expires, the bot connector will create a new conversation session on the Watson side [More Info](https://cloud.ibm.com/docs/services/assistant?topic=assistant-dialog-runtime#dialog-runtime-context).

### Authentication

With Watson there are two methods of authentication that are currently supported. These methods are username/password and IAM (token based) authentication. You can choose either one for your bot configuration but IAM is **highly recommended** (as it is more secure).

#### Username/Password authentication

You will be presented with following screen to complete the Vendor Settings in order to add the bot connector using username/password authentication.

<img class="fancyimage" style="width:600px" src="img/watsonassistantv2/userpass-based-auth.png">

Figure 1.1 Showing the configuration that needs to be filled out when using username/password authentication

You need to fill in the following infromation:

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
    <td>Watson Assistant Workspace URL. Note that this workspace URL changes according to your account. In order to figure out which URL is correct for you, check the location of your Assistant in IBM's Cloud console. Then, choose the corresponding URL based on geo-location. For example, if your IBM location is "eu-gb", the London URL is the correct one for you.</td>
    <td>https://api.eu-de.assistant.watson.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>Assistant ID</td>
    <td>Watson Assistant Assistant ID. Retrievable from the settings of your Watson Assistant.</td>
    <td>8671e9a1-xxxx-xxxx-xxxx-xxxxf9dfcb74</td>
  </tr>
  <tr>
    <td>Username</td>
    <td>Username for the Watson Assistant conversation. Retrievable from the settings of your Watson Assistant.</td>
    <td>de0a48a5-9f4f-xxxx-xxxx-xxxxx9856751</td>
  </tr>
  <tr>
    <td>Password</td>
    <td>password for the Watson Assistant conversation which should be used for the bot</td>
    <td>Dxxxxxxxxxx1</td>
  </tr>
  </tbody>
</table>

#### IAM authentication

You will be presented with following screen to complete the Vendor Settings in order to add the bot connector using IAM authentication.

<img class="fancyimage" style="width:600px" src="img/watsonassistantv2/token-based-auth.png">

Figure 1.2 Showing the configuration that needs to be filled in when using the IAM authentication method.

You need to fill in the following infromation:

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
    <td>Watson Assistant Workspace URL. Note that this workspace URL changes according to your account. In order to figure out which URL is correct for you, check the location of your Assistant in IBM's Cloud console. Then, choose the corresponding URL based on geo-location. For example, if your IBM location is "eu-gb", the London URL is the correct one for you.</td>
    <td>https://api.eu-de.assistant.watson.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>Assistant ID</td>
    <td>Watson Assistant ID</td>
    <td>8671e9a1-xxxx-xxxx-xxxx-xxxxf9dfcb74. Retrievable from the settings of your Watson Assistant.</td>
  </tr>
  <tr>
    <td>API key</td>
    <td>API key which will be used for the Bot's authentication in Watson. Retrievable from the settings of your Watson Assistant.</td>
    <td>xxxxxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxxxxZG</td>
  </tr>
  <tr>
    <td>Token endpoint url</td>
    <td>URL for creating/refreshing Watson Assistant tokens. Leave as is.</td>
    <td>Dxxxxxxxxxx1</td>
  </tr>
  </tbody>
</table>

#### Test Connection

{: .important}
You have to agree to a Data Disclaimer from this point on in order to use the bot connector. To agree to the disclaimer, click on the checkbox "I agree to the Data Disclaimer" at the bottom of the configuration menu.

To validate the credentials you provided above, you can now perform a test connection request. Click on the "Test Connection" button to do so. For UserPass authentication see in Figure 1.3 and 1.4. For IAM authentication see in Figure 1.5 and 1.6.

<!-- <img class="fancyimage" style="width:600px" src="img/watsonassistant/userpass-connection-success.png">

Figure 1.3 Showing the success case of the valid credentials for UserPass authentication

<img class="fancyimage" style="width:600px" src="img/watsonassistant/userpass-connection-failed.png">

Figure 1.4 Showing the fail case of the invalid credentials for UserPass authentication
<img class="fancyimage" style="width:600px" src="img/watsonassistantv2/token-connection-success.png">

Figure 1.5 Showing the success case of the valid credentials for IAM authentication

<img class="fancyimage" style="width:600px" src="img/watsonassistantv2/token-connection-failed.png">

Figure 1.6 Showing the fail case of the invalid credentials for IAM authentication -->

Please note that your bot should be capable of handling unsupported messages either via fallback intents or [as your design pleases](https://cloud.google.com/dialogflow/es/docs/intents-default). This will ensure the success of the call to the API of Lex for testing the connection.

<div class="notice">
Please be careful while providing credentials that you have selected the right workspace URL. Selecting the wrong Watson Assistant gateway causes connection failure. See the note in the table above for more information on finding the correct workspace URL
</div>
Once you are done with the configuration and the connection test succeded, you can save your configuration by pressing on "Done".

**Congratulations!** You have completed the configuration of the Watson Assistant bot.

{: .important}
The following guide is presetns customization for the Watson Assistant. It is intended for users who are familiar with the IBM Watson cloud dashboard. Continue if you are familiar and have access to the IBM Watson cloud dashboard.

### Sending Native Content

The Watson Assistant allows the user to define native response types to the dialog nodes. The supported Watson Assistant native types include Image, List, Pause, and Text. Users can define single or multiple native content types per dialog. The native content types can be defined with the Watson dashboard UI or directly by using the JSON editor (Figure 2.1 shows how to access both methods in the IBM Watson dashboard).

<img class="fancyimage" style="width:100%" src="img/watsonassistant/watson-json-editor.png">

Figure 2.1 IBM Watson Native Rich Content Wizard and JSON Editor

{: .important}
**Please note** that the Watson Assistant API version from `2018-09-20` is used to support the native content response in our connectors.

If you use the **JSON Editor** then the default body of the native content is as follows:

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

Users can configure the Image native type using the IBM watson assistant dashboard. To do this, a dialog node will need to selected that will hold the image response. Click on the "Add response type" and select `Image` from the select box as shown in Figure 2.1.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Image-Select-Response.png">

Figure 2.1 Response type of Image is highlighted

Once `image` is selected, you will be asked to fill in the information for the specific image you want to use. The `Image Source` URL must be provided. You can also fill in the image title and description (example filled form is shown in the Figure 2.2).

{: .important}
If Images are sent in Rich content, then their URLs must be added to a whitelist via internal LivePerson configuration. Please contact your account team to do so. Please note that you must add all possible domains to this list manually as wildcards are not supported. Moreover, all image domains must be HTTPS secure.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Image-Fields-Response.png">

Figure 2.2 Image fields filled example

If you are using the **JSON editor**, you can add an Image native type by posting the following JSON. Please make sure to change the `source`, `title` and `description` properties within your data.

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

Users can define the List native type using the IBM Watson assistant dashboard. To do this, a dialog node will need to selected that will hold the list response. Click on the "Add response type" and select `Option` from the select box as shown in Figure 2.3.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Option-Select-Response.png">

Figure 2.3 Response type of List is highlighted

Once `Option` is selected the form which needs to be filled out will be shown. You must provide the `Title` and `Description` fields. Furthermore, an additional option can be added by clicking the "Add option" button. Once the button is clicked you will be asked to add the option's label and value. Make sure you provide both of them (example filled form shown in Figure 2.4).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Option-Fields-Response.png">

Figure 2.4 List fields filled example

If you are using the **JSON Editor** use the below structure to create a list. Note that the `options` property is an array of objects which holds the different choices presented to the user.

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

An example list populated with two options can be seen below. Please note that within options object,`text` **(value->input->text)** is the content that you set for an option.

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

Users can configure the Pause type if they want to create a delay in the bot's responses. You will need to first select a node which will create the delay. Click on the "Add response type" and select the Pause option as shown in Figure 2.5

**Note:** using the delay as a single/sole response from the bot to the consumer is effectively a ‘no response’ action. Using this allows the bot to receive a consumer message without responding to the consumer.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Pause-Select-Response.png">

Figure 2.5 Response type of Pause is highlighted

Once Pause is selected, the form will ask you to provide the duration for the pause (in milliseconds). Moreover, if you want to show user an indication that the bot is typing, you can do that by selecting the Typing Indicator radio box. This will show an indication like "Agent is typing..." for the length of the pause.

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Pause-Fields-Response.png">

Figure 2.6 Pause fields filled example

If you are using **JSON Editor** you can use the following JSON structure to define a Pause content type. This example will pause for 5 milliseconds with the typing indication on.

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

Users can define a Text native type to send textual responses to the consumer. To add this type, a dialog node will need to be selected that will hold text response. Click on the "Add response type" and select the "Text" option as shown in Figure 2.7

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Text-Select-Response.png">

Figure 2.7 Response type of Text is highlighted

Once Text is selected, the form will allow you to add the response you wish to send. You can add multiple responses variation (example filled form is shown in Figure 2.8).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/Text-Fields-Response.png">

Figure 2.8 Text fields filled example

If you are using the **JSON Editor** you can use the following JSON structure to create text responses. The example below shows two text responses defined that will follow each other sequentially.

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

Users can define a response with various content types. The following example shows using the **JSON Editor** to do so. First, the text response will be sent. Then, a 5 second delay will follow. Finally, an image will be sent.

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
**Please note** that the Watson assistant API version from `2018-09-20` is used to support the rich content response in the connector.

The core Conversational Cloud platform supports the use of rich/structured content. For more information on the format and functionality available, please refer to the documentation found [here](getting-started-with-rich-messaging-introduction.html). As a result, the Bot Connector also supports this.

To send structured content via Watson Assistant you will need to send custom JSON. To do this, you will need to first select the dialog node that will hold the structured content (Figure 3.1).

<img class="fancyimage" style="width:850px" src="img/watsonassistant/dialognode.png">

Figure 3.1 Watson Dialog Node

From there, under the section "Then respond with": Click the three vertical dots and select Open JSON Editor (Figure 3.2)

<img class="fancyimage" style="width:500px" src="img/watsonassistant/dialogjsoneditor.png">

Figure 3.2 Watson Assistant Dialog JSON Editor

In the JSON Editor you will need to add your custom JSON response (Figure 3.3).

<img class="fancyimage" style="width:500px" src="img/watsonassistant/jsoneditor.png">

Figure 3.3 Watson Assistant JSON Editor

There is a strict JSON structure for the response that must be used. The JSON structure can be found below in **Figure 3.4**. An example with a sample JSON structure that uses a standard Structured Content card with a button option can be seen in **Figure 3.5**.

##### Figure 3.4 Structured Content Watson JSON Structure (JSON Editor should contain this object structure for Rich Content)

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

##### Figure 3.5 Structured Content Watson JSON Example (JSON Editor should contain this object structure for Rich Content)

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

#### Structured Content Watson JSON Example (IAM)

For new IAM workspaces that have a new Watson response, _Then respond with_ "text" should be used:

<img class="fancyimage" style="width:400px" src="img/watsonassistant/image_5.png">

Put the structured content objects that is shown in the below example alongside the metadata in the `text` field. Figure 3.7 shows the final picture of how it should look like.

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

To use [Quick Replies](quick-replies-introduction-to-quick-replies.html), we require a special formatting of the structured content.
The quick replies rich content should be added to the `quickReplies` property of the `structuredContent` object, and also a message should be included.

This message will be sent to the customer along with the quick replies.

{: .noice}
**Please note** Quick Replies are only supported in Messaging Conversations.

##### Figure 3.7 Quick Replies StructuredContent structure.

```javascript
{
  "structuredContent": {
    "quickReplies": {
      // insert quickReplies rich content here as described here
      //https://developers.liveperson.com/quick-replies-introduction-to-quick-replies.html
      "type": "quickReplies",
      "replies": [...],
      "itemsPerRow": 8
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

Figure 3.8 Watson Quick Replies StructuredContent example.

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
          }
        }
      ],
      "selection_policy": "sequential"
    }
  }
}
```

### Change Time To Response of Conversation

Change the TTR of a conversation based on the action response of Watson. There are 3 different types of Time to Response states: "URGENT", "NORMAL", "PRIORITIZED".

The time values of these are defined in the Agent Workspace.

##### Figure 4.1 Watson JSON response for changing TTR

```json
{
  "output": {
    "text": {
      "values": ["Sure thing! Change the TTR to URGENT."],
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

### Transfer/Escalations

<div class="notice">
<strong>Naming Conventions:</strong> Before going into <strong>actions</strong> and <strong>skills</strong>, we'll need to define the naming conventions used for either.

All non-escalation actions are signified by using underscores. For example, in the case of closing a conversation, the action name returned by <strong>Watson</strong> needs to be <strong>CLOSE_CONVERSATION</strong>.

For escalations, the naming convention for the skills you escalate should use a "-" instead of whitespace. Furthermore, if transferring to a skill specifically assigned to bots, it’s best practice to prefix the skill name with "BOT-" within the Conversational Cloud.

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

In the example above, you can see the `actions` array. Inside the array, we defien an escalation skill name in the  `skill` parameter. This will be sent in an object to the chat/messaging connector, which will grab the `skillId` from a previously stored array based on the name, and escalate.

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

To close a chat or messaging conversation, we utilize the action object as we did for a transfer (see example above). In the example below, the **Watson Assistant** JSON response should be used as follows:

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

To close a messaging conversation without triggering post conversation survey please provide the `withoutPcs` flag with the value true in the action parameters:

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

### Invoke LivePerson Function

During a conversation, it is possible to trigger a LivePerson Function that is deployed to the [LivePerson Functions](liveperson-functions-overview.html) (Function as a Service) platform. This provides a way to run custom logic with a bot.

To invoke a LivePerson Function, we utilize the action object as we did for a close chat/conversation (see example above). In the example below, the **Watson Assistant** JSON response should be mirrored as follows:

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

To retrieve the **_lambdaUuid_** of your LivePerson Function follow [this guide](liveperson-functions-external-invocations-client-credentials.html#step-4-get-the-lambda-uuid-from-functions)

In addition, it is possible to send your own payload to the function. Set your content inside the **payload** parameter

The bot does not escalate on a failed invocation by default. To enable this, set the additional parameter **failOnError** to **true**

### Engagement attributes as context

Third-Party bots allow the collection of engagement attributes (more information can be found [here](engagement-attributes-types-of-engagement-attributes.html)) if the `Engagement Attributes` option is checked in the `Conversation Type` step as shown in Figure 7.1.

<img class="fancyimage" style="width:750px" src="img/engagement_attr_select.png">
Figure 7.1 Conversation Type step in creation/modification of bot configuration.

These attributes are **only** collected at the start of a conversation. Third-Party bots leverage the LivePerson Visit Information API to collect the engagement attributes. Further information on the Visit Information API can be found [here](visit-information-api-visit-information.html). Moreover, Engagement attributes are not updated throughout the life cycle of a conversation and only passed along with each message request. In Watson Assistant V2 these engagement attributes are added to the property `lpSdes`. For the preservation of these attributes within a conversation, the `context` property is used (further information about `context` can be found [here](https://cloud.ibm.com/docs/assistant?topic=assistant-api-client-get-context)). An example of the request body can be seen below:

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

The Conversational Cloud Messaging platform provides a new metadata input type (`encodedMetadata`) for passing a base64 encoded metadata during a conversation. The new metadata input type is in addition to the existing [conversation metadata](messaging-agent-sdk-conversation-metadata-guide.html) input field. Third-party bots also support this property and this section will cover the information needed for you to send encoded metadata within your conversations. Before sending encoded metadata you must ensure the following conditions in order to successfully send the data.

<ul>
  <li><b>The feature is turned on for your account. Contact your account team if this is not the case.</b></li>
  <li>Content is base64 encoded.</li>
  <li> Metadata size is limited to 5kb.</li>
</ul>

{: .important}
Failing to comply with the above will cause the message to be dropped. This feature is only available for messaging conversations.

Encoded Metadata can be sent alongside a simple Text response, a Rich Content (structured content) response and Multiple responses. The `encodedMetadata` can be defined with the context editor or using the JSON editor(Figure 8.1). In both methods, the Third-Party bot leverages the context variables to send the encoded metadata. The encoded metadata is passed throughout the conversation responses unless it is overwritten by a new `encodedMetadata` object.

  <img class="fancyimage" style="width:800px" src="img/watsonassistantv2/context_adding_choices.png">
  Figure 8.1 Showing context editor with the encoded metadata.

#### Sending Watson Native Content with Encoded Metadata

Sending encoded metadata with Native Content (Text, Image and Options) is possible using the Watson `context editor` or also through the `JSON editor`. An example response definition for both methods can be seen below:

  <img class="fancyimage" style="width:800px" src="img/watsonassistantv2/watson_encoded_metadata_context_editor.png">
  Figure 8.2 Showing context editor with the encoded metadata.

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

Sending encoded metadata with the Native Content is possible using the Watson `context editor` or also through the `JSON editor`. An example response definition for both methods can be seen below:

  <img class="fancyimage" style="width:800px" src="img/watsonassistantv2/watson_encoded_metadata_with_structured_content.png">
  Figure 8.3 Showing context editor with the encoded metadata.

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

If you have a different context for multiple dialogs in a conversation that are using structured content, then you can define the `encodedMetadata` for each of the dialog separately. In that case, you will not define `encodedMetadata` via the context editor or inside the `context` property if using JSON editor. The below example shows where the `encodedMetadata` property should be placed in structured content for such cases. Please note you will have to use the JSON editor in this case:

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

It is possible to send a private text message in the Conversational Cloud agent workspace. This feature can also be used via Third-Party bots. This will allow brands to define private message texts within the conversational flow of the bot. These messages are published into the conversation and visible only to Agent/Manger participants. This enables Brands to customize messages giving more insight, summarizing actions taken by the bot, or advising on next actions the handover agent should take.

{: .important}
Please note: if you have not migrated to new Agent Workspace you will not be able to see the `Private` message indicator in the conversation window. Nevertheless, private text messages will not be shown to the consumer and remain visible only to Agents and Managers.

The private text message can be added via Watson's `JSON editor` (as shown in Figure 9.1). There are two properties, `text` and `messageAudience` required for sending a private text message.

| key             | value                                 | notes                     |
| --------------- | ------------------------------------- | ------------------------- |
| text            | any string value                      | mandatory                 |
| messageAudience | value should be "AGENTS_AND_MANAGERS" | case sensitive, mandatory |

<img class="fancyimage" style="width:800px" src="img/watsonassistantv2/context_adding_choices.png">
Figure 9.1 Showing JSON editor option access via Watson Assistant.

It is possible to send only a private text message response in a node. The example payload of such response is below (also Figure 9.2 `JSON Editor` view):

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

<img class="fancyimage" style="width:800px" src="img/watsonassistantv2/private_message_response_custom_payload.png" />
Figure 9.2 Showing single private text message definition inside JSON Editor

It is also possible to send a private text message with an action (e.g. Transfer / Escalations). An example payload or such a case is below:

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

- Currently IBM Watson Assistant retains sessions only for 5 minutes for Free and 60 minutes for Plus or premium members. For more information [read here](https://cloud.ibm.com/docs/services/assistant?topic=assistant-dialog-runtime#dialog-runtime-context)
- Currently IBM Watson allows **only 5** response types per node.
