# Authenticate as an app


<a name="overview"></a>
## Overview
Request an access token for an application


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="oauth-token-post"></a>
### OAuth2 Client Credentials flow for requesting an access token for an application
```
POST /oauth/token
```


#### Description
Standard OAuth2 endpoint for authenticating clients.

More information in [Section 4.4 of RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.4)


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header where the appId and the appSecret are base64 encoded, and are sent via `Basic base64(appId:appSecret)`; e.g. `Basic YXBwOnNlY3JldA==`|string||
|**Body**|**body**  <br>*required*|Request Body|[ClientCredentialsGrantRequest](#clientcredentialsgrantrequest)||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Authentication successful.|[TokenResponse](#tokenresponse)|
|**400**|Improperly formed authentication body|[Error](#error)|
|**401**|Unauthorized|[Error](#error)|
|**500**|Internal server error|[Error](#error)|


#### Consumes

* `application/x-www-form-urlencoded`


#### Produces

* `application/json`




<a name="definitions"></a>
## Definitions

<a name="clientcredentialsgrantrequest"></a>
### ClientCredentialsGrantRequest
Entity for requesting tokens using a client credentials grant.


|Name|Description|Schema|
|---|---|---|
|**grant_type**  <br>*optional*|Client credentials grant  <br>**Default** : `"client_credentials"`|string|


<a name="error"></a>
### Error
Response entity resulting from a failed API call.


|Name|Description|Schema|
|---|---|---|
|**error**  <br>*required*|Type of error that occurred.|string|
|**error_description**  <br>*optional*|(optional) Additional details about the resulting error.|string|
|**message**  <br>*optional*|(optional) Service-defined description of error.|string|
|**path**  <br>*optional*|(optional) HTTP request path.|string|
|**status**  <br>*optional*|(optional) HTTP response code.|string|
|**timestamp**  <br>*optional*|(optional) Time at which the error occurred, in the following format: yyyy-MM-dd'T'HH:mm:ss.SSSZ|string|


<a name="tokenresponse"></a>
### TokenResponse
Client credentials authentication object


|Name|Description|Schema|
|---|---|---|
|**access_token**  <br>*optional*|Access token for application, in the form of a JWT token.|string|
|**expires_in**  <br>*optional*|Time, in seconds, before the access token expires.|integer|
|**id**  <br>*optional*|UUID for the application or user who’s access token is returned.|string|
|**jti**  <br>*optional*|UUID for the JWT token itself.|string|
|**scope**  <br>*optional*|Access scopes granted to the returned access token.|string|
|**token_type**  <br>*optional*|Defaults to `bearer` to express the type of access token being returned.|string|





