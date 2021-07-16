---
pagename: API
redirect_from:
  - ProactiveMessaging.html
Keywords:
sitesection: Documents
categoryname: "Messaging Channels"
documentname: Proactive Messaging
permalink: proactive-messaging-api.html
indicator: messaging
---

### Introduction

Proactive Messaging allows brands to send outbound messages to consumers and route the responses from consumers into Conversational Cloud; creating two-way messaging conversations. Proactive Messaging v2.0 API is the latest API with many improvements from the older 1.0 API version. The Proactive v2.0 API comes with rate limiting, support for scheduling guardrails, high send rate and integrates with Conversational Cloud campaign and engagement for conversation routing. Proactive Messaging v2.0 API is currently available to customers for SMS, WhatApp and Inapp. And it supports customer SDE, which includes [customer info](engagement-attributes-types-of-engagement-attributes.html#customer-info) and/or [personal info](engagement-attributes-types-of-engagement-attributes.html#personal-info). Customer SDE is only applicable for SMS and WA. 
Note: Proactive Messaging can be leveraged using Proactive 2.0 API or the [Web Tool](https://knowledge.liveperson.com/messaging-channels-proactive-messaging-proactive-messaging-overview.html).

### Getting Started

1. Onboarding to the [Proactive Web Tool](https://knowledge.liveperson.com/messaging-channels-proactive-messaging-proactive-messaging-overview.html) is mandatory before onboarding to Proactive 2.0 API. For the Proactive Web Tool, fill out this [request](https://forms.gle/tUqhtE7kjAJpmo9L8) to get on-boarded. 
2. To onboard on Proactive 2.0 API, perform steps as mentioned below
- Login to [Proactive](https://proactive-messaging.fs.liveperson.com/) web app with user having administrator privileges.
    * Click on Settings tab in menu bar.
    * Click on Enable button to onboard to proactive api.
    * Click on show secrets to get app Id and secrets which will be used to create APP JWT. Click here to learn how to use [APP JWT](https://developers.liveperson.com/connector-api-send-api-authorization-and-authentication.html#get-appjwt).

### API Specifications
## API Domain
* Proactive messaging is deployed in three regions. **North America**, **EMEA** (Europe, Middle East and Africa), **APAC** (Asia Pacific). Use the domain api to identify the zone of proactive api which is to be used for an account.

| Method | URI  |
| :--- | :--- |
| GET | http://api.liveperson.net/api/account/{ACCOUNT_ID}/service/agentVep/baseURI.json?version=1.0|

```json
{
    "service": "agentVep",
    "account": "ACCOUNT_ID",
    "baseURI": "va.agentvep.liveperson.net"
}
```

| If Sentinel **baseURI** then | Proactive Region | Proactive **API domain** | API Documentation |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **va**.agentvep.liveperson.net  | NA | proactive-messaging.**z1**.fs.liveperson.com | Click [here](https://proactive-messaging.z1.fs.liveperson.com/api/api-docs/?api=outbound) for API spec
| **lo**.agentvep.liveperson.net  | EMEA | proactive-messaging.**z2**.fs.liveperson.com | Click [here](https://proactive-messaging.z2.fs.liveperson.com/api/api-docs/?api=outbound) for API spec
| **sy**.agentvep.liveperson.net  | APAC | proactive-messaging.**z3**.fs.liveperson.com | Click [here](https://proactive-messaging.z3.fs.liveperson.com/api/api-docs/?api=outbound) for API spec

## Campaign API: Example Request and Response
* Click [**Campaign**](https://proactive-messaging.z1.fs.liveperson.com/api/api-docs/?api=outbound#/Campaign/campaign) to go through API spec and use example here to get started.

| Method | URI  |
| :--- | :--- |
| POST | https://{domain}/api/v2/account/{ACCOUNT_ID}/campaign|

**Path Parameters**

| Name  | Description | Value/Example |
| :--- | :--- | :--- |
| domain   | see [API Domain](#api-domain-and-documentation) | proactive-messaging.**z1**.fs.liveperson.com or proactive-messaging.**z2**.fs.liveperson.com or proactive-messaging.**z3**.fs.liveperson.com |
| ACCOUNT_ID | LivePerson site ID | 34567231 |

**Request Headers**

| Header | Description | Value/Example |
| :--- | :--- | :--- |
| Content-Type | Used to indicate the media type of the resource | application/json |
| Authorization | Extract the access_token value from the response retrieved by the [Get AppJWT](https://developers.liveperson.com/connector-api-send-api-authorization-and-authentication.html#get-appjwt) | Bearer <<APP_JWT>> |

**Request Body Example - JSON Payload - New Version - Whatsapp With Rich Template, including customer SDE**

```json
{
    "campaignName": "TestProactiveAPI",
    "skill": "sales",
    "templateId": "1111111111111",
    "outboundNumber": "22222222222",
    "consent": true,
    "consumers": [
        {
            "consumerContent": {"wa": "12345678891"},
            "variables": {
                "1": "Text1",
                "2": "Text2",
                "3": "Text3",
                "4": "Text4",
                "5": "Text5"
            },
            "headerVariables": {
                "video": "https://file-examples-com.github.io/uploads/2017/04/file_example_MP4_640_3MG.mp4" 
            }
        },
        {
            "consumerContent": {"wa": "1234456678899"},
            "variables": {
                "1": "Test1",
                "2": "Test2",
                "3": "Test3",
                "4": "Test4"
            },
            "headerVariables": {
                "video": "https://file-examples-com.github.io/uploads/2017/04/file_example_MP4_640_3MG.mp4"
            },
            "personalInfo": {
                "firstname": "Smith",
                "lastname": "John",
                "age": {
                    "age": 31,
                    "year": 1990,
                    "month": 1,
                    "day": 11
                },
                "contacts": [{
                    "email": "test@example.com",
                    "phone": "+1 480-400-8000",
                    "address": {
                        "country": "United States",
                        "region": "NA"
                    }
                }],
                "gender": "MALE",
                "language": "en-US",
                "company": "LP"
            },
            "customerInfo": {
                "cstatus": "VIP",
                "ctype": "Gold",
                "customerId": "138766AC",
                "balance": -200.99,
                "currency": "EUR",
                "socialId": "11256324780",
                "imei": "3543546543545688",
                "userName": "user000",
                "companySize": 500,
                "companyBranch": "East Village",
                "accountName": "Bank corp",
                "role": "Marketing manager",
                "lastPaymentDate": {
                    "day": 15,
                    "month": 10,
                    "year": 2016
                },
                "registrationDate": {
                    "day": 23,
                    "month": 5,
                    "year": 2015
                },
                "loginStatus": 1
            }
        }
    ]
}
```
**Response Example**

```json
{
    "proactiveCampaignId": "a9cRASfbQ",
    "leCampaignId": "1239032370",
    "leEngagementId": "1244018070",
    "requestTraceId": "f7d5baa8-d4c1-46ad-bd1e-9a98a38b99a3",
    "failedConsumers": [
        {
            "variables": {
                "1": "Test1",
                "2": "Test2",
                "3": "Test3",
                "4": "Test4"
            },
            "consumerContent": {
                "wa": "1234456678899"
            },
            "headerVariables": {
                "video": "https://file-examples-com.github.io/uploads/2017/04/file_example_MP4_640_3MG.mp4"
            },
            "phone": "+1234456678899",
            "countryCode": "IN",
            "errorMessage": "MISSING_VARIABLE=5"
        }
    ],
    "acceptedConsumers": [
        {
            "id": "252d195b-1a4f-8807-aa45-97d2a5560e44",
            "phoneNumber": "+12345678891",
            "consumerContent": {
                "wa": "12345678891"
            }
        }
    ]
}
```

**Request Body Example - JSON Payload - New Version - SMS**

```json
{
    "campaignName": "TestProactiveAPI",
    "skill": "sales",
    "templateId": "666555567888",
    "outboundNumber": "22222222222",
    "consent": true,
    "consumers": [
        {
            "consumerContent": {"sms": "12345678891"},
            "variables": {
                "1": "Hello X"
            }
        },
        {
            "consumerContent": {"sms": "1234456678899"},
            "variables": {
                "1": "Hello Y"
            }
        }
    ]
}
```
**Response Example**

```json
{
    "proactiveCampaignId": "a9cRASfbQ",
    "leCampaignId": "1239032370",
    "leEngagementId": "1244018070",
    "requestTraceId": "f7d5baa8-d4c1-46ad-bd1e-9a98a38b99a3",
    "failedConsumers": [],
    "acceptedConsumers": [
        {
            "id": "252d195b-1a4f-8807-aa45-97d2a5560e44",
            "phoneNumber": "+12345678891",
            "consumerContent": {
                "sms": "12345678891"
            }
        },
        {
            "id": "674476fgf-1a4f-7088-45aa-44e05560e44",
            "phoneNumber": "+1234456678899",
            "consumerContent": {
                "sms": "1234456678899"
            }
        }
    ]
}
```

**Request Body Example - JSON Payload - New Version - Handoff(SMS + Whatsapp without Rich Template)**

```json
{
    "campaignName": "TestProactiveAPI",
    "skill": "sales",
    "templateId": "1234567890",
    "outboundNumber": "22222222222",
    "consent": true,
    "consumers": [
        {
            "consumerContent": {"sms": "12345678891", "wa": "12345678891"},
            "variables": {
                "1": "Test1",
                "2": "Test2",
                "3": "Test3"
            }
        },
        {
            "consumerContent": {"sms": "1234456678899", "wa": "1234456678899"},
            "variables": {
                "1": "Test1",
                "2": "Test2",
                "3": "Test3"
            }
        }
    ]
}
```
**Response Example**

```json
{
    "proactiveCampaignId": "a9cRASfbQ",
    "leCampaignId": "1239032370",
    "leEngagementId": "1244018070",
    "requestTraceId": "f7d5baa8-d4c1-46ad-bd1e-9a98a38b99a3",
    "failedConsumers": [],
    "acceptedConsumers": [
        {
            "id": "252d195b-1a4f-8807-aa45-97d2a5560e44",
            "phoneNumber": "+12345678891",
            "consumerContent": {
                "sms": "12345678891",
                "wa": "12345678891"
            }
        },
        {
            "id": "674476fgf-1a4f-7088-45aa-44e05560e44",
            "phoneNumber": "+1234456678899",
            "consumerContent": {
                "sms": "1234456678899",
                "wa": "1234456678899"
            }
        }
    ]
}
```

**Request Body Example - JSON Payload - New Version - Inapp Handoff**

```json
{
    "campaignName": "TestInappProactiveAPI",
    "skill": "sales",
    "templateId": "H1234567890",
    "consent": true,
    "consumers": [
        {
            "consumerContent": {"inapp": "user1"},
            "variables": {
                "1": "Hi user1, welcome to proactive messaging.",
            }
        }
    ]
}
```
1. All fields are required. 
2. If variables is empty object, the default value set in handoff will be used.
3. The value of consent must be true. 
4. If the vaule of skill or templateId is not correct, it will failed to create proactive campaign and error will be returned.  
 
**Response Example**

```json
{
    "proactiveCampaignId": "a9cRASfbQ",
    "leCampaignId": "1239032370",
    "leEngagementId": "1244018070",
    "requestTraceId": "f7d5baa8-d4c1-46ad-bd1e-9a98a38b99a3",
    "failedConsumers": [],
    "acceptedConsumers": [
        {
            "id": "252d195b-1a4f-8807-aa45-97d2a5560e44",
            "consumerContent": {
                "inapp": "user1"
            }
        }
    ]
}
```

**Request Body Example - JSON Payload - Old Version**

```json
{
    "campaignName": "TestProactiveAPI",
    "skill": "sales",
    "templateId": "943679028015322",
    "consent": true,
    "outboundNumber": "12025166656",
    "consumers": [
        {
            "consumerCountryCode": "1",
            "consumerPhoneNumber": "1012959736",
            "variables": {
            	"1": "Test outbound api"
            }
        }
    ]
}
```
**Response Example**

```json
{
   "proactiveCampaignId": "08TwCku2h",
   "leCampaignId": "1887624732",
   "leEngagementId": "1966477634",
   "requestTraceId": "705ffabe-14bb-4217-9eb7-8c12ff43a5d6",
   "failedConsumers": [],
   "acceptedConsumers": [
       {
           "id": "tjlaY5FJfv",
           "phoneNumber": "+11012959736"
       }
   ]
}
```

## Conversations API: Example Request and Response
* click [**Conversations**](https://proactive-messaging.z1.fs.liveperson.com/api/api-docs/?api=outbound#/Campaign/conversations) to go through API spec and use example here to get started.


| Method | URI  |
| :--- | :--- |
| GET | https://{domain}/api/v2/account/{ACCOUNT_ID}/campaign/{PROACTIVE_CAMPAIGN_ID/conversations|

**Path Parameters**

| Name  | Description | Value/Example |
| :--- | :--- | :--- |
| domain   | see [API Domain](#api-domain-and-documentation)| proactive-messaging.**z1**.fs.liveperson.com or proactive-messaging.**z2**.fs.liveperson.com or proactive-messaging.**z3**.fs.liveperson.com |
| ACCOUNT_ID | LivePerson site ID | 34567231 |
| PROACTIVE_CAMPAIGN_ID | Proactive campaign ID found in campaign response | 08TwCku2h |

**Request Headers**

| Header | Description | Value/Example |
| :--- | :--- | :--- |
| Content-Type | Used to indicate the media type of the resource | application/json |
| Authorization | Extract the access_token value from the response retrieved by the [Get AppJWT](https://developers.liveperson.com/connector-api-send-api-authorization-and-authentication.html#get-appjwt) | Bearer <<APP_JWT>> |

**Response Example**

```json
{
    "campaignStatus": "FINISHED",
    "conversations": [
        {
            "id": "tjlaY5FJfv",
            "status": "DELIVERED",
            "conversationId": null,
            "errorMessage": null
        }
    ]
}
```

### Proactive 2.0 API: Frequently Asked Questions

<strong>Can we share the bot users for proactive 2.0 api with other systems?</strong>
The bot users should only be used for proactive 2.0 api. The bot users are needed since we need to send messages on behalf of agent to consumers. The bot users session in proactive 2.0 api can break if these bot users are logged in some where else in some other services.

<strong>What is the rate limit for the API?</strong>
The current rate limit is 10 TPS/second/brand per api.

<strong>What is the daily limit when sending outbound messages?</strong>
It depends on the channel. Messaging Channel providers like WhatsApp have certain limitations on how many messages can be sent per day. Considering these limitations Proactive Messaging will limit to 100K recipients/message/day/channel/account. For example, if account X creates Y campaigns on 04/28/2020 with total recipients R for SMS channel cumulative. If 100K - R is 100 then creating a new campaign on 04/28/2020 for SMS channel with more than 100 recipients will fail.

<strong>Which channels are supported as of now?</strong>
- Proactive messaging supports SMS and WA channels only. The channel is decided based on templateId in campaigns api request.
- Choose templateId="1234567890" for SMS messages and WA templateId for sending WA messages.

<strong>Does Proactive Messaging provide a way to send SMS messages within a certain time window (TCPA compliance)?</strong>
 Proactive Messaging ensures that recipients only receive messages within the time window brands specifies. This time window is calculated based on the recipient phone number. This helps brands adhere to one of the legal requirements for sending SMS texts i.e. SMS can only be sent between 8 am and 9 pm to avoid spamming consumers after business hours.

<strong>Once a campaign is submitted, how soon will these recipients receive the messages?</strong>
Messages are sent at a rate upto 10 messages per second per channel per account. For example, a campaign is created for an SMS channel using the default receiving window for 100 recipients. Some of these recipients have phone numbers from regions belonging to PST, CST, EST time zones. Once a campaign is submitted/published, based on the phone number, a zone is computed (number with +1 - (201) is found to be in EST). Using the specified receiving window, a decision is made to send a message to the phone number if current time in that zone is within the window. If the recipient receiving window is closed then a message will be sent on the next opening of the window.

<strong>How will batching capability work?</strong>
A single campaign can have from 1 recipient and not more than 100 recipients. It is recommended to batch recipients in a campaign.

<strong>What are the error codes for invalid recipients information in the campaign?</strong>
Consider an example response of campaigns API:
```json
{
    "proactiveCampaignId": "t86nfq57S",
    "leCampaignId": "1156064532",
    "leEngagementId": "1190093132",
    "requestTraceId": "221cc131-056a-4c19-a259-8e6ec8e57101",
    "failedConsumers": [
        {
            "phone": "+11012539745",
            "errorMessage": "<<ERROR_MESSAGE>>",
            "variables": {
                "1": "Testing Outbound Api WA"
            }
        }
    ],
    "acceptedConsumers": []
}
```

| <<ERROR_MESSAGE>> | Description |
|-------------------------------------------|------------------------------------------------------------------------------------|
| 'INVALID_NUMBER'                  		         | The associated recipient/consumer country code or phone number or both is invalid. |
| 'DUPLICATE_NUMBER'                		         | At least one of the consumers has the same phone number as another in the same campaign. |
| 'MISSING_CONSUMER_INFORMATION==<<CHANNEL>>'        | At least one of the consumers is missing consumer information such as phone number for one of the channels in the template or handoff. |
| 'TOO_MANY_VARIABLES'              		         | The template expects less variables for creating the message to the recipient. |
| 'INSUFFICIENT_VARIABLES'              	         | The template expects more variables for creating the message to the recipient. |
| 'MISSING_VARIABLE=<<VARIABLE_NAME>>'  	         | The consumer has a missing variable identified by VARIABLE_NAME. |
| 'VARIABLE_NOT_STRING=<<VARIABLE_NAME>>'            | The consumer has a variable which is not a string identified by VARIABLE_NAME. |
| 'Fields missing in request: <<FIELD_NAME>>'        | The entire request was reject because it was miissing fields.  For example, if the consumers list is missing the variables field. |
| 'INSUFFICIENT_HEADER_VARIABLES'                    | At least one of the consumers was missing a header variable for a rich text campaign. |
| 'TOO_MANY_HEADER_VARIABLES'                        | At least one of the consumers had too many header variables for a rich text campaign.  |
| 'MISSING_HEADER_VARIABLE=<<HEADER_VARIABLE_TYPE>>' | At least one of the consumers had an incorrect header variables for a rich text campaign.  |
| 'HEADER_VARIABLE_NOT_STRING'                       | At least one of the consumers had a header variable that is not a string for a rich text campaign.  |
| 'HEADER_VARIABLE_INVALID_URL'                      | At least one of the consumers had a header that is not a valid URL for a rich text campaign.  |
| 'IMAGE_URL_NOT_WHITELISTED'                        | At least one of the consumers had a image link that is not from a whitelisted host for for a rich text campaign. |

<strong>What kind of security, encryption, parameter, failures?</strong>
The API uses App Jwt Oauth 2.0 authentication.

<strong>Does the API have status call backs? How do we get the status of the message?</strong>
Proactive Messaging does not have call backs to inform the status. Proactive Messaging provides status of messages through [conversations](https://proactive-messaging.fs.liveperson.com/api/api-docs/v2/outbound/#/Campaign/conversations) API.

<strong>Does LivePerson return some sort of error response when the user already opted out? For example if we try to send to a number that's blocked?</strong>
- Proactive guarantees opt-out from SMS only. If a consumer opts out from twilio SMS, we guarantee that no future Proactive messages will be sent to the consumer until they re-opt-in again. For messages that are sent to consumer who opted out, the state of recipient will be marked 'SKIPPED' in conversations api.
- Proactive messaging does not have the ability to capture opt-out from WA channels.

<strong>Is there a throughput limitation for the data that gets passed from Twilio to LP? For example, if brand sends 100 Twilio msgs/sec (their max throughput), then can the data flow through to LP at the same rate?</strong>
- Proactive Messaging does not have any limitations on the message size while sending messages to twilio or other channels. However a large message may translate to more than one message when the recipient receives it.
- Example: A message of more than 140 characters will be divided into two messages and sent to recipients.
 
<strong>What reporting metrics do I get? What metrics are available now?</strong>
- Proactive Messaging provides the status of messages delivered to recipients through [conversations](#conversations-api-example-request-and-response) api. [conversations](#conversations-api-example-request-and-response) api provides the necessary information to compute the success and failure of messages being sent to connectors. Below are status of recipients that provides the information like

| <<MESSAGE_STATUS>> | Description |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| 'DELIVERED'         | Message was delivered successfully to our downstream service. |
| 'DRAFT'             | When recipients are added to a campaign and not yet published. For users of 2.0 API, this can happen 	when recipients are added to the campaign and publishing fails abnormally. |
| 'TOO_MANY_VARIABLES'| More variables are provided for the message than expected |
| 'FAILED'            | Messages is not delivered to recipient because of an error indicated by error message |
| 'NOT_SENT'  		  | Not sent state happens when campaign is in published mode and recipients are yet to schedule. |
| 'SKIPPED'   		  | Usually happens when the user has Opted Out from receiving any message from the Brand. |
| 'SCHEDULED'   	  | Message that is not delivered and is scheduled to be delivered at a later moment during the next business hour. |

<strong>What is the lifespan of the app JWT? When we do need to get a new JWT, do we have to first make the call to LivePerson Domain API in order to get the sentinel service domain, or is that domain consistent enough that we can hard code that in?</strong>
- An APP JWT expiration time is 1 hour from the time it is created. To get an app JWT from sentinel API, a call to domain api has to be made to get the sentinel api domain. This domain can be cached for some duration. We expect the domain to change in very rare cases. It’s still recommended that cache duration should not be more than 1 day.

- When using app JWT to call Proactive api, a response below indicates the jwt is expired and new app jwt to be obtained from sentinel api.
	```json
	{
		"code": 0,
		"message": "jwt expired"
	}
	```

<strong>Do we need any other JWT other than APP JWT e.g. Consumer JWT?</strong>
Proactive Messaging service does not create or consume consumer JWT or other JWT except APP JWT. Proactive Messaging api only consumes AppJwt created from provided clientId and Secret for authentication.

<strong>What should the authentication header look like, is the bearer token the only thing required even in production usage? Do we need to include our ConsumerKey/Secret or our AccessToken/Secret that we use in the 1.0 API at all, or any other information?</strong>
App Jwt will be consumed as Bearer Token. No other key, secret or token will be consumed by Proactive Messaging api.

<strong>How does proactive 2.0 api provide status of message e.g. success/failure of delivery ?</strong>
The Proactive 2.0 campaign api is asynchronous meaning that the success and failure of a message to a recipient is noted only when the recipient is picked from the proactive internal queue and a message is sent as per pre configured message rate. The [conversations](#conversations-api-example-request-and-response) api will provide the status of recipients tied to the campaign created.

<strong>Of the error cases described above, which of those errors should we consider "retry-able"? For example, a bad request due to a missing field is not retry-able because it will just always fail, but a case where one of the downstream services was temporarily unavailable could warrant a retry. Which error cases that we could get back from the /campaigns endpoint are retryable and how should we handle a retry to avoid sending duplicate messages to a customer?</strong>
Proactive Messaging service has retry mechanism internally on dependent services to reduce failures due to transient errors.

<strong>What’s the lookback period?</strong>
- Lookback period is how long will LP services maintain context (like campaign info, skill etc) for a reply of a message that is sent to the recipient/consumer using a campaign. Current lookback period is 30 days from when messages are sent using Proactive api. 
- Example: When a message is sent to consumer using Proactive Messaging api and if consumer replies within 30 days from when message was sent, the response will be redirected to Conversational Cloud agent according to specified skill in Proactive Campaign. A response after 30 days will be be treated as any inbound message and routed to a default skill in Conversational Cloud (this is configured by brand). Please note, if a consumer has an existing active conversation with a brand in any channel, the outbound message won’t be delivered.

<strong>Are the scheduling times required? What happens if we don't specify it? What if we only specify one day Monday, etc.?</strong>
- As indicated in the swagger documentation, this is an optional field. If scheduling times are not passed, then Proactive Messaging will default to channel window times i.e. 13 hrs. (8:00 am - 9:00 pm) for SMS and 24 hrs. for other channels. e.g. If only Monday time is passed, then messages will only be sent in the Monday window times and any remaining messages after Monday window time will be sent in next Monday window times. For SMS, if default window 8:00 am - 9:00 pm is less than required then provide schedule window in campaign request to send SMS outside the default window.

<strong>One variable is required for SMS but what happens when more than 1 variable is passed? Will the payload fail, or will it just take the first variable?</strong>
- Proactive messaging performs strict checking for variables. If more variables are specified than what are required, proactive messaging will mark the recipient failed with error 'TOO_MANY_VARIABLES' which will be part of campaign response.

<strong> How do we know which field is optional or required?<strong>
- Proactive messaging is using industry recommended swagger specifications for API documentation. Swagger model specification will specify required and optional fields. e.g. Visit [**Campaign**](https://proactive-messaging.z1.fs.liveperson.com/api/api-docs/?api=outbound#/Campaign/campaign) API spec and click on model as indicated by image below to learn about campaign request optional and required fields.
- <img src="images/swaggerModelExample.png" alt="Swagger Model" style="width:auto;max-height:500px;">

<strong>What are the restrictions on the field in campaign request?<strong>

| FIELD_NAME | LIMITATIONS | EXPLANATION |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| campaignName         | 255 char max length | |
| skill             | 255 char max length | |
| templateId | 32 char max length | templateId will be provided by proactive messaging when a template is created |
| outboundNumber            | 16 char max length | Phone number cannot be more than 16 digit |
| variable  		  | 1550 char max length | SMS messages more than 160 chars may be sent as multiple messages |

<strong>Is Whatsapp Rich template enabled for all accounts?</strong>
Yes.

<strong>What are different components of a Whatsapp template? Are all the components mandatory to be present in a rich template?</strong>
There are four different components of a Whatsapp template
- Header (Image, Video, Document is supported currently. Only 1 type is allowed for a template)
- Body
- Footer
- Buttons (2 types: Quick Reply Buttons, Call To Action Buttons)
Message body in WA Rich template is mandatory. Header, footer, buttons are optional in WA Rich template depending on template design.

<strong>What extensions are supported for WA rich template in the header section?</strong>
Allowed extensions for different types of header for a rich template: 
- Image:[jpg,png],
- Document:[pdf],
- Video:[mp4,3gpp]

<strong>Are there any limitations on the URL added for header image/video/document type?</strong>
Below are the limitations:
- URL provided for header (image/video/document) should be publicly accessible
- Only https urls are supported
- Before sending WhatsApp rich messages using a template with header of type image, please reach out to your CSM to get the domain whitelisted in Houston. Root Url/ domain has to be whitelisted by CSM in houston site settings messaging.rich.content.valid.urls.
 For example; if the brand wants to send images from upload.wikimedia.org like: 
https://upload.wikimedia.org/wikipedia/commons/9/97/Art_by_Chance.jpg
https://upload.wikimedia.org/wikipedia/commons/6/63/Beity_Logo.jpg
they should have https://upload.wikimedia.org added in houston site settings. Please see the screenshot below. 
<img src="images/URL_whitelisting.png" alt="URL Whitelisting" style="width:auto;max-height:500px;">

<strong>Do we need any input from user for footer and quick reply buttons section while creating campaign using rich template?</strong>
Footer and quick reply buttons have static values and do not need any user input while campaign creation

<strong>What kind of customers can get Inapp message through Proactive Messaging?</strong>
Only registered customers can. 

<strong>How does first Inapp message display in agent workspace?</strong>
First Inapp message is not part of conversations becuase customers cannot send first message on behalf of agent. Agent widget is used to display first message. It's not perfect. we are trying to solve it. 

<strong>Is customer SDE enabled for all accounts?</strong>
To use customer SDE via API, reach out to Proactive team to get it enabled for the account. Currently the feature is not enabled for all accounts.