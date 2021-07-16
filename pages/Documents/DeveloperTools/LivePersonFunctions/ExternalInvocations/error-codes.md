---
pagename: Error Codes
keywords:
sitesection: Documents
categoryname: "Developer Tools"
documentname: LivePerson Functions
subfoldername: External Invocations
permalink: liveperson-functions-external-invocations-error-codes.html
indicator: both
redirect_from:
---

This section describes possible errors that can occur when invoking a lambda from outside LivePerson's platform.

## Error codes

| Error                                               | Description                                                                                                     |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| 'com.liveperson.faas.es.general'                    | General error, no specific reason                                                                               |
| 'com.liveperson.faas.es.unavailable'                | Could not reach/access remote system                                                                            |
| 'com.liveperson.faas.es.badinput'                   | Payload was in the wrong format or value was missing                                                            |
| 'com.liveperson.faas.es.notdeployed'                | Lambda that is being invoked, is not deployed                                                                   |
| 'com.liveperson.faas.es.missinglambda'              | Lambda does not exist                                                                                           |
| 'com.liveperson.faas.handler.custom-failure'        | Lambda calls the callback with an Error like callback(new Error('whoops'), null)                                |
| 'com.liveperson.faas.handler.runtime-exception'     | Lambda crashes because of implementation error, such as accessing a variable that is `undefined`.               |
| 'com.liveperson.faas.handler.executiontime-exceeded' | Lambda exceeds execution time See [here](liveperson-functions-monitoring-logs.html) |
| 'com.liveperson.faas.handler.log-limit-reached'     | Lambda exceeds log limits See [here](liveperson-functions-monitoring-logs.html)     |
| 'com.liveperson.faas.fm.general'                    | General error, no specific reason                                                                               |
| 'com.liveperson.faas.fm.unavailable'                | Could not reach/access remote system                                                                            |


## Http codes

| Code                                               | name             | Description                                              |
|----------------------------------------------------|-----------------|-----------------------------------------------|
| 200,202       |   Success                             | Request was successfully accepted/processed   |
| 400           |   Bad Request                         | The request is either not correct or malformed                                            |
| 401,403       |   Unauthorized                        | Missing authentication or missing privileges                   |
| 404           |   Not Found                           | Requested resource was not found. In the case of lambda, this can also mean it was not deployed  |
| 405           |   Method Not Allowed                  | The request was using the wrong HTTP method                   |
| 408           |   Request Timeout                     | Server did not receive the complete request by the client within the read limit |
| 429           |   Ratelimit                           | The client exceeded the rate-limit, which is based on a per-account level            |
| 500,502,504   |   Internal Server Error               | Unexpected Server Error, which can be temporary                               |
| 901           |   Error during lambda execution       | Lambda Execution failed due to an issue with the lambda coding. This can include runtime exception, exceeding processing window & returning of an error by the lambda                   |