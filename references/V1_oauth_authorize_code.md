# Authorize on behalf of a user


<a name="overview"></a>
## Overview
Request authorization code to authorize on behalf of a user.


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com  
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="oauth-authorize-get"></a>
### Authorize as a user with the authorization code grant flow
```
GET /oauth/authorize
```


#### Description
Standard OAuth2 endpoint for authorizing users via OAuth2. This endpoint returns an Authorization Code

 More Information in [Section 4.1 of RFC 6749](https://tools.ietf.org/html/rfc6749#section-4.1)

Example: https://api.watsonwork.ibm.com/oauth/authorize?response_type=code&client_id=123456789&redirect_uri=example.mybluemix.net/callback&state=123456789


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Query**|**client_id**  <br>*required*|Your application's id (appId)|string||
|**Query**|**redirect_uri**  <br>*required*|Redirect after completing interaction with IdP (Identity Provider).|string||
|**Query**|**response_type**  <br>*required*|Desired response type. Code grant uses `code`.|enum (code)|`"code"`|
|**Query**|**scope**  <br>*optional*|Level of access that the app wants the user to authorize. If not specified, the default scopes on app creations will be used.|string||
|**Query**|**state**  <br>*required*|An opaque value to prevent Cross-Site request forgery. Apps should use the following guidelines https://tools.ietf.org/html/rfc6749#section-10.12|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**302**|If we grant the access request, the authorization server issues an authorization code and delivers it to the client by adding that code and the state to the query component of the redirection URI. Example: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz<br><br>Error Response: If we deny the access request, we will add error=access_denied to the query component of the redirection URI.  <br>**Headers** :   <br>`Location` (string)  <br>`Set-Cookie` (string)|No Content|







