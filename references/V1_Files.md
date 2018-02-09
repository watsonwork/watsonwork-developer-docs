# Files


<a name="overview"></a>
## Overview
Upload a file, create a message with the file and add the file to the Resource Drawer of a space.


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com  
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="v1-spaces-spaceid-files-post"></a>
### Share a file with a space.
```
POST /v1/spaces/{spaceId}/files
```


#### Description
Upload a file, create a message with the file and add the file to the Resource Drawer of a space.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header, in form of `Bearer {access_token}`|string||
|**Path**|**spaceId**  <br>*required*|The space id to share the file with.|string||
|**Query**|**dim**  <br>*optional*|Renders an image in the transcript with given dimensions (WIDTH)x(HEIGHT) in pixels, example ?dim=400x300|string||
|**FormData**|**file**  <br>*required*|The content of the file.|file||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**201**|File was shared successfully.|[Response](#response)|
|**400**|Improperly formed message body.|[Error](#error)|
|**401**|Unauthorized.|[Error](#error)|
|**403**|Forbidden.|[Error](#error)|
|**500**|Internal server error.|[Error](#error)|


#### Consumes

* `multipart/form-data`


#### Produces

* `application/json`




<a name="definitions"></a>
## Definitions

<a name="error"></a>
### Error
Response entity resulting from failed API call.


|Name|Description|Schema|
|---|---|---|
|**error**  <br>*optional*|The HTTP response message.|string|
|**message**  <br>*optional*|Service defined description of error.|string|
|**path**  <br>*optional*|The HTTP request path.|string|
|**status**  <br>*optional*|The HTTP response code.|string|
|**timestamp**  <br>*optional*|The time at which the error occurred.|string|


<a name="response"></a>
### Response
Complete response entity resulting from successful API call.


|Name|Description|Schema|
|---|---|---|
|**created**  <br>*optional*|Date and time when was was created, as milliseconds since January 1, 1970 00:00:00 UTC.|string|
|**createdBy**  <br>*optional*|ID of the creator of the file.|string|
|**id**  <br>*optional*|ID generated for file.|string|
|**name**  <br>*optional*|The name of the file.|string|
|**size**  <br>*optional*|The size of the file in bytes, uploads are capped at 20 megabytes.|integer|
|**urls**  <br>*optional*|File access URLs (require Authorization token to invoke.)  metadata, link to file info.  noredirect_download, link to file contents in X-CONTENT-LOCATION header.  redirect_download, link to file contents via 302 redirect.  If the file is flagged as potential malware, attempts to download the file will result in 404.|string|





