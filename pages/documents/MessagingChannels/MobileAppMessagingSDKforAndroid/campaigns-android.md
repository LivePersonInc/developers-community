---
pagename: Campaigns
redirect_from:
  - consumer-experience-android-sdk-advanced-campaigns.html
Keywords:
sitesection: Documents
categoryname: "Messaging Channels"
documentname: Mobile App Messaging SDK for Android
subfoldername: Advanced Features

order: 291
permalink: mobile-app-messaging-sdk-for-android-advanced-features-campaigns.html

indicator: messaging
---


Campaigns are the cornerstone of LiveEngage - the place where every digital engagement is created and organized. By using campaigns, brands can target specific audiences in order to achieve their business goals, such as increasing sales or generating leads.

Using the Monitoring APIs, brands can:

* Report on the customer’s journey inside the app

* Get engagements based on the reported SDEs

* Route conversations to a specific skill (based on engagements)

While web messaging allows automatic capturing of events (using the LE Tag), when using campaigns for In-App Messaging, it is up to the app to report the various events by using the In-App Monitoring APIs as will be explained in this guide.

### Prerequisites

- Follow the steps in the [Campaigns for Messaging guide](https://s3-eu-west-1.amazonaws.com/ce-sr/CA/Campaigns/Mobile+App+Engagement+Configuration+Guide.pdf) **before** adding the implementation to a mobile app.

- The SDK must be initialized with the `MonitoringInitParams` object.

### Notes & Best Practices

* To start a conversation with a specific campaign and engagement, provide a `CampaignInfo` object to the `ConversationViewParams` object.

* A monitoring session is a 6-hours window. All SDEs that report during the session get aggregated.

* If not reporting any SDEs (idle) for 30 minutes, a new session starts when reporting the next SDE.

### Monitoring APIs

The Monitoring APIs provide brands access to the LivePerson monitoring system. The APIs can be used for reporting engagement attributes and to retrieve engagements. The eligibility for an engagement is based on campaigns and an engagement's definitions.

Monitoring APIs include two APIs:

* [sendSDE](android-monitoring_api.html) - Sends engagement attributes to LivePerson. Should be used whenever the app would like to report on an engagement attribute.

* [getEngagement](android-monitoring_api.html) - In case that there are a matching campaign and engagement, getEngagement returns an engagement.  

### Code Samples

#### conversationViewParams

```java
ConversationViewParams conversationViewParams = new ConversationViewParams();
// Creating a campaignInfo object
CampaignInfo campaignInfo = new CampaignInfo(campaignId, engagementId, engagementContextId, sessionId, visitorId);
// Adding the created CampaignInfo to the conversationViewParams
conversationViewParams.setCampaignInfo(campaignInfo);

LPAuthenticationParams lpAuthenticationParams = new LPAuthenticationParams(LPAuthenticationParams.LPAuthenticationType.AUTH);
lpAuthenticationParams.setAuthKey(authCode);

// Presenting the conversation window. If a new conversation starts, it will be routed according to the engagement in campaignInfo
LivePerson.showConversation(activity, lpAuthenticationParams, conversationViewParams);
```

#### getEngagement API

Use this API to send engagement attributes (as part of the request body).  As an optional parameter, you can pass MontoringParams, which includes PageId, Entry Points, and Engagement Attributes for routing the conversation. Available parameters include:

   - context: application context

   - consumerID: an optional brand app consumer ID 

   - monitoringParams: an instance of includes optional PageId, JSONArray of Entry Points and a JSONArray of Engagement Attributes

   - EngagementCallback: operation callback: onSuccess() response with LPEngagementResponse that contains pageId, sessionId, visitorId and engagementDetailsList onError() response with the MonitoringErrorType 


```java
// Calling getEngagement and providing the created identityList and monitoringParams (includes entryPoints and engagementAttriutes)
LivepersonMonitoring.getEngagement(context, identityList, monitoringParams, new EngagementCallback() {
			@Override
			public void onSuccess(@NotNull LPEngagementResponse lpEngagementResponse) {
				...
			}

			@Override
			public void onError(@NotNull MonitoringErrorType errorType, @Nullable Exception exception) {
				...
			}
		});
```



#### Initialize SDK with Monitoring

```java
// Creating init object for the Monitoring APIs
MonitoringInitParams monitoringInitParams = new MonitoringInitParams("AppInstallId");

// Initializing the SDK with the created MonitoringInitParams
LivePerson.initialize(context, new InitLivePersonProperties(brandId, appId, monitoringInitParams, new InitLivePersonCallBack() {

  @Override
  public void onInitSucceed() {
    ...
  }

  @Override
  public void onInitFailed(Exception e) {
    ...
  }
}));
```

#### Monitoring parameters example

```java
// Creating Identities array.
ArrayList<LPMonitoringIdentity> identityList = new ArrayList<>();
// Creating the identity Object and adding to the array
// ConsumerId - unique and non-guessable identifier of the consumer. Should be the same consumer id provided in the JWT
// BrandIssuer - Issuer, who identified the consumer - usually the brand.
LPMonitoringIdentity monitoringIdentity = new LPMonitoringIdentity("ConsumerId", "BrandIssuer");
identityList.add(monitoringIdentity);

// Creating entryPoints object
JSONArray entryPoints = new JSONArray();
//
// The next 3 lines are confusing developers. They give the impression that the entryPoints data will be available
// in LiveEngage to match Engagements based on either URL or Section, and using language. This is not the case currently.
// As currently implemented, the contents of each of the 3 lines below will appear in LiveEngage as section names exactly as
// they are typed below - for example section 'http://www.liveperson-test.com', section 'sec://food' and section 'lang://De'
//
// So, either the lines below should be changed to highlight that entryPoints simply match to sections within LiveEngage
// and the examples should be changed to something more meaningful
//
// OR - better yet
//
// The parsing within LiveEngage of entryPoints should be fixed to match what this example suggests was the original intention
// with the
// http line getting presented in LiveEngage as the current URL
// sec line(s) getting presented in LiveEngage as the current section(s) 
// lang line getting presented in LiveEngage as the current/desired language of the visitor
//
// Whichever is the outcome - some clarification of how the entryPoints are used is needed. 
entryPoints.put("http://www.liveperson-test.com");
entryPoints.put("sec://Food");
entryPoints.put("lang://De");

// Creating engagement attributes
JSONArray engagementAttriutes = new JSONArray();
JSONObject purchase = new JSONObject();
purchase.put("type", "purchase");
purchase.put("total", 11.7);
purchase.put("orderId", "Dx342");

JSONObject lead = new JSONObject();
lead.put("leadId", "xyz123");
lead.put("value", 10500);

engagementAttriutes.put(purchase);
engagementAttriutes.put(lead);

MonitoringParams monitoringParams = new MonitoringParams("PageId", entryPoints, engagementAttriutes);
```




#### sendSde API

Use this API to report engagement attributes (SDEs).  Available parameters include:

   - context: application context 
   
   - consumerID: brand app consumer ID  

   - monitoringParams: an instance of LPMonitoringParams that includes an optional Array of Entry Points and an optional dictionary of Engagement Attributes.  An additional optional parameter is PageID, which you use for Page identification for sending events on the current engagement. LPSdeResponse and LPtEngagementResponse received the PageID.

   - SdeCallback: operation callback: onSuccess() response with LPSdeResponse that contains pageId, sessionId and visitorId onError() response with the MonitoringErrorType.


```java
// Sending engagement attributes and providing the created identityList and monitoringParams (includes entryPoints and engagementAttriutes)
LivepersonMonitoring.sendSde(context, identityList, monitoringParams, new SdeCallback() {
  @Override
  public void onSuccess(@NotNull LPSdeResponse lpSdeResponse) {
    ...
  }

  @Override
  public void onError(@NotNull MonitoringErrorType errorType, @Nullable Exception exception) {
    ...
  }
});
```


