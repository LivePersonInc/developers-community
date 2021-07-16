---
pagename: Skill Availabilities
sitesection: Documents
categoryname: "Agent Manager Experience"
documentname: Agent manager workspace API
subfoldername: methods
order: 10
permalink: agent-manager-workspace-api.html
indicator: messaging
---

### General

Skill availability API retrieves the number of available agents per login status, grouped by skill

### Request

Method | URL
------ | ---------------------------------------------------------------------------------------------------
POST| https://[{domain}](/agent-manager-domain-api.html)/manager_workspace/api/account/{accountId}/skill/availability

Note: The amount of retrieved skills is limited by configuration, default value is 1000.<br/>
 
**BODY Parameters** 

Note: Should be a valid JSON object, at least empty body ("{}")

|Name  | Description | Type/Value  | Required | Notes|
|:---- | :---------- | :---------- | :------- | :---|
|filters | Contains parameters to filter by. | Container  | Optional |

_filters info_ 

|Name  | Description | Type/Value  | Required | Notes|
|:---- | :---------- | :---------- | :------- | :---|
|userTypes | Type of the user conducting the conversation. | alphanumeric  | Optional | Valid values: SYSTEM, HUMAN, BOT. 
    
Request body - json example:

```json
{
    "filters": {        
        "userTypes": [
            "HUMAN"
        ]
    }        
}
```


### Response

Name| Description | Type/Value
:-------- | :------------------------------------------------- | :-----------------
metadata | All response-related Metadata.| container
skillAvailabilities  | List of skill availabilities records. Only skills with at least one available agent are returned | container

_metadata info_

Name| Description | Type/Value
:-------- | :------------------------------------------------- | :-----------------
count  | Number of returned skills.| long

_skillAvailabilities info_

| Name| Description | Type/ Value| Notes|
|-----|-------------|------------|------| 
| skillId| The skill Id. | Long | 
| onlineAgents| The number of online agents.| Long |
| backSoonAgents| The number of back soon agents.| Long |
| awayAgents| The number of away agents.| Long |

Response DTO - json example:

```json
{
    "metadata": {
        "count": 2
    },
    "skillAvailabilities": [ {
            "skillId": 3680508910,
            "onlineAgents": 1,
            "backSoonAgents": 2
        }, {
            "skillId": 3680508912,
            "awayAgents": 1            
        }
    ]
}
```
