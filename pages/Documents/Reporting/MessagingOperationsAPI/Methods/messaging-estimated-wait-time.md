---
pagename: Messaging Estimated Wait Time
redirect_from:
  - data-messaging-operations-messaging-estimated-wait-time.html
sitesection: Documents
categoryname: "Reporting"
documentname: Messaging Operations API
subfoldername: Methods
order: 40
permalink: messaging-operations-api-methods-messaging-estimated-wait-time.html

indicator: messaging
---

This method returns the current average wait time in queue, per requested skill. The estimated wait time is the time from a consumer's first message until an agent is assigned to the conversation. This method can help you to better manage your operations and monitor your service level across all skills on an account. Messaging estimated wait time is calculated every 10 seconds, therefore new data will only be available every 10 seconds.

**Notes**:

1. The Estimated Wait Time API is currently not available by default, in order to enable the data flow for this API please contact your account manager.

2. This method will only return a result, as long as there is enough throughput to reliably calculate an estimated wait time. The throughput used is the number of assigned conversations to agent. An acceptable throughput starts at 120 conversations per hour, per skill. This will be enough for the API to calculate the estimated wait time and provide an answer to the call found below.

3. This API returns real time data, based on your current capacity. The API will provide accurate estimations as long as there are no major changes with your agents' capacity. Major changes can be defined as any change over 15% in your agents' capacity. If major changes occur (for example, several agents log off at the same time), previous estimated wait times are no longer valid. In that case, it is recommended to wait 10-15 minutes before calling the API again in order to make sure the data is recalculated and accurate.

4. This API should not be called more than every 10 seconds per skill.

5. **Limitation**: in order for the queue data to appear, there must be at least one agent logged in to LE.

### Retrieving Messaging Estimated Wait Time Data by Account and Skills

| Method | URL |
| :--- | :--- |
| GET | https://[{domain}](/agent-domain-domain-api.html)/lp-messaging-ewt-app/api/account/{accountID}/ewt?skills=<skillIDs>&v=<version> |

 - Note: Data for at most 300 skills will be returned.

**URL Parameters**

| Name | Description | Type / Value | Required |
| :----- | :-------------- | :-------------- | :--- |
| v | version of API e.g. v=1 | numeric | default: 1 |
| skills | When provided, the response will contain estimated wait time data for the requested skill Id/s. When not provided, the response will contain estimated wait time data for all skills of the account. If there is no data for the specified skill/s an object will be returned with value -1 for key: "estimatedWaitTime". You can provide one or more skill Ids. If you provide several skill IDs, they must be comma-separated. Example: skills=4,15,3. | numeric, separated by commas | optional |

**Response Body**

This is an example response which contains information for two skills, skills=2,3 where there is data only for skill "3".

```json
    {
        "estimatedWaitTimeResponse": [
            {
                "skillId": 2,
                "estimatedWaitTime": -1,
                "timestamp": 1526466893703
            },
            {
                "skillId": 3,
                "estimatedWaitTime": 10,
                "timestamp": 1526466893703
            }
        ]
    }
```

**Elements in the Response**

| Name | Description | Type / Value |
| :----- | :------------- | :-------------- |
| estimatedWaitTimeResponse | A list that contains elements which represent skills' data. | element |
| skillId | The skill Id. | long |
| estimatedWaitTime | The estimated wait time in seconds. | long |
| timestamp | The time of the response in UTC time stamp in milliseconds. | long |

**Possible Response Codes**

| Code | Response |
| :----- | :--------- |
| 200 | OK - Successfully retrieved the data. |
| 400 | Bad request - Problem with body or query parameters. |
| 401 | Unauthorized - Bad Authentication. |
| 403 | Forbidden - Bad Authorization (invalid permissions). |
| 500 | Internal Server Error - Please try again after the time specified in the response has passed. |
