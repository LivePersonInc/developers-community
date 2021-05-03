---
pagename: Bot Conversation Errors
sitesection: Documents
categoryname: "Conversational AI"
documentname: Third-Party Bots
permalink: third-party-bots-bot-conversation-errors.html
indicator: both
---

## Introduction

This document describes possible errors which can be thrown during a conversation, with the reason for the error and the solution to fix the error.

### com.liveperson.bot-connectors-worker.error.connector.messaging.send-message

#### Description

This error indicates that the message could not be send to the conversation

#### Reasons

The reason for this is mostly wrong formatted structured content. Another issue could be missing url whitelisting for images

#### Solutions

Please check [structured content](getting-started-with-rich-messaging-introduction.html)

### com.liveperson.bot-connectors-worker.error.connector.messaging.end-conversation

#### Description

This error indicates an issue with closing a messaging conversation.

#### Reasons

This usually happens if the conversation was already closed/transferred while the bot is evaluating the response.

#### Solutions

None.

### com.liveperson.bot-connectors-worker.error.connector.messaging.change-ttr

#### Description

This error indicates an issue in changing the TTR value for the current conversation.

#### Reasons

Mostly, the error is a wrong value which is used for the TTL

#### Solutions

Please choose the right value for your TTR step.
See the documentation for the individual vendors on how to set TTR properly

### com.liveperson.bot-connectors-worker.error.connector.messaging.transfer-to-skill

#### Description

This happens if the bot could not transfer the conversation to the desired messaging skill.

#### Reasons

Usually, this happens if there is an issue within the Liveperson APIs. Another reason could be that the customer has already closed the conversation.

#### Solutions

None.

### com.liveperson.bot-connectors-worker.error.connector.messaging.conversation-closed

#### Description

This happens if the bot tries to send commands to an already closed conversation.

#### Reasons

Usually, this happens if there is an issue within the Liveperson APIs. Another reason could be that the customer has already closed the conversation.

#### Solutions

None.

### com.liveperson.bot-connectors-worker.error.connector.messaging.agent-not-authorized

#### Description

This happens if the bot tried to send a command to a conversation which is not assigned to the bot anymore.

#### Reasons

Usually, this happens if there is an issue within the Liveperson APIs. Another reason could be that the customer has already closed the conversation or the conversation was transferred to a new agent in the meantime

#### Solutions

None.

### com.liveperson.bot-connectors-worker.error.connector.chat.send-message

#### Description

This happens if the bot could not send a message to a chat conversation

#### Reasons

Mostly the structured content format is wrong, so please double-check this.

#### Solutions

Please check [structured content](getting-started-with-rich-messaging-introduction.html)

### com.liveperson.bot-connectors-worker.error.connector.chat.end-conversation

#### Description

This happens if a chat conversation could not be closed by the bot.

#### Reasons

Usually, this happens if the conversation was already closed by the consumer in the meantime.

#### Solutions

None.

### com.liveperson.bot-connectors-worker.error.connector.chat.transfer-to-skill

#### Description

This happens if a chat conversation could not be transferred to the desired chat skill.

#### Reasons

For chat conversations, there must be an agent available with the desired skill to transfer and also available slots.

#### Solutions

If this issue happens frequently, increase the capacity for the desired chat skill

### com.liveperson.bot-connectors-worker.error.pipes.messaging-handle-bot-action.transfer-skill-not-existing

#### Description

This happens if the provided skill in the action parameters is not valid.

#### Reasons

The skill name provided in the action parameters can not be found on the lp account.

#### Solutions

Double-check that the skill exists on your account and also check the spelling, it's case sensitive.

### com.liveperson.bot-connectors-worker.error.pipes.verify-ai-response.missing-action-and-messages

#### Description

This error is thrown if the response of the AI Vendor does not contain any action nor messages.

#### Reasons

Since the bot does not know how to behave without any AI Vendor feedback, we are throwing an error.

#### Solutions

Make sure that your AI Vendor has a valid response for every user input.

### com.liveperson.bot-connectors-worker.error.pipes.verify-ai-response.no-messages-and-not-supported-action

#### Description

This error is thrown if the response of the AI Vendor does not contain any messages and the provided actions are not supported by our bot connector.

#### Reasons

Since the bot does not know how to behave without any AI Vendor feedback, we are throwing an error.

#### Solutions

Make sure that your AI Vendor has a valid response for every user input.

### com.liveperson.bot-connectors-worker.error.pipes.verify-ai-response.quick-replies-not-supported

#### Description

This happens if the AI Vendor returns a quickReplies response for a chat conversation.

#### Reasons

QuickReplies are only supported for Messaging Conversations

#### Solutions

Do not send QuickReplies to Chat Conversations

### com.liveperson.bot-connectors-worker.error.pipes.conversation-limit-checker.max-conv-limit-reached

#### Description

The bot does not accept new conversation anymore and instead error escalates them.

#### Reasons

To ensure the stability of our service, a bot can have a maximum number of 999 open conversations assigned.

#### Solutions

Add more bots to support handling such kind of load, you can check how to add a bot [here](third-party-bots-getting-started.html)

### com.liveperson.bot-connectors-worker.error.events-queue.not-catched-pipeline-error

#### Description

This error indicates that there is an unknown error while processing the consumer event.

#### Reasons

Mostly implementation errors on our end.

#### Solutions

Please reach out to LivePerson Support and provide the exact error details. You can do this by clicking copy on the relevant error.

### com.liveperson.bot-connectors-worker.error.aivendor.dialogflowv2.send-query

#### Description

Could not send a query to DialogFlow.

#### Reasons

Mostly issues with DialogFlow APIS.

#### Solutions

Double-check you have enough credits left for your Dialogflow account.
Check for any interruption on Dialogflow side.

### com.liveperson.bot-connectors-worker.error.aivendor.dialogflowcx.send-request

#### Description
Could not send a request to DialogFlow CX.
#### Reasons
Mostly issues with DialogFlow CX APIS.
#### Solutions
Double-check you have enough credits left for your Dialogflow CX account.
Check for any interruption on Dialogflow CX side.

### com.liveperson.bot-connectors-worker.error.aivendor.dialogflowcx.test-connection

#### Description
Testing connection with DialogFlow CX failed.
#### Reasons
Mostly credential issues.
#### Solutions
Check for your bot credentials.

### com.liveperson.bot-connectors-worker.error.aivendor.dialogflowcx.parse-message.parser-error

#### Description
Testing connection with DialogFlow CX failed.
#### Reasons
This error happens when credentials are not provided correctly.
#### Solutions
Verify the credentials provided for the bot.

### com.liveperson.bot-connectors-worker.error.aivendor.dialogflowcx.parse-message.multiple-actions

#### Description
This error happens when there are invalid or unknown multiple actions are received from the vendor.
#### Reasons
It was not possible to parse multiple actions from DialogFlow CX
#### Solutions
Verify the bot response correspond to the standards we provide in our developer's documentation.

### com.liveperson.bot-connectors-worker.error.aivendor.faas.invoke-lambda

#### Description

This indicates an issue during Faas invocation.

#### Reasons

This could have multiple reasons: function code non working, function invocation was not finished after 30s, Faas Quota limit was reached.

#### Solutions

Please verify and ensure that you have enough API calls quota left for FaaS function and make sure that FaaS function is working and invokable. Refer to the [Faas Documentation](liveperson-functions-deployment.html#testing-your-function) to understand how to test your function code.
Furthermore, please ensure your defined function follow the standard implementation as described in Third-Party bots documentation for [Custom Integration](third-party-bots-custom-integration.html). Failure to do so will result in the erroneous result.

### com.liveperson.bot-connectors-worker.error.aivendor.faas.missing-response-body

#### Description

This happens if there is no response body provided.

#### Reasons

The Faas callback was invoked without a response body object.

#### Solutions

Please make sure to provide a response body in the callback, for further information see [Custom Integration Documentation](liveperson-functions-deployment.html#testing-your-function)

### com.liveperson.bot-connectors-worker.error.aivendor.faas.failed-hook

#### Description

Indicates that the Faas hook could not be invoked.

#### Reasons

Implementation errors inside Faas hook.

#### Solutions

Double-check and test the Faas Hook code. You can refer to the [Faas Documentation](liveperson-functions-deployment.html#testing-your-function) to find out how to test your function code.
Please also check the dedicated documentation for [Third-Party-Bots Faas Hooks](https://developers.liveperson.com/third-party-bots-hook-configuration.html)

### com.liveperson.bot-connectors-worker.error.aivendor.lex.composite-format-not-supported

#### Description

This error is thrown Lex responds with a composite format.

#### Reasons

Lex response contained a composite format.

#### Solutions

Do not use the composite format in Lex for TPB.

### com.liveperson.bot-connectors-worker.error.aivendor.lex.custom-payload-malformed

#### Description

The custom format provided by lex is malformed.

#### Reasons

Mostly JSON errors.

#### Solutions

Please verify your custom JSON payload with a JSON validator of your choice.

### com.liveperson.bot-connectors-worker.error.aivendor.lex.custom-payload-no-params

#### Description

The custom payload did not contain any params.

#### Reasons

The params object is missing in the custom payload response.

#### Solutions

Add the params object in the custom payload response.

### com.liveperson.bot-connectors-worker.error.aivendor.lex.custom-payload-type-not-supported

#### Description

This happens in the payload contains a type which is not supported.

#### Reasons

Custom payload type provided is not supported.

#### Solutions

Remove the custom payload type from your response.

### com.liveperson.bot-connectors-worker.error.aivendor.lex.message-format-not-supported

#### Description

This happens if the provided message format is not supported.

#### Reasons

The chosen message format is not integrated into our connector.

#### Solutions

Only use supported message formats. [Lex](third-party-bots-amazon-lex.html)

### com.liveperson.bot-connectors-worker.error.aivendor.lex.parser-crashed

#### Description

This indicates an issue during parsing.

#### Reasons

Usually malformed response from Lex.

#### Solutions

IF this issue happens frequently, please reach out to LP Support with the copied error details.

### com.liveperson.bot-connectors-worker.error.aivendor.lex.send-query

#### Description

Happens if the query to Lex could not be sent.

#### Reasons

Lex temporarily unavailable.

#### Solutions

Double-check the credentials for your bot are still valid and you have enough credits left

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parser.custom.undefined-structured-content

#### Description

This error happens if the structured content property is undefined.

#### Reasons

Structured content response is undefined in Watson response

#### Solutions

Double-check the relevant Watson Payload and also double check the Watson docs [Watson Assistant](third-party-bots-ibm-watson-assistant.html)

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parser.image.undefined-source

#### Description

This error happens if there is no image source property provided on the Image object in the Watson response.

#### Reasons

Since no source is provided, the bot is unable to create the right LP Structured Content Object.

#### Solutions

Provide the source parameter for your Image.

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parser.list.undefined-options

#### Description

This error happens because the bot received a list response from Watson, without any options inside.

#### Reasons

The bot doesn't know how to handle an empty list, therefore we assume this is an error.

#### Solutions

Provide options properties to your Watson List object.

### com.liveperson.bot-connectors-worker.error.aivendor.watson.message-format-not-supported

#### Description

The message format provided by Watson is not supported by our connector.

#### Reasons

You are using a new format which we do not support yet.

#### Solutions

Please refer to this docs to see what messages we support [Watson Assistant](third-party-bots-ibm-watson-assistant.html)

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parser.text-and-custom.undefined-text

#### Description

The text property provided in the payload was undefined.

#### Reasons

Undefined text property.

#### Solutions

Either remove the text property or populate it with a text.

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parser.pause.undefined-time

#### Description

The provided pause time is not defined. Therefore we don't know what to do.

#### Reasons

Undefined pause time property.

#### Solutions

Double-check the pause time property is provided

### com.liveperson.bot-connectors-worker.error.aivendor.watson.parse-message.get-parse-message-failed

#### Description

This indicates an issue during message parsing.

#### Reasons

Wrong structure in the JSON payload.

#### Solutions

Double-check the Watson responses here: [Watson Assistant](third-party-bots-ibm-watson-assistant.html)[Watson AssistantV2](third-party-bots-ibm-watson-assistant-version-2.html)

### com.liveperson.bot-connectors-worker.error.aivendor.watson.index.generic-parser-crashed

#### Description

This happens if there is an issue with parsing the provided Watson response.

#### Reasons

Malformed Watson response.

#### Solutions

Double-check the Watson responses here: [Watson Assistant](third-party-bots-ibm-watson-assistant.html)[Watson AssistantV2](third-party-bots-ibm-watson-assistant-version-2.html)

### com.liveperson.bot-connectors-worker.error.aivendor.watson.send-query

#### Description

This happens if we could not send a query to Watson.

#### Reasons

Usually this happens if the quota limit is reached.

#### Solutions

Increase your Watson Quota to match the expected load.

### com.liveperson.bot-connectors-worker.error.aivendor.watson.watson-error

#### Description

This error is thrown if Watson had issues processing the consumer event.

#### Reasons

This could have multiple reasons. Mostly is a wrong implementation on Watson side.

#### Solutions

Check the error logs on your Watson Instance to find out the root cause of the failing bot.

### com.liveperson.bot-connectors-worker.error.aivendor.watsonv2.send-query

#### Description

This happens if we could not send a query to Watson.

#### Reasons

Usually, this happens if the quota limit is reached.

#### Solutions

Increase your Watson Quota to match the expected load.

### com.liveperson.bot-connectors-worker.error.aivendor.watsonv2.create-session

#### Description

This error happens if we could not create a Watson session for the conversation.

#### Reasons

Mostly, this would only fail because of a network issue.

#### Solutions

None. If this issue happens frequently, please reach out to LP Support with the error details.

### com.liveperson.bot-connectors-worker.error.aivendor.watsonv2.invalid-session

#### Description

The session id used by the conversation is not valid anymore.

#### Reasons

The lifespan of a conversation state is different in LP and IBM. It could be that an open conversation in LP is already closed in Watson.

#### Solutions

Increase the lifetime of a Watson conversation
Alternatively, you can also auto close conversations from the LP side remove any stuck conversations.

### com.liveperson.bot-connectors-worker.error.aivendor.microsoft.send-query

#### Description

Sending query to MS Bot Framework failed.

#### Reasons

This usually happens if the Endpoint is not responding in time.

#### Solutions

Make sure you send the response in time. Another reason could be an too small Azure instance, try to increase the provisioned resources for your bot.
If you are using a custom endpoint, double check it behaves exactly as the one we expect [Microsoft Bots](third-party-bots-microsoft-direct-line-introduction.html)

### com.liveperson.bot-connectors-worker.error.aivendor.microsoft.parser-crashed

#### Description

The parser could not parse the provided input and therefore crashed.

#### Reasons

Malformed JSON, malformed payload.

#### Solutions

Double-check the payload and make sure it is same as described [here](third-party-bots-microsoft-direct-line-basic-content.html) and [here](third-party-bots-microsoft-direct-line-advanced-features.html)

### com.liveperson.bot-connectors-worker.error.aivendor.microsoft.response-missing

#### Description

There is no response provided by the MS bot.

#### Reasons

Implementation error on MS bot.

#### Solutions

Double-check the payload and make sure it is same as described [here](third-party-bots-microsoft-direct-line-basic-content.html)

### com.liveperson.bot-connectors-worker.error.aivendor.microsoft.activity.invalid-type

#### Description

The provided activity type is not supported.

#### Reasons

The bot is not capable of handling this activity type.

#### Solutions

Double-check that you are only using supported activity types as described [here](third-party-bots-microsoft-direct-line-basic-content.html)

### com.liveperson.bot-connectors-worker.error.aivendor.microsoft.activity.invalid-name

#### Description

The provided activity name is not supported.

#### Reasons

The bot is not capable of handling this activity name.

#### Solutions

Double-check that you are only using supported activity names as described [here](third-party-bots-microsoft-direct-line-basic-content.html#bot-actions)

### com.liveperson.bot-connectors-worker.error.aivendor.faas.failed-faas-request

#### Description

This indicates an issue during Faas invocation.

#### Reasons

This could have multiple reasons: function code non working, function invocation was not finished after 30s, Faas Quota limit was reached.

#### Solutions

Please verify and ensure that you have enough API calls quota left for FaaS function and make sure that FaaS function is working and invokable. Refer to the [Faas Documentation](liveperson-functions-deployment.html#testing-your-function) to understand how to test your function code.
Furthermore, please ensure your defined function follow the standard implementation as described in Third-Party bots documentation for [Custom Integration](third-party-bots-custom-integration.html). Failure to do so will result in the erroneous result.

If none of these applies and the errors persist, please escalate to LP Support and provide the exact error information by copying it from within the Conversation Errors UI.

### com.liveperson.bot-connectors-worker.error.sdes-service.missing-session-or-visitor-id

#### Description

This indicates an issue fetching the SDEs because required properties are missing.

#### Reasons

Mostly this issue happens because of a wrong integration on customer end where no Visitor Session is created before starting the conversation.

#### Solutions

Please ensure that you create a Visitor Session prior to starting the conversation. [Website Monitoring](app-engagement-api-overview.html).

### com.liveperson.bot-connectors-worker.error.sdes-service.uauth-sdes-entry-is-empty

#### Description

This indicates an issue fetching the SDEs.

#### Reasons

Mostly this issue happens because of a wrong integration on customer end where no Visitor Session is created before starting the conversation. Another reason could be that no SDEs were set.

#### Solutions

Please ensure that you create a Visitor Session prior to starting the conversation. [Website Monitoring](app-engagement-api-overview.html).
Also please check that you set the SDEs correctly. [Engagement Attributes](engagement-attributes-api-engagement-attributes.html)

### com.liveperson.bot-connectors-worker.error.aivendor.faas.parse-message.malformed-alternative-intents

#### Description

This indicates an issue with the format of the alternate intent

#### Reasons

This issue will happen if the alternate intent that was sent in the FaaS function response doesn't conforms to our expected format.

#### Solutions

Please ensure that you are sending alternative intents in the correct format as defined per our documentation. [Faas Documentation](third-party-bots-custom-integration.html#sending-intent-information).
