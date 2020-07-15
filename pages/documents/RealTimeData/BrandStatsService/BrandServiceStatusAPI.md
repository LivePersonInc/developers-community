---
pagename: BrandServiceStatusAPI
redirect_from:
sitesection: Documents
categoryname: "RealTimeData"
documentname: BrandServiceStatusAPI
permalink: BrandServiceStatusAPI.html
indicator:
---

### Introduction

The following document outlines the Brand Stats Service API. This API presents the status of system test proceedures in a brand scope.
Details on the tests that are avaialble can be found in the [here](/BrandStatusService_test-details.html)

**Service Domain**
Please ask your account team to indicate which domain of the below domains your account is in. This can also be seen in the URL in your production account when accessing your Conversational Cloud / Conversation Manager interface.

| Service Domain | Brand Service Status API Domain      |
| :------------- | :----------------------------------- |
| VA:            | https://va.bstats.int.liveperson.net |
| CA:            | https://ca.bstats.int.liveperson.net |
| SY:            | https://sy.bstats.int.liveperson.net |
| ME:            | https://me.bstats.int.liveperson.net |
| LO:            | https://lo.bstats.int.liveperson.net |
| AM:            | https://am.bstats.int.liveperson.net |
| LO:            | https://lo.bstats.int.liveperson.net |

#### Request

| Method | URL                                                 |
| :----- | :-------------------------------------------------- |
| GET    | https://{Service Domain}/account/[accountID]/bstats |

**Security**
Brand Stats Service requires an external appKey that shall be validated against LivePerson authentication service. The customer specific appKey should be generated in the [API Key creator](https://developers.liveperson.com/api-guidelines-create-api-keys.html)

| Parameter  | Description                   | Type | Required | Notes |
| :--------- | :---------------------------- | :--- | :------- | :---- |
| ApiKeyAuth | App key generated for Account |      | Required |       |

**Parameters**

| Parameter | Description                   | Type   | Required | Notes                                                                                                                                  |
| :-------- | :---------------------------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| accountId | Brands Status Service account | string | Required | Brand Status account is NOT the Brand's production account, but is the designated account where the testing proceedures are configured |

**Body**

**Example cURL**:

{: .important}
**Please note** Make sure to replace [`{Domain}`](#step-1-identify-the-third-party-bots-api-domain), `{accountId}`, `{userName}` and `{password}` from the below command with your information

```bash
curl -X GET \
 https://bstats-qa-int.dev.lprnd.net/api/account/le74292582/bstats \
 -H 'accept: */*' \
 -H 'authorization: OAuth .....
 -H 'cache-control: no-cache' \
 -H 'content-type: application/json' \
```

The image below presents an example GET request performed in Postman
<img class="fancyimage" style="width:600px" src="img/bstats_curl_postman.png">

**Response**:

#### Example Response

Example response of the GET request returned by the API will look like this

```json
{
    "accountId": "123456789",
    "updateTimestampMilliseconds": 1592471558173,
    "servicesStatus": [
        {
            "total": 6,
            "failure": 0,
            "success": 6,
            "timestampSeconds": 1592471558,
            "name": "Messaging Agent And Consumer"
        },
        {
            "total": 6,
            "failure": 0,
            "success": 6,
            "timestampSeconds": 1592471558,
            "name": "All connection"
        },
        {
            "total": 6,
            "failure": 0,
            "success": 6,
            "timestampSeconds": 1592471558,
            "name": "Predefined Content"
        }
    ]
}

In case account is not define in Sheriff, response will be:

{
    "accountId": "123456789",
    "updateTimestampMilliseconds": 1592471742150,
    "servicesStatus": []
}

```

### Response Codes

| Code | Response                                                             |
| :--- | :------------------------------------------------------------------- |
| 200  | OK - request for the given API succeeded.                            |
| 400  | Client error                                                         |
| 401  | Unauthorized - Invalid bearer token.                                 |
| 403  | Forbidden                                                            |
| 404  | Not Found - If the provided conversation Id is invalid or not found. |
| 500  | Server error                                                         |
| 503  | Temporary error                                                      |

Due to security considerations, we cannot return messages explaining the error, but only the generic and code errors. LivePerson support and technical team can help with further investigations should you encounter these errors.
