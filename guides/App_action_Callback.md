# App Actions Callback
The callback has to be implemented to provide the user-specific configuration service of an app. The request is triggered when a user clicks on the **Configure** button of an app.

## URI scheme
_Host_ : **api.watsonwork.ibm.com**
_Scheme_: **HTTPS**

## Path
```
actionURL?actionHandlerContextToken=<token>
```

The **actionURL** is the one that was registered for the app. It is required to be a fully qualified URL using the **https** protocol.

The **actionHandlerContextToken** url parameter contains the configuration token which has to be used to get the action context information via Watson Work Services - see [Get action context information](../guides/get_action_context.md). This action handler token is generated via Watson Work Services together when the user triggers the configuration of an app for a specific space or when the team administrator triggers app configuration for a specific team.


### Response

HTTP status code **200 OK**

There is no further evaluation of the response code and no error handling in place.
