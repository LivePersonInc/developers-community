---
pagename: Overview
redirect_from:
  - data-data-access-overview.html
sitesection: Documents
categoryname: "Historical Data"
documentname: Data Access API

level-order: 1
order: 1
permalink: data-access-api-overview.html
root-link: true
indicator: chat
---

### Introduction

{: .notice}
Our Data APIs enable you to retrieve many attributes and information types. [Please see this table](https://developers.liveperson.com/api-guidelines-api-data-metrics.html) for the different types of information and attributes which are retrievable via both our Historical and Real Time Data APIs.

The Conversational Cloud Data Access API provides brands with the ability to address specific Goals and KPIs while also extending the reporting capabilities of their account by accessing their entire raw data. The data includes full information about their agents’ activities and visitors’ journeys.

Brands can use this data in data warehouse systems as well as create customized reports from a combination of their own data, data provided by Conversational Cloud advanced analytics and other 3rd parties data system they are working with.

Data access is not a default function of Conversational Cloud; it must be configured separately for each account.
The four types of data supported and configurable in each account are as follows:

* Agent Activity
* Web Session
* Engagement
* Survey

The Data Access API retrieves historical data. This API is based on the REST architecture style and supports the HTTPS GET protocol (data retrieval), all retrieved data is returned in JSON format.

**Note**

Data Access retention is limited to a 30 days period in order to comply with the GDPR. The GDPR (General Data Protection Regulation) is a European Union regulation that is aimed to protect personal data of individuals within the EU.

### Getting Started

A few things you'll need to get started with this API:

1. **There's no need to reterive your domain for this API**. Here are the different domains by geo location:

	* US accounts: va.da.liveperson.net

	* UK accounts: lo.da.liveperson.net

	* APAC accounts: sy.da.liveperson.net

2. This API requires authorization using API key that is available in the Conversational Cloud API Keys tab.

3. [Here are the API terms of use](https://www.liveperson.com/policies/apitou).  

4. This API requires backend enablement, please contact your account manager to do so.


### Architecture

![DataAccessAPI](img/dataaccess.png)

JSON-Generating Data Flow Process:

1. Every visitor and/or agent action triggers an event.
2. Events are stored in HDFS (Hadoop File System).
3. Job processes the events (in the Hadoop environment) and generates a grouping of all the events related to each session once they are considered “closed”.
4. A data access job then runs

![DataAccessAPI02](img/Data access-02.png)


### Use Cases

1. Brands that handles multiple contact centers in different regions can now pull the agent activity data per region and review their agents’ utilization. The data contains information on status change the agent has made during his shift. The brand can then integrate the data with specific regional information from their workforce management system.

2. If a brand has a customer membership programs, they can learn whether their premium members are indeed the heaviest buyers. They can use the order value variable from LivePerson against their own customer membership data and compare the Average Order Value for each membership segment.
