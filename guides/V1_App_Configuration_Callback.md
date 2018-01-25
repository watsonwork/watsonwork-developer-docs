---
copyright: 'Copyright IBM Corp. 2017'
link: 'app-configuration-callback'
is: 'published'
---
## App Configuration Callback
This callback has to be implemented to provide the user-specific configuration service of an app. The request is triggered when a user clicks on the **Configure** button of an app.

Changes in version 1.1.0
- New url parameter `configurationToken`
- Deprecate url parameter `spaceId`

## Version information
- Version: 1.1.0

## URI scheme
_Host_ : **api.watsonwork.ibm.com**
_Scheme_: **HTTPS**

## Path
```
GET <configurationURL>?configurationToken=<configurationToken>
```

The **configurationURL** is the one that was registered for the app. It is required to be a fully qualified URL using the **https** protocol.

The **configurationToken** url parameter contains the configuration token which has to be used to access the configuration data via Watson Work Services - see [Access configuration data](./docs#access-configuration-data). This configuration token is generated via Watson Work Services together with corresponding configuration data when the user triggers the configuration of an app for a specific space. The Watson Workspace client triggers its generation and appends this url parameter before the **configurationURL** is called by the Watson Workspace client.

The _deprecated_ **spaceId** url parameter gets appended when the configurationURL is loaded and it contains the **ID** of the space for which the configuration of the app should take place.
This url parameter will be removed in the near future and shall no longer be used.

### Response

HTTP status code **200 OK**

There is no further evaluation of the response code and no error handling in place.   
