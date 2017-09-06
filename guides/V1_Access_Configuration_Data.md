---
copyright: 'Copyright IBM Corp. 2017'
link: 'access-configuration-data'
is: 'beta'
---
# Access configuration data
The configuration data is generated via Watson Work Services by Watson Workspace clients when a user triggers the configuration of your app. It contains the needed data for the configuration of the app - see [ConfigurationData](./docs#configurationdata).
It can be accessed with a configuration token which had been generated before and is exposed via an url parameter for the [App Configuration Callback](../guides/V1_App_Configuration_Callback.md). Only when the app is authorized [as an App](../references/V1_oauth_token_client_credentials.yml) it can access the configuration data.
The configuration data is not directly sent to the App Configuration Callback in order to allow the direct verification of the call to the App Configuration Callback.

The configuration data is deleted and can not be accessed again after a successful call.

The configuration data will expire after 5 minutes. Afterwards it can be no longer accessed via the configuration token - i.e. the response will be **404 - Not Found**.

### Version information
- Version: 1.0.0

### URI scheme
_Host_ : **api.watsonwork.ibm.com**
_Scheme_: **HTTPS**

### Path
```
GET v1/apps/<appId>/configurationData/<configurationToken>
```

#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The configuration data is returned and deleted successfully.|[ConfigurationData](./docs#configurationdata)|
|**401**|Unauthorized.||
|**403**|Forbidden.||
|**404**|Not Found. The app with the given `appId` or the configuration data for the given `configurationToken` could not be found.||
|**500**|Internal server error.||


#### Produces

* `application/json`


<a name="configurationdata"></a>

#### ConfigurationData
Entity that represents the configuration data for the configuration of an app for a specific space and by a specific user

|Name|Description|Schema|
|---|---|---|
|**appId**  <br>*required*|Id of the app for which the configuration data has been generated.|string|
|**spaceId**  <br>*required*|Id of the space for which the configuration data has been generated.|string|
|**userId**  <br>*required*|Id of the user by which the configuration data has been generated.|string|
