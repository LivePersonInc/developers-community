---
pagename: Overview
redirect_from:
  - rt-interactions-engagement-attributes-overview.html
sitesection: Documents
categoryname: "Website Monitoring"
documentname: Engagement Attributes API

order: 1
permalink: engagement-attributes-api-overview.html
root-link: true
level-order: 6

indicator: both
---
### Introduction

This API provides a way to report back to LivePerson consumer events such as the topic and resolution of the conversation during the session (e.g., call). This information is added to the existing session and can be used in the goal reached calculation.

### Getting Started

A few things you'll need to get started with this API:

1. **Retrieve your domain**. Use the [LivePerson Domain API](agent-domain-domain-api.html) to retrieve this information by providing the following service name:

	* smt
	
**SUGGESTION**: place an inline lookup widget here: enter account number, retrieve domain for this API/service name.

2. In order to utilize this API, you will need an API key. [Here are the instructions on how to get that](guides-gettingstarted.html).

3. [Here are the API terms of use](https://www.liveperson.com/policies/terms-of-use).
