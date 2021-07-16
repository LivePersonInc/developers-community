---
pagename: Limitations & Restrictions
keywords:
sitesection: Documents
categoryname: "Developer Tools"
documentname: LivePerson Functions
subfoldername: Developing with FaaS
permalink: liveperson-functions-developing-with-faas-limitations-restrictions.html
indicator: both
redirect_from:
  - function-as-a-service-developing-with-limitations-restrictions.html
  - liveperson-functions-developing-with-faas-limitations-restrictions.html#connectivity
---

The following section describes the limitations and restrictions of the platform

- [Timeouts](#timeouts)
- [HTTP-Requests](#http-requests)
- [Lambda](#lambda)
- [Logging](#logging)

### Timeouts

The usage of `setTimeout()` in LivePerson Functions must be handled with care.

* Functions cannot exceed the runtime of **30 seconds**. The error `Lambda Execution is taking too long` will be thrown.
* If a function is at high load and it contains a `setTimeout()` call, the event loop of the service may fill up. Even functions with a lower execution time than 30 seconds could therefore take longer, may reach the execution time limit and fail. Because of this, it's important to double check if timeouts cannot be avoided in your use case.

### Connectivity

* HTTP/HTTPS based protocols.
* MTLS is supported, but we don't track certificate expiration.
* Max. 20 requests/sec (all beyond that are rejected with `429 - Too Many Requests`) per Lambda.

### Lambda

* Multiple Requests will be batched and processed by the same instance. There is not an instance per request.
* The source code must not exceed the length of `100.000` characters.
* The resources of a lambda are limited. CPU is capped at `500m` and the memory at `256 MB`. So beware, if you want to use for example large file processing inside a function and reach this limit the function will stop immediately and the invocation will fail (no results will be saved).

### Logging

* Logs written during invocation are limited to 10 entries, with an overall maximum of `6000` characters per lambda invocation (including log `message` and `extras`). If this limit is exceeded, only 1 error log will be stored.
* Be aware that logs written during manual test invocations will not be written into the storage. Logs with a Debug level will only be shown on manual test invocations and not written into the storage.
* The maximum timespan between Start Date and End Date of the `Investigate Function Logs` screen is restricted to 7 days.

<img src="img/faas-limitations-investigate-logs.jpg" alt="LivePerson Functions Logs" style="width:80%;"/>

### Deployment History

The deployment history will be stored indefinitely. However, only the 5 most recent versions will be stored for inspection and restoration. If you require a more expansive history we'd urge you to look into using VCS outside of LivePerson systems in combination with our CLI.