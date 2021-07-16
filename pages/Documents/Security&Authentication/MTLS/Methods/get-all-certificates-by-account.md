---
pagename: Get all certificates by account
keywords:
sitesection: Documents
categoryname: "Security & Authentication"
documentname: MTLS 
subfoldername: Methods
permalink: mtls-methods-get-all-certificates-by-account.html
---

This API gets all certificates from a specific account by account ID.

### Request

 |Method|      URL|  
 |:--------  |:---  |
 |GET|  https://[{domain}]/mtls/account/{accountId}/certificates |


**Request Headers**

 |Header         |Description  |
 |:------|        :--------  |
 |Authorization|    Contains token string to allow request authentication and authorization.  |



**Path Parameters**

 |Parameter|  Description|  Type/Value |
 |:------    |:--------    |:--------|
 |accountId|  LP site ID |   String |

### Response

**Response Codes**

| Code | Description           |
|------|-----------------------|
| 200  | OK                    |
| 401  | Not Authenticated     |
| 403  | Not Authorized        |
| 500  | Internal Server Error |


**Response Body**

for example:

```JSON
[
  {
      "id": 3515906310,
      "deleted": false,
      "name": "Cert1",
      "displayName": "Cert1",
      "siteId": "le1606809",
      "status": "UnAvailable",
      "expirationDate": null
  }
]
```

**Entity Structure:**

| Attribute | Description  | Type/Value | Required | Notes |
| :------   | :--------    | :-------- | :--- | :--- |
| id | A certificate's unique object ID in the account config table. | long number | Read only | |
| deleted   | Indicates whether the certificate is deleted or not. | Boolean | Read only | |
| name | A certificate's unique name. | unique string | Required | |
| displayName    | A certificate's display name.  | string | Required | |
| siteId | The account ID the certificate is associated with. | string | Required | |
| status | Indicates if the certificate is available/not available/expired | string | Required | (the certificate is available if it exists at both Hashicorp Vault and LivePerson's Data Base and if isn't expired)|
| expirationDate | certificate's expiration date. | string | Not Required | |
