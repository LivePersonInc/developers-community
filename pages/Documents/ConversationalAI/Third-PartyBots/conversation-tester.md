---
pagename: Conversation Tester
sitesection: Documents
categoryname: "Conversational AI"
documentname: Third-Party Bots
permalink: third-party-bots-conversation-tester.html
indicator: both
---
 
#### Conversation tester.
## Introduction
By using the Conversation tester, you will be able to test your bot and identify if your bot's response has the right configuration.
The Conversation Tester feature aims to help you to identify possible misconfiguration in your bot. This provides three important components. First, the chat window in which you can start testing your bot. Second, the Logs column in which you will see if your bot response was processed or had an error. And finally, the JSON EDITOR column will help you to identify the error cause.
 
## Processed Response
When you are testing your bot and you get a successful response, it means that your bot's response has the correct configuration. See the image below.
<img style="width:800px" src="img/botconnectordashboard/processed_response.png">
 
## Error Response
When testing your bot and you get an error in the response, you will be able to see what was the JSON object that produced the error in your bot response. By hovering on the last alert you will see a tooltip that will give you the possible solutions for your error. See the image below.
 
<img style="width:800px" src="img/botconnectordashboard/error_response.png">
 
### Errors that can be found per vendor
 
### Dialog Flow V2
 
## Dialog Flow V2 Invalid Action Body
## Description
This error happens when the bot has an invalid body and the Google Dialog Flow V2 is unable to parse it. It can be a wrong parameter, a value, or a missing parameter. Even though it is shown as an error in the Third Party Bots, the bot gently ignores unknown actions and the conversation will continue.

## Transfer Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `skill` is the required parameter and it has to be provided as a **String**
- `agentId` is an optional parameter and if provided the value must be a **String**

## Change TTR Action Error 
## Description
This error happens when the required parameter `ttrType` is either not provided or if provided the format of the value is not a **String**


## Close Conversation Action Error
## Description
For this action there are no required parameters. When the withoutPcs optional parameter is provided the format should be **Boolean**

## Faas Invocation Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `lambdaUuid` is a required parameter and it has not being provided as a **String** 
- `payload` is a required parameter and it has not being provided as a **Object** 
- `failOnError` is an optional parameter and it has not being provided as **Boolean** 
 
#### Error Solution
Please check [Change Time To Response of Conversation](third-party-bots-google-dialogflow-version-2.html#change-time-to-response-of-conversation)
 
## Dialog Flow V2 Invalid Text Body
## Description
This error happens when the bot's response has an invalid value in its text message and the vendor is unable to parse the content.
 
## Dialog Flow V2 Invalid Structured Content
## Description
This error happens when the bot's configuration has an invalid content body in its structured content response and the vendor is unable to parse it. It can be a wrong parameter or a value;
 
#### Error Solution
Please check [Sending Rich Content](third-party-bots-google-dialogflow-version-2.html#sending-rich-content-structured-content)
 
## Dialog Flow V2 Invalid Text With Encoded Metadata Body
## Description
This error happens when the bot's configuration has an invalid text message with encoded metadata. It can be that the encodedMetadata property is missing or there is something wrong with the encoded metadata body.
 
#### Error Solution
Please check [Sending Encoded Metadata](third-party-bots-google-dialogflow-version-2.html#sending-encoded-metadata)
 
## Dialog Flow V2 Invalid Delay Body
## Description
This error happens when the bot's response has an invalid delay value and the vendor is unable to parse it. It can be that there is a wrong delay value.
 
#### Error Solution
Please check [Sending Pause/Delay Message](third-party-bots-google-dialogflow-version-2.html#sending-pausedelay-message)
 
## Dialog Flow V2 Invalid Private Text Body
## Description
This error happens when the bot's response has an invalid value in its private text message and the vendor is unable to parse the content. It can be a missing property or a wrong parameter or value.
 
#### Error Solution
Please check [Sending Private Text Message](third-party-bots-google-dialogflow-version-2.html#sending-private-text-message)
 
## Dialog Flow V2 Invalid AI Vendor Response
## Description
This error happens when it was not possible to get any response from the vendor.
 
## Dialog Flow V2 Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Dialog Flow V2 No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.

### DialogFlow CX
 
## DialogFlow CX Invalid Action Body
## Description
This error happens when the bot has an invalid body and the Google Dialog Flow CX is unable to parse it. It can be a wrong parameter, a value, or a missing parameter. Even though it is shown as an error in the Third Party Bots, the bot gently ignores unknown actions and the conversation will continue.

## Transfer Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `skill` is the required parameter and it has to be provided as a **String**
- `agentId` is an optional parameter and if provided the value must be a **String**

## Change TTR Action Error 
## Description
This error happens when the required parameter `ttrType` is either not provided or if provided the format of the value is not a **String**


## Close Conversation Action Error
## Description
For this action there are no required parameters. When the withoutPcs optional parameter is provided the format should be **Boolean**

## Faas Invocation Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `lambdaUuid` is a required parameter and it has not being provided as a **String** 
- `payload` is a required parameter and it has not being provided as a **Object** 
- `failOnError` is an optional parameter and it has not being provided as **Boolean**
 
#### Error Solution
Please check [Change Time To Response of Conversation](third-party-bots-google-dialogflow-cx.html#change-time-to-response-of-conversation)
 
## DialogFlow CX Invalid Text Body
## Description
This error happens when the bot's response has an invalid value in its text message and the vendor is unable to parse the content.
 
## DialogFlow CX Invalid Structured Content
## Description
This error happens when the bot's configuration has an invalid content body in its structured content response and the vendor is unable to parse it. It can be a wrong parameter or a value;
 
#### Error Solution
Please check [Sending Rich Content](third-party-bots-google-dialogflow-cx.html#sending-rich-content-structured-content)
 
## DialogFlow CX Invalid Text With Encoded Metadata Body
## Description
This error happens when the bot's configuration has an invalid text message with encoded metadata. It can be that the encodedMetadata property is missing or there is something wrong with the encoded metadata body.
 
#### Error Solution
Please check [Sending Encoded Metadata](third-party-bots-google-dialogflow-cx.html#sending-encoded-metadata)
 
## DialogFlow CX Invalid Delay Body
## Description
This error happens when the bot's response has an invalid delay value and the vendor is unable to parse it. It can be that there is a wrong delay value.
 
#### Error Solution
Please check [Sending Pause/Delay Message](third-party-bots-google-dialogflow-cx.html#sending-pausedelay-message)
 
## Dialog Flow CX Invalid Private Text Body
## Description
This error happens when the bot's response has an invalid value in its private text message and the vendor is unable to parse the content. It can be a missing property or a wrong parameter or value.
 
#### Error Solution
Please check [Sending Private Text Message](third-party-bots-google-dialogflow-cx.html#sending-private-text-message)
 
## Dialog Flow CX Invalid AI Vendor Response
## Description
This error happens when it was not possible to get any response from the vendor.
 
## Dialog Flow CX Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Dialog Flow CX No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
 
###  Watson Assistant
 
## Watson Assistant Invalid Text Body
## Description
This error happens when the bot's response has an invalid value in its text message and the vendor is unable to parse the content.
 
#### Error Solution
Please check [Text](third-party-bots-ibm-watson-assistant.html#text)
 
 
## Watson Assistant Invalid Structured Content
## Description
This error happens when the bot's configuration has an invalid content body in its structured content response and the vendor is unable to parse it. It can be a wrong parameter or a value;
 
#### Error Solution
Please check [Sending Rich Content](third-party-bots-ibm-watson-assistant.html#sending-rich-content-structured-content)
 
## Watson Assistant Invalid Delay Body
## Description
This error happens when the bot's response has an invalid delay value and the vendor is unable to parse it. It can be that a wrong delay value.
 
#### Error Solution
Please check [Pause/Delay](third-party-bots-ibm-watson-assistant.html#pausedelay)
 
## Watson Assistant Invalid Private Text Body
## Description
This error happens when the bot's response has an invalid value in its private text message and the vendor is unable to parse the content. It can be a missing property or a wrong parameter or value.
 
#### Error Solution
Please check [Sending Private Text Message](third-party-bots-ibm-watson-assistant.html#sending-private-text-message)
 
## Watson Assistant Invalid Message Format
## Description
This error happens when the bot's response has an invalid value in its message and the vendor is unable to parse it. It can be an unknown type or a wrong value.
 
#### Error Solution
Please check [Sending Native Content](third-party-bots-ibm-watson-assistant.html#sending-native-content)
 
## Watson Assistant Invalid Image Body
## Description
This error happens when the bot's response has an invalid property when trying to send an image. The vendor won’t be able to validate the Watson native content image. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Image](third-party-bots-ibm-watson-assistant.html#image)
 
 
## Watson Assistant Invalid Option Body
## Description
This error happens when the bot's response option response type has an invalid body and the vendor is unable to parse it. It can be a wrong parameter or value.
 
#### Error Solution
Please check [List](third-party-bots-ibm-watson-assistant.html#list)
 
## Watson Assistant Invalid Body
## Description
This error happens when the bot's response has an invalid body. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Sending Native Content](third-party-bots-ibm-watson-assistant.html#sending-native-content)
 
## Watson Assistant Invalid AI Vendor Response
## Description
This error happens when there was not possible to get any response from the vendor.
 
## Watson Assistant Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Watson Assistant No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
 
### Watson Assistant V2
 
## Watson Assistant Invalid Text Body
## Description
This error happens when the bot's response has an invalid value in its text message and the vendor is unable to parse the content.
 
#### Error Solution
Please check [Text](third-party-bots-ibm-watson-assistant-version-2.html#text)
 
## Watson Assistant Invalid Structured Content
## Description
This error happens when the bot's configuration has an invalid content body in its structured content response and the vendor is unable to parse it. It can be a wrong parameter or a value;
 
#### Error Solution
Please check [Sending Rich Content](third-party-bots-ibm-watson-assistant-version-2.html#sending-rich-content-structured-content)
 
## Watson Assistant Invalid Delay Body
## Description
This error happens when the bot's response has an invalid delay value and the vendor is unable to parse it. It can be that a wrong delay value.
 
#### Error Solution
Please check [Pause/Delay](third-party-bots-ibm-watson-assistant-version-2.html#pausedelay)
 
## Watson Assistant Invalid Private Text Body
## Description
This error happens when the bot's response has an invalid value in its private text message and the vendor is unable to parse the content. It can be a missing property or a wrong parameter or value.
 
#### Error Solution
Please check [Pause/Delay](third-party-bots-ibm-watson-assistant-version-2.html#sending-private-text-message)
 
## Watson Assistant Invalid Message Format
## Description
This error happens when the bot's response has an invalid value in its message and the vendor is unable to parse it. It can be an unknown type or a wrong value.
 
#### Error Solution
Please check [Sending Native Content](third-party-bots-ibm-watson-assistant-version-2.html#sending-native-content)
 
## Watson Assistant Invalid Image Body
## Description
This error happens when the bot's response has an invalid property when trying to send an image. The vendor won’t be able to validate the Watson native content image. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Image](third-party-bots-ibm-watson-assistant-version-2.html#image)
 
## Watson Assistant Invalid Option Body
## Description
This error happens when the bot's response option response type has an invalid body and the vendor is unable to parse it. It can be a wrong parameter or value.
 
#### Error Solution
Please check [List](third-party-bots-ibm-watson-assistant-version-2.html#list)
 
## Watson Assistant Invalid Body
## Description
This error happens when the bot's response has an invalid body. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Sending Native Content](third-party-bots-ibm-watson-assistant-version-2.html#sending-native-content)
 
## Watson Assistant Invalid AI Vendor Response
## Description
This error happens when there was not possible to get any response from the vendor.
 
## Watson Assistant Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Watson Assistant No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
 

###  Lex
## Lex Invalid Action Body
## Description
This error happens when the bot has an invalid action body and Lex is unable to parse it. It can be a wrong parameter, a value, or a missing parameter. Even though it is showing as an error in the Third Party Bots, the bot gently ignores unknown actions and the conversation will continue.

## Transfer Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `skill` is the required parameter and it has to be provided as a **String**
- `agentId` is an optional parameter and if provided the value must be a **String**

## Change TTR Action Error 
## Description
This error happens when the required parameter `ttrType` is either not provided or if provided the format of the value is not a **String**


## Close Conversation Action Error
## Description
For this action there are no required parameters. When the withoutPcs optional parameter is provided the format should be **Boolean**

## Faas Invocation Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `lambdaUuid` is a required parameter and it has not being provided as a **String** 
- `payload` is a required parameter and it has not being provided as a **Object** 
- `failOnError` is an optional parameter and it has not being provided as **Boolean**

#### Error Solution
Please check [Change Time To Response of Conversation](third-party-bots-amazon-lex.html#change-time-to-response-of-conversation)
 
## Lex Invalid Text Body
## Description
This error happens when the bot's response has an invalid value in its text message and the vendor is unable to parse the content.

#### Error Solution
Please check [Sending Encoded Metadata](third-party-bots-amazon-lex.html#sending-encoded-metadata)
 
## Lex Invalid Structured Content
## Description
This error happens when the bot's configuration has an invalid content body in its structured content response and the vendor is unable to parse it. It can be a wrong parameter or a value;
 
#### Error Solution
Please check [Sending Rich Content](third-party-bots-amazon-lex.html#sending-rich-content-structured-content)
 
 
## Lex Invalid Text With Encoded Metadata Body
## Description
This error happens when the bot's configuration has an invalid text message with encoded metadata. It can be that the encodedMetadata property is missing or the is something wrong with the encoded metadata body.
 
#### Error Solution
Please check [Sending Encoded Metadata](third-party-bots-amazon-lex.html#sending-encoded-metadata)
 
## Lex Invalid Delay Body
## Description
This error happens when the bot's response has an invalid delay value and the vendor is unable to parse it. It can be that a wrong delay value.
 
#### Error Solution
Please check [Sending Pause/Delay Message](third-party-bots-amazon-lex.html#sending-pausedelay-message)
 
## Lex Invalid Private Text Body
## Description
This error happens when the bot's response has an invalid value in its private text message and the vendor is unable to parse the content. It can be a missing property or a wrong parameter or value.
 
#### Error Solution
Please check [Sending Pause/Delay Message](third-party-bots-amazon-lex.html#sending-private-text-message)
 
## Lex Invalid Message Format
## Description
This error happens when the bot's response has an invalid value in its message and the vendor is unable to parse it. It can be an unknown type or a wrong value.
 
## Lex Invalid JSON
## Description
This happens when the bot's response has an invalid JSON and the vendor is unable to parse it. This usually happens when creating a Custom Payload in the bot's response.
 
## Lex Invalid AI Vendor Response
## Description
This error happens when there was not possible to get any response from the vendor.
 
## Lex Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Lex No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
 
###  Microsoft Bot Framework
 
## Microsoft Bot Framework Invalid Body
## Description
This error happens when the bot's response has an invalid body. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Rich Content](third-party-bots-microsoft-bot-framework.html#rich-content-structured-content)
 
## Microsoft Bot Framework Invalid AI Vendor Response
## Description
This error happens when there was not possible to get any response from the vendor.
 
## Microsoft Bot Framework Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Microsoft Bot Framework No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
 
###  Faas
 
## Invalid Action Body
## Description
This error happens when the bot has an invalid action body and Faas is unable to parse it. It can be a wrong parameter, a value, or a missing parameter. Even though it is showing as an error in the Third Party Bots, the bot gently ignores unknown actions and the conversation will continue.

## Transfer Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `skill` is the required parameter and it has to be provided as a **String**
- `agentId` is an optional parameter and if provided the value must be a **String**

## Change TTR Action Error 
## Description
This error happens when the required parameter `ttrType` is either not provided or if provided the format of the value is not a **String**


## Close Conversation Action Error
## Description
For this action there are no required parameters. When the withoutPcs optional parameter is provided the format should be **Boolean**

## Faas Invocation Action Error
## Description
This error happens when either one or multiple of the following conditions not met
- `lambdaUuid` is a required parameter and it has not being provided as a **String** 
- `payload` is a required parameter and it has not being provided as a **Object** 
- `failOnError` is an optional parameter and it has not being provided as **Boolean**
 
#### Error Solution
Please check [Change Time To Response of Conversation](third-party-bots-custom-integration.htmll#change-time-to-response-of-conversation)
 
## Faas Invalid Body
## Description
This error happens when the bot's response has an invalid body. It can be a wrong parameter or value.
 
#### Error Solution
Please check [Sending intent information](third-party-bots-custom-integration.htmll#sending-intent-information)
 
 
## Faas Invalid AI Vendor Response
## Description
This error happens when there was not possible to get any response from the vendor.
 
## Faas Invalid Parsed Response
## Description
This error happens when not parsed messages and actions were found from the vendor.

## Faas No Support for Quick Replies in Chat
## Description
Chat connector does not support quick replies.
