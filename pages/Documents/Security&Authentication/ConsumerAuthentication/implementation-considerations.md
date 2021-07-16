---
pagename: Implementation Considerations
redirect_from:
  - guides-authentication-implementation-considerations.html
  - authentication-implementation-considerations.html
sitesection: Documents
categoryname: "Security & Authentication"
documentname: Consumer Authentication
permalink: consumer-authentication-implementation-considerations.html
order: 2
indicator: both
---

### User Authentication 

**Brand's Digital Resources (Native Mobile App, Website)**  
It is the brand responsability to authenticate the user within the brand's digital resources. Once authentication is completed, "token exchange" should take place using the LivePerson SDK. The recieved token should indicates which user authenticated.  
LivePerson supports OIDC ID Tokens. The ID Token is a security token that contains claims about the authentication of an end-user by an authorization server when using a client, and potentially other requested claims. The ID Token is represented as a JSON Web Token ([JWT](https://openid.net/specs/openid-connect-core-1_0.html)).
Currently, LivePerson supports two methods for passing the ID Token: [implicit](https://oauth.net/2/grant-types/implicit/) or [code flow](https://oauth.net/2/grant-types/authorization-code/).

**LivePerson SDK** ([iOS](https://developers.liveperson.com/mobile-app-messaging-sdk-for-ios-overview.html), [Android](https://developers.liveperson.com/mobile-app-messaging-sdk-for-android-overview.html))  
This is a LivePerson layer embedded into the customer app (mobile/web). It mediates between the app and the LivePerson Service and provides the interaction conversation UI. This layer calls the mobile app to supply an OAuth 2.0 code whenever the LivePerson Service needs it.


### ID Token Exchange

**ID Token exchange using LivePerson's SDK for native mobile application**  
To authenticate a user (brand's consumer), the SDK requires an OAuth 2.0 code or JWT (depending on the specific flow) supplied by the mobile app. for implementation details please read [How It Works?](.....)

**ID Token exchange using JavaScript for web application**  
The customer web app is based on an embedded LivePerson's Web-SDK. The web app can display the embedded window originated by the LivePerson SDK, or open a Conversational Cloud popup window to interact with the consumer. When the Conversational Cloud embedded window is set to pop-out mode, the authentication must take place using a page redirect mechanism.


**Retrieving ID Token using 'Token Endpoint'**  
In case using token endpoint which accepts a valid OAuth 2.0 code along with the clientID and secret information, response should include a valid ID Token. The token should contain user unique identifier and additional claims, encoded and signed as a [JWT](https://tools.ietf.org/html/rfc7519). The clientID and secret information are encoded in
the Authorization header as per https://developers.liveperson.com/consumer-authentication-detailed-api.html#openid-connect-provider-op-development-details.

Example of ID Token Request (made by LivePerson to your authorization server):

```http
POST /oauth2/v3/token HTTP/1.1
Host: www.customer.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

code=3shshs92jsls/snxbxismNSsgHSVb&
redirect_uri=https://liveperson.net/oauth2/code_redirect&
grant_type=authorization_code
```

Example of ID Token Response (your authorization server response to LivePerson):

```http
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache

{
   "access_token": "SlAV32hkKG", # currently not in use
   "token_type": "Bearer",
   "expires_in": 3600,
   "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFlOWdkazcifQ.ewogImlzc
     yI6ICJodHRwOi8vc2VydmVyLmV4YW1wbGUuY29tIiwKICJzdWIiOiAiMjQ4Mjg5
     NzYxMDAxIiwKICJhdWQiOiAiczZCaGRSa3F0MyIsCiAibm9uY2UiOiAibi0wUzZ
     fV3pBMk1qIiwKICJleHAiOiAxMzExMjgxOTcwLAogImlhdCI6IDEzMTEyODA5Nz
     AKfQ.ggW8hZ1EuVLuxNuuIJKX_V8a_OMXzR0EHR9R6jgdqrOOF4daGU96Sr_P6q
     Jp6IcmD3HP99Obi1PRs-cwh3LO-p146waJ8IhehcwL7F09JdijmBqkvPeB2T9CJ
     NqeGpe-gccMg4vfKjkM8FcGvnzZUN4_KSP0aAp1tOJ1zZwgjxqGByKHiOtX7Tpd
     QyHE5lcMiKPXfEIQILVq0pc_E2DzL7emopWoaoZTF_m0_N0YzFC6g6EJbOEoRoS
     K5hoDalrcvRYLSrQAZZKflyuVCyixEoV9GfNQC3_osjzw2PAithfubEEBLuVVk4
     XUVrWOLrLl0nx7RkKU8NXNHq-rvKMzqg"
}

```

The id_token in the response is standard JWT and can be translated to the unpacked form. Here is an example of the unpacked id_token:

```json
{
   "iss": "www.customer.com",     # issuer
   "sub": "fdskjfd-user-id-3773hshshs",   # user id
   "exp": "1353801026",           # expiration timestamp
   "iat": "1353601026",             # token issuing  timestamp
   "email": "user@gmail.com",
   "picture": "http://www.customer.com/pics/fdskjfd-user-id-3773hshshs"
}
```

<div class="hide">Cleanup - Should add another component - Customer Authorization Endpoint, which is mandatory for external windows. This is the endpoint where users will log in and then be redirected to the external window page with the code/JWT as a query/hash param. Auth0 is an example for such a service, but the customer may want to implement their own landing page to manipulate query parameters and redirects rather than rely on a provided Auth service as is.)</div>


