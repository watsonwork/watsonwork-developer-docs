# Get User Access Token


<a name="overview"></a>
## Overview
Request an access token for a user


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="oauth-token-post"></a>
### OAuth2 Authorization Code flow for requesting an access token for a user
```
POST /oauth/token
```


#### Description
Standard OAuth2 endpoint for authenticating users via OAuth2 authorization code.

More Information in [Section 4.1.3 of RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.1.3)


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header where the appId and the appSecret are base64 encoded, and are sent via `Basic base64(appId:appSecret)`; e.g. `Basic YXBwOnNlY3JldA==`|string||
|**Body**|**body**  <br>*required*|Request Body|[AuthorizationCodeGrantRequest](#authorizationcodegrantrequest)||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Authentication successful|[TokenResponse](#tokenresponse)|
|**400**|Improperly formed authentication body.|[Error](#error)|
|**401**|Unauthorized.|[Error](#error)|
|**500**|Internal server error.|[Error](#error)|


#### Consumes

* `application/x-www-form-urlencoded`


#### Produces

* `application/json`




<a name="definitions"></a>
## Definitions

<a name="authorizationcodegrantrequest"></a>
### AuthorizationCodeGrantRequest
Entity for requesting tokens using an authorization code grant.


|Name|Description|Schema|
|---|---|---|
|**code**  <br>*optional*|Authorization code previously received from the /oauth/authorize response.|string|
|**grant_type**  <br>*optional*|Authorization code grant  <br>**Default** : `"authorization_code"`|string|
|**redirect_uri**  <br>*optional*|Must match the value that was previously sent to the /oauth/authorize request.|string|


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
|**access_token**  <br>*optional*|Access token.|string|
|**expires_in**  <br>*optional*|Time, in seconds, before the access token expires.|integer|
|**refresh_token**  <br>*optional*|Refresh token.|string|
|**scope**  <br>*optional*|Access scopes granted to the returned access token.|string|
|**token_type**  <br>*optional*|Type of the token returned. Currently always set to `bearer`.|string|





