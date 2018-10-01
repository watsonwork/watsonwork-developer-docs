# Refresh User Access Token


<a name="overview"></a>
## Overview
Refresh access token using refresh token


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="oauth-token-post"></a>
### OAuth2 flow for refreshing an access token for a user
```
POST /oauth/token
```


#### Description
Standard OAuth2 endpoint for authenticating users via OAuth2 refresh token.

More Information in [Section 6 of RFC 6749](https://tools.ietf.org/html/rfc6749#section-6)


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header where the appId and the appSecret are base64 encoded, and are sent via `Basic base64(appId:appSecret)`; e.g. `Basic YXBwOnNlY3JldA==`|string||
|**Body**|**body**  <br>*required*|Request Body|[RefreshTokenGrantRequest](#refreshtokengrantrequest)||


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


<a name="refreshtokengrantrequest"></a>
### RefreshTokenGrantRequest
Entity for requesting tokens using a refresh token grant.


|Name|Description|Schema|
|---|---|---|
|**grant_type**  <br>*optional*|Refresh token grant  <br>**Default** : `"refresh_token"`|string|
|**refresh_token**  <br>*optional*|Refresh token previously received from the /oauth/token response.|string|
|**scope**  <br>*optional*|Optional, the requested scope of the JWT token to be issued.|string|


<a name="tokenresponse"></a>
### TokenResponse
Client credentials authentication object


|Name|Description|Schema|
|---|---|---|
|**access_token**  <br>*optional*|Access token for application, in the form of a JWT token.|string|
|**displayName**  <br>*optional*|Name of the app or user whose access token is returned.|string|
|**expires_in**  <br>*optional*|Time, in seconds, before the access token expires.|integer|
|**id**  <br>*optional*|UUID for the app or user whose access token is returned.|string|
|**jti**  <br>*optional*|UUID for the JWT token itself.|string|
|**permissions**  <br>*optional*|The user’s permssion associated with the JWTToken|string|
|**providerId**  <br>*optional*|ID provider of the JWT token|string|
|**refresh_token**  <br>*optional*|Refresh token for application, in the form of a JWT token.|string|
|**scope**  <br>*optional*|Access scopes granted to the returned access token.|string|
|**token_type**  <br>*optional*|Defaults to `bearer` to express the type of access token being returned.|string|





