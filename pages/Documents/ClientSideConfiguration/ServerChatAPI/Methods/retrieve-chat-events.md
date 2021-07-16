---
pagename: Retrieve Chat Events
redirect_from:
  - consumer-experience-server-chat-retrieve-chat-events.html
sitesection: Documents
categoryname: "Client Side Configuration"
documentname: Server Chat API
subfoldername: Methods

order: 90
permalink: server-chat-api-methods-retrieve-chat-events.html

indicator: chat
---


This method retrieves the chat events. The possible event types include: state, url, line and a2a-transfer. You should use this method to periodically poll for new events in the chat session. The method for polling should always be the URI specified in the "next" link tag. This will retrieve a document that only contains events added after your last poll.

### Request

| Method | URL  |
| :--- | :--- |
| GET | https://[{domain}](/agent-domain-domain-api.html)/api/account/{accountId}/chat/{chatId}/events?v=1&NC=true |

**Formats**

- XML
- JSON

**Request Headers**

| Header | Description |
| :--- | :--- |
| Authorization | LivePerson appKey=721c180b09eb463d9f3191c41762bb68 |
| Content-Type | application/json |
| Accept | application/json |

**Parameters**

| Name  | Description | Type/Value |
| :--- | :--- | :--- |
| from | The ID of the first event that is shown in the response. | numeric |
| appkey | 721c180b09eb463d9f3191c41762bb68 | string |

### Response

**Response Codes**

| Code | Description |
| :--- | :--- |
| 200 | Successful |

JSON Example:

```json
    {
      "events": {
        "link": [
          {
            "@href": "https://{domain}/api/account/{accountId}/chat/{chatId}/events",
            "@rel": "self"
          },
          {
            "@href": "https://{domain}/api/account/{accountId}/chat/{chatId}/events?from=5",
            "@rel": "next"
          }
        ],
        "event": [
          {
            "@id": "0",
            "@type": "state",
            "time": "2017-02-27T06:30:00.695-05:00",
            "state": "waiting"
          },
          {
            "@id": "1",
            "@type": "line",
            "time": "2017-02-27T06:30:00.696-05:00",
            "textType": "plain",
            "text": "Thank you for choosing to chat with us.",
            "by": "info",
            "source": "system",
            "systemMessageId": "4",
            "subType": "REGULAR"
          },
          {
            "@id": "2",
            "@type": "state",
            "time": "2017-02-27T06:30:25.502-05:00",
            "state": "chatting"
          },
          {
            "@id": "3",
            "@type": "line",
            "time": "2017-02-27T06:30:25.502-05:00",
            "textType": "plain",
            "text": "You are now chatting with Natalie.",
            "by": "info",
            "source": "system",
            "systemMessageId": "3",
            "subType": "REGULAR"
          },
          {
            "@id": "4",
            "@type": "line",
            "time": "2017-02-27T06:30:31.655-05:00",
            "textType": "html",
            "text": "<div dir=\"ltr\" style=\"direction: ltr; text-align: left;\">hi</div>",
            "by": "Natalie",
            "source": "agent",
            "subType": "REGULAR"
          }
        ]
      }
    }
```

**Elements in the Response**

| Name | Description | Type/Value | Notes |
| :--- | :--- | :--- | :--- |
| time | The time the event occurred. | time | |
| text | Content of the chat. | alphanumeric | |
| textType | The type of message. | plain/html | |
| by | Type of message that is sent. | string | Valid values: "info", "agent", "visitor" |
| source | Indication of who sent the message. | string | Valid values: "system", "agent", "visitor" |
| systemMessageId | The ID of the message. | string | See System Messages below.|

**System Messages**

Messages that are initiated by the system. These messages are added with the `<systemMessageId>` element tag. The following table describes the available messages and IDs. **Please note**: while the **systemMessageID** field in the response is numeric, it is a number passed as a string.
​

| ID | Event |
| :--- | :--- |
| 4 | Routing chat to an operator. |
| 22 | Ticket ID associated with chat. |
| 5 | Operator ends chat. |
| 3 | Operator accepts chat. |
| 2 | Site operators are currently busy. |
| 13 | Chat is transferred to an operator. |
| 15 | Chat is transferred to another skill group. |
| 6 | Chat is unexpectedly disconnected. |
| 23 | Chat requeued by system. |

**Event type="state" Parameters**

| Name | Description | Type/Value | Notes |
| :--- | :--- | :--- | :--- |
| time | The time the event occurred. | time | |
| state | The state of the chat. | string | Valid values: "waiting", "chatting", "ended" |

**Event type="a2a-transfer" Parameters**

| Name | Description | Type/Value | Notes |
| :--- | :--- | :--- | :--- |
| time | The time the event occurred. | time | |
| domain | The domain of the target account. | alphanumeric | |
| chatRequestParameters | The parameters for the chat request. | alphanumeric | Should be taken as is and sent in the body of the chat request to the target account.  |
| a2aEventId | The id of the a2a-transfer event.  | alphanumeric | Needed for the target account to identify the a2a-transfer chat request. |
| a2aSourceSessionId | The session id in the source account. | alphanumeric | Needed for the target account to identify the a2a-transfer chat request. |
| a2aSourceSiteId |  The id of the source account. | alphanumeric | Needed for the target account to identify the a2a-transfer chat request. |
| skill | The skill of the target account. | alphanumeric | |
| remoteSiteId | The id of the target account.  | numeric | |
| a2a-transfer | URI to initiate a request to chat after the a2a-transfer. | link relationship | |
