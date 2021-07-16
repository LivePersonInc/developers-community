---
pagename: Events
redirect_from:
  - le-tag-events-events.html
  - lp-tag-visitor-flow.html
  - le-tag-events-visitor-flow-events.html
  - lp-tag-engagement-window.html
  - le-tag-events-engagement-window-events.html
  - lp-tag-engagement.html
  - le-tag-events-engagement-events.html
sitesection: Documents
categoryname: "Website Monitoring"
documentname: Web Tag
subfoldername: Events
permalink: web-tag-events-events.html

indicator: both
---

The `lpTag` handles the communication of many events that occur on the vistor's webpage.

These tag events provide transparency into the lifecycle flows of engagements, embeddeded chat windows, and cobrowse sessions, among others. 

Below you can find a list of events published on a web page by the Web Tag, each organized under an `appName` and given an `eventName`.

[See here to learn how to bind to events](le-tag-events-event-binding.html)

### Visitor Flow Events

#### VAR_ADDED

This event is triggered when an [Engagement Attribute (SDE)](engagement-attributes-overview.html) is reported.

**Event Information**

| Name | Value |
| :---| :--- |
| eventName | "VAR_ADDED" |
| appName | "lp_sdes" |

**Event Data**

| Name | Description | Type / Value |
| :--- | :--- | :--- |
| | The SDE JSON | JSON |

*Example (Transaction Engagement Attribute):*

```javascript
{
    "type": "cart", //MANDATORY
    "total": 11.7, //TOTAL CART VALUE
    "numItems": 6, //NUMBER OF ITEMS IN CART
    "products": [{  //ARRAY OF PRODUCTS
        "product": {
        "name": "prod1", //PRODUCT NAME
        "category": "category", //PRODUCT CATEGORY NAME
        "sku": "sku", //PRODUCT SKU OR UNIQUE IDENTIFIER
        "price": 7.8 //PRODUCT PRICE
        }, "quantity": 1 //NUMBER OF PRODUCTS
    }]
}
```

#### MONITORING_STATE

This event is triggered when vistor monitoring starts and/or when its state is changed.

**Event Information**

| Name | Value |
| :---| :--- |
| eventName | "MONITORING_STATE" |
| appName | "lp_SMT" |

**Event Data**

| Name | Description | Type / Value |
| :--- | :--- | :--- |
| active | The monitoring state. | Boolean |

*Example:*

```javascript
{
    "active": "boolean"
}
```

### Chat Window Events


These are chat window related events. Because the customer conversation is contained within the window, the events provided here are related to the lifecycle of a conversation.

{: .important}
These events will only be triggered for an **embedded** window, **not** a pop-out window.

#### state

This event triggers when the chat state is changed.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "state" |
| appName | "lpUnifiedWindow" |

**Event Data**

| Name | Description | Type | Notes |
| :-- | :--- | :--- | :--- |
| state | The chat state. | string | Available states: "resume", "initialised", "uninitialised", "preChat", "postChat", "offline", "waiting", "chatting", "interactive", "ended", "Notfound". Out of these, **only** "initialised", "chatting" and "ended" are relevant for Messaging. |

*Example:*

```javascript
{ "state" : "chatting" } //The current chat state
```

#### conversationInfo

This event triggers when the conversation data was changed, for example the conversation state. For chat, the event data includes the current value of all known attributes. For messaging, the event data only contains the attributes that have changed.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "conversationInfo" |
| appName | "lpUnifiedWindow" |

**Event Data**

| Name | Description | Type | Notes |
| :--- | :--- | :--- | :--- |
| agentName | The agent name to which the visitor is connected. | string | |
| agentId | The agent ID to which the visitor is connected. | ALPHA_NUMERIC | |
| conversationId | The conversation ID. | ALPHA_NUMERIC | For messaging |
| state | The chat state. | string | Available states: "resume", "initialised", "uninitialised", "waiting", "chatting", "ended", "Notfound" |
| monitoringSessionId | Session ID. | ALPHA_NUMERIC | |
| visitorId | Visitor ID. | ALPHA_NUMERIC | |
| skill | The conversation skill. | string | |
| engagementId | The engagement ID that was clicked to open the chat. | ALPHA_NUMERIC | |
| campaignId | The engagement’s campaign ID. | ALPHA_NUMERIC | |
| language | The conversation language. | string | An [ISO 639-1 Alpha-2](http://openid.net/specs/openid-connect-core-1_0.html#ISO639-1) language code in lowercase and an [ISO 3166-1 Alpha-2](http://openid.net/specs/openid-connect-core-1_0.html#ISO3166-1) country code in uppercase, separated by a dash. For example, en-US or fr-CA. |
| engagementName | The engagement name as defined in Conversational Cloud UI. | string  | |

*Example:*

```javascript
{
   "agentName": "John Doe",
   "agentId": 2,
   "conversationId": 4294973105,
   "state": "chatting",
   "monitoringSessionId": "WIoWBRC_RL6pkcK5fL-3-g.5bb46ddd7ae63b731b5eeb10189b15bc97226af0",
   "visitorId": "UYxShcOtSEWq0oSsuMCrOQ",
   "skill": "MySkill",
   "engagementId": 1346152510,
   "campaignId": 1346152410,
   "language": "en-US",
   "engagementName": "Sticky chat button"
}
```

#### engagementData

This event triggers when the state changes to "chatting" to show the engagement info.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "engagementData" |
| appName | "lpUnifiedWindow" |

**Event Data**

| Name | Description | Type |
| :--- | :--- | :--- |
| engagementName | The engagement name as defined in Conversational Cloud UI | string | |
| state | The chat state ("chatting"). | string |

*Example:*

```javascript
{
    "engagementName" : "Sticky chat button",
    "state": "chatting"
}
```

#### maximized

This event triggers when the chat window is in maximized view.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "maximized" |
| appName | "lpUnifiedWindow" |

#### minimized

This event triggers when the chat window is in minimized view.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "minimized" |
| appName | "lpUnifiedWindow" |

#### windowClosed

This event triggers when the chat window is closed (disposed and removed from the DOM).

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "windowClosed" |
| appName | "lpUnifiedWindow" |

### Engagement Events

These are engagement-related events, including rendering, display and interactions with the engagement.

#### START

This event is triggered when the flow to display the engagement has started.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "START" |
| appName | "LP_OFFERS" |

**Event Data**

| Name | Description | Type / Value | Notes |
| :--- | :--- | :--- | :--- |
| contexts | The engagement and page context ID (impression ID) in the current monitored session. | Array of Objects | Example: <br>[ <br> {"EngagementContext":{"id": "1"}}, <br> {"pageContext":{"id":"173828"}} <br> ] |
| campaignId | The engagement’s campaign ID. | ALPHA_NUMERIC | |
| engagementId | The engagement ID. | ALPHA_NUMERIC | |
| engagementRevision | The engagement revision. | ALPHA_NUMERIC | |
| engagementType | The engagement format. | Numeric | Available values: 0: "Peeling corner", 1: "Overlay", 2: "Toaster", 3: "Slide-out", 5: "Embedded", 6: "Sticky" |
| contextId | The engagement context ID (engagement impression ID) in the current monitored session. | ALPHA_NUMERIC | |
| zoneId | Internal. The engagement zone ID. | ALPHA_NUMERIC | |
| state | The agent's state | Numeric | Available values: 1 - online, 2 – offline, 4 - busy |
| confKey | Internal. CampaignId + EngagementId + Revision. | string | |
| tglName | Internal. The engagement format description. | string | |
| done | If the configuration has finished loading. | Boolean | |
| engagementName | The engagement name as defined in Conversational Cloud UI. | string | |

*Example:*

```javascript
{
    "contexts": [
        {"EngagementContext": {
                "id": "1"
            }
        },
        {"pageContext": {
                "id": "1738225948"
            }
        }
    ],
    "campaignId": 210599710,//The campaign Id
    "engagementId": 210600710,//The engagement Id
    "engagementRevision": 18,//The revision we are going to show
    "engagementType": 3,//The engagement type
    "contextId": "1",//The context (instance in memory on the backend)
    "zoneId": 471288710, //The zone this is on
    "state": 2, //The current state of the agents (online, offline, busy) , to set the display state
    "confKey": "210599710_210600710_18",
    "tglName": "slider" //The taglet that needs to be downloaded
    "done": true, //If the configuration has finished loading
    "engagementName": "Slide-out chat button" //The description of the engagement
}
```

#### OFFER_DISPLAY

This event is triggered when the engagement has been rendered and is going to be displayed on the page.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_DISPLAY" |
| appName | "LP_OFFERS" |

**Event Data**

See [START](#start) event.

*Example:*

```javascript
{
    "contexts": [
        {"EngagementContext": {"id": "2"}},
        {"pageContext": {"id": "1738225948"}}
    ],
    "campaignId": 248955910,//The campaign Id
    "engagementId": 248956110,//The engagement Id
    "engagementRevision": 14,//The revision we are going to show
    "engagementType": 6,//The engagement type
    "contextId": "2",//The context (instance in memory on the backend)
    "zoneId": 471288510,//The zone this is on
    "state": 2,//The current state of the agents (online, offline, busy) , to set the display state
    "confKey": "248955910_248956110_14",
    "tglName": "overlay",//The taglet that was downloaded
    "done": true,//If the configuration has finished loading
    "engagementName": "Mine"//The description of the engagement
}
```

#### OFFER_IMPRESSION

This event is triggered when the engagement has been displayed on the page.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_IMPRESSION" |
| appName | "LP_OFFERS" |

**Event Data**

See [START](#start) event.

####  OFFER_CLICK

This event is triggered when the engagement has been accepted by a user.

**Event information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_CLICK" |
| appName | "LP_OFFERS" |

#### OFFER_TIMEOUT

This event is triggered when an engagement duration has timed out.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_TIMEOUT" |
| appName | "LP_OFFERS" |

**Event Data**

See [START](#start) event.

#### OFFER_DECLINED

This event is triggered when an engagement is closed by a user.

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_DECLINED" |
| appName | "LP_OFFERS" |

**Event Data**

See [START](#start) event.

#### OFFER_REMOVE

This event is triggered when an engagement is removed from the DOM (auto or user initiated).

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "OFFER_REMOVE" |
| appName | "LP_OFFERS" |

**Event Data**

See [START](#start) event.

<!--
### Cobrowse Events

These are cobrowse-related events, including rendering, display and interactions with the engagement.

#### cobrowseOffered

This event is triggered when ...

**Event Information**

| Name | Value |
| :--- | :--- |
| eventName | "cobrowseOffered" |
| appName | "lpCoBrowse" |

**Event Data**

| Name | Description | Type / Value | Required |
| :--- | :--- | :--- | :--- |
| serviceId | ServiceId from the dialog | string | Yes |
| agentId | Agent ID | string | Yes |
| visitorName | Name of the Visitor | string | Yes |
| mode | Mode from the dialog | string | Yes |
| ssid | Monitoring Session ID | string | No |
| svid | Monitoring Visitor ID | string | No |
| scid | Monitoring Context ID | string | No |
| cid | Engagement Context ID | string | No |
| eid | Engagement ID | string | No |

*Example:*

```javascript
{
    serviceId: "<ServiceId from the dialog>",
 	agentId: "<Agent ID>",
 	visitorName: "<Name of the Visitor>",
 	mode: "<Mode from the dialog>",
 	//optional parameters:
 	ssid: "<Monitoring Session ID>",
 	svid: "<Monitoring Visitor ID>",
 	scid: "<Monitoring Context ID>",
 	cid: "<Engagement Context ID>",
 	eid: "<Engagement ID>"
}
```

#### cobrowseAccepted

#### cobrowseDeclined

#### sliderOpened
-->
