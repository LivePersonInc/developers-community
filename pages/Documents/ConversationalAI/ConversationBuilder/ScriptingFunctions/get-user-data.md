---
pagename: Get User Data
redirect_from:
    - conversation-builder-scripting-functions-get-and-set-user-data-and-variables.html
Keywords:
sitesection: Documents
categoryname: "Conversational AI"
documentname: Conversation Builder
subfoldername: Scripting Functions
permalink: conversation-builder-scripting-functions-get-user-data.html
indicator: both
---

Use the following built-in functions to get user data.

### Get user channel
Returns the platform channel the user is currently communicating on. This function returns:

* lp_sms (for SMS)
* lp_web (for Web)
* lp_inapp (for In-app SDK)
* lp_whatsapp (for WhatsApp)
* lp_rcs (for RCS)
* lp_abc (for Apple Business Chat)
* twilio_sms (for Twilio SMS)
* lp_fb (for Facebook)

The "lp_" prefix indicates the LivePerson platform.

| Function Name | Arguments | Returns |
| --- | --- | --- |
| `getUserChannel()` | None | lp_sms, lp_web, lp_inapp, lp_whatsapp, lp_rcs, lp_abc, twilio_sms, or lp_fb |

#### Example

```javascript
var channel = botContext.getUserChannel();
botContext.printDebugMessage("channel used by the user is: " + channel);
```


### Get user platform ID

Get User Platform Id is used to get the user’s unique platform ID.
// === REQUEST FOR IMPROVED DOCUMENTATION ===
// Please explain what the platform ID is: 
// - Does it identify the platform of the user, or the user ID within the platform? 
// - What is a platform in this context (how is a platform different from a channel)?
// Please provide examples (i.e. WhatsApp number?, Facebook id?).
// === END OF REQUEST FOR IMPROVED DOCUMENTATION ===


| Function Name | Arguments | Returns |
| --- | --- | --- |
| `getUserPlatformId()` | None | string: unique User platform ID |

#### Example

```javascript
// get the user’s platform ID
var userId = botContext.getUserPlatformId();
// display the results...
botContext.printDebugMessage('The userPlatformId = ' + userId);
```

### Get authenticated customer info

There are two built in methods to return authenticated customer information. You can attempt to see if either of these 2 methods return true or not.  If the visitor is authenticated, (typically they would set personal or customer info being logged in) you can access the Personal Info or Customer Info object array.


| Function Name | Arguments | Returns |
| --- | --- | --- |
| `getLPUserPersonalInfo()` | See below for accessing attributes | [personal info](engagement-attributes-types-of-engagement-attributes.html#personal-info) object or nothing |
| `getLPCustomerInfo()` | See below for accessing attributes | [customer info](engagement-attributes-types-of-engagement-attributes.html#customer-info) object or nothing |

#### Personal info example

This is an example JSON object for the Personal Info. Keep in mind that not all fields may be available for your conversation. In addition, one of the following fields (firstname, lastname, company) must be populated for this object to return, otherwise it will be null.

```json
{
    "type": "personal",
    "personal": {
        "firstname": "John",
        "lastname": "Doe",
        "age": {
            "age": 34,
            "year": 1980,
            "month": 4,
            "day": 1
        },
        "contacts": [
            {
                "email": "myname@example.com",
                "phone": "+1 555-333-7777"
            }
        ],
        "gender": "MALE",
        "language": "en-US",
        "company": "company"
    }
}
```

Here is how you might use the `getLPUserPersonalInfo()` method in JavaScript to check for a user’s first and last name.

```javascript
var personalInfo = botContext.getLPUserPersonalInfo();
botContext.printDebugMessage('PERSONAL INFO:'+personalInfo);
if(personalInfo){
    var fullName = personalInfo.firstname+" "+personalInfo.lastname;
    botContext.printDebugMessage('Full Name: '+fullName);
    botContext.setBotVariable("fullName",fullName,true,false);
}
```

#### Customer info example

Here is an example JSON object for the Customer Information.

```json
{
    "type": "ctmrinfo",
    "info": {
        "companyBranch": "test",
        "ctype": "vip",
        "customerId": "138766AC",
        "balance": -400.99,
        "currency": "USD",
        "socialId": "11256324780",
        "imei": "99887766554433",
        "userName": "user000",
        "companySize": 500,
        "accountName": "bank corp",
        "role": "broker",
        "lastPaymentDate": {
            "day": 15,
            "month": 10,
            "year": 2014
        },
        "registrationDate": {
            "day": 23,
            "month": 5,
            "year": 2013
        },
        "storeNumber": "123865",
        "storeZipCode": "20505"
    }
}
```

Here is how you might use the `getLPCustomerInfo()` method in JavaScript to check for a user’s customerId.

```javascript
var customerInfo = botContext.getLPCustomerInfo();
if(customerInfo){
    var customerId = customerInfo.customerId;
    botContext.printDebugMessage('customerId: '+customerId);
    botContext.setBotVariable("customerId",customerId,true,false);
}
```
