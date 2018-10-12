# Photos


<a name="overview"></a>
## Overview
The Photo microservice API supports the storage and retrieval of photos in IBM Watson Workspace. When working with photos in Watson Work Services, the Photo microservice provides the following endpoint:
*  POST endpoint to upload a custom image to Watson Work Services.
*  To retrieve a URL for a user’s photo please see details for getting their Person object and its PhotoURL at [IBM Watson Work Services People Service Documentation](../people).


### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="updatephoto"></a>
### Upload a photo.  This endpoint will allow the caller to update its own photo or icon. Updating someone else’s photo is not allowed.
```
POST /photos/
```


#### Description
Upload a photo to the current account.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Accept**  <br>*required*|must be set to `application/json`|string||
|**Header**|**Authorization**  <br>*required*|Authorization header, in the form of `Bearer {access_token}`|string||
|**FormData**|**file**  <br>*required*|JPG photo file being uploaded, with a size of 300kb or less.|file||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Photo successfully uploaded.|No Content|
|**415**|Unsupported file media type.|No Content|
|**500**|Server error occurred on POST attempt.|No Content|


#### Consumes

* `multipart/form-data`


#### Produces

* `application/json`







