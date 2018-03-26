# Webhooks


<a name="overview"></a>
## Overview
This API has to be implemented by the callbacks implementing outbound webhooks.

- Changes in version 1.6.0:
  - New event type and notification format for `space-updated` and `space-deleted`.
- Changes in version 1.5.0:
  - New event type and notification format for `reaction-added` and `reaction-removed`.
- Changes in version 1.4.0:
  - New event type and notification format for `message-deleted`.
- Changes in version 1.3.0:
  - Fields of input and output entities are correctly marked as required.
- Changes in version 1.2.0:
  - New event types and notification formats for `message-annotation-added`, `message-annotation-edited`, and `message-annotation-removed`.
  - Changed type of `time` fields to 64 bit (long) integers.
- Changes in version 1.1.0:
  - The verification process of outbound webhooks has changed.
  - The `GET` endpoint has been removed.  The `POST` endpoint is now used for the verification of outbound webhooks.


### Version information
*Version* : 1.2.0


### URI scheme
*Host* : api.watsonwork.ibm.com  
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="callbackurl-post"></a>
### Send an event to the webhook callback or verify a webhook callback.
```
POST /{callbackUrl}
```


#### Description
Callbacks of outbound webhooks are called in two situations:
- Webhook verification: Verify that the webhook is under the control of the person who added it to an app.
For verifications the `type` value in the body is `verification`.  A verification is successful if these conditions are met:
  - The response status is 200.
  - The JSON response body contains the verification challenge in the `response` value.
  - The header field `X-OUTBOUND-TOKEN` contains the `HMAC-SHA256` hash of the body with the `webhookSecret` as key.
- Event notification:  Each webhook callback is only notified about events for which it has been added to an app.
For notifications the `type` value in the body is the type of the event.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Content-Type**  <br>*required*|has to be `application/json;charset=UTF-8`|string||
|**Header**|**X-OUTBOUND-INDEX**  <br>*required*|Only used for event notifications.<br><br>An index that is increased with each successful event notification.  Each combination of app and space have their own counter.<br>Allows detection of missed events, e.g. because the receiving callback was offline for an extended period of time.|integer||
|**Header**|**X-OUTBOUND-RETRY-COUNT**  <br>*optional*|Only used for event notifications.<br><br>An index that is increased with each failed event notification and that is reset to 0 with the next successful notification.<br>Allows the callback to be idempotent.<br>A value of 0 (the default) indicates a regular notification, the first retry has a count of 1.|integer|`"0"`|
|**Header**|**X-OUTBOUND-TOKEN**  <br>*required*|Used for webhook verification and event notification.<br><br>An `HMAC-SHA256` hash of the JSON request body.<br>The hash is generated with the `webhookSecret` of the webhook as key.<br>This key is returned during registration of app and webhook.<br><br>This token can be used by the receiver to verify that the request really comes from Watson Work Services.<br><br>Note that this token is used primarily in request headers.  For verification requests it is additionally expected in the<br>response header.  In this case it has to hash the response body.  That means that for verification requests the `X-OUTBOUND-TOKEN` is<br>part of the request and of the response header and typically has different values in each.|string||
|**Path**|**callbackUrl**  <br>*required*|**General Description:**<br>The URL as specified on webhook creation.<br>It is the **url** field of the webhook entity that is provided with the **POST** or **PUT** request to **/v1/apps**, that adds the webhook.<br>See App Registry API for details.<br><br>**Requirements to URL:** The following requirements are checked by webhook registration (even if the webhook is disabled):<br>  - only **https** protocol is supported<br>  - the usage of IP addresses in host name is not allowed, only domain names are allowed.<br>  - _localhost_ as hostname is not allowed<br>  - the host name should be resolvable, the resulting IP address must **not** take following values:<br><br>  **for IPv4 protocol:**<br>  **0.\*.\*.\***                  - local network<br>  **10.\*.\*.\***                 - private network<br>  **172.16.\*.\***                - private network<br>  **192.168.\*.\***               - private network<br>  **127.\*.\*.\***                - loopback<br>  **169.254.\*.\***               - link local<br>  **192.0.0.8-255**               - IETF Protocol Assignments<br>  **192.0.2.\***                  - TEST-NET-1<br>  **198.51.100.\***               - TEST-NET-2<br>  **203.0.113.\***                - TEST-NET-3<br>  **223.255.255.\***              - Reserved<br>  **224.0.0.0 - 239.255.255.255** - Multicast<br>  **240.0.0.0 - 255.255.255.254** - Reserved<br>  **255.255.255.255**             - Broadcast<br><br>  **for IPv6 protocol:**<br>  **::**                             - Unspecified address<br>  **::1**                            - Loopback<br>  **::ffff:\*:\***                   - IPv4, please see table above for the range of restricted IPv4 addresses<br>  **2001:db8:\*:\*:\*:\*:\*:\***     - Documentation<br>  **fe80-febf:\*:\*:\*:\*:\*:\*:\*** - Link Local<br>  **:ff00:\*:\*:\*:\*:\*:\*:\***     - Multicast<br><br>**HTTPS handshake:** The webhook server has to support the TLSv1.2 protocol. The trust chain of a certificate must connect to a known and trusted root certificate. In case self-signed certificates should be supported (certificates with no trust chain), isSelfSignedAllowed url parameter must be specified when enabling the webhook. The callback server must support at least one of the following ciphers (IBM JDK notation):<br><br>    SSL_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>    SSL_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>    SSL_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>    SSL_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>    SSL_DHE_RSA_WITH_AES_256_GCM_SHA384<br>    SSL_DHE_RSA_WITH_AES_128_GCM_SHA256<br>    SSL_DHE_RSA_WITH_AES_128_CBC_SHA256|string||
|**Body**|**body**  <br>*required*|message body|[InputBody](#inputbody)||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Successfully received request.  Supported for event notification and webhook verification.|[VerificationOutputBody](#verificationoutputbody)|
|**201**|Successfully received request.  Only supported for event notification.|No Content|
|**203**|Successfully received request.  Only supported for event notification.|No Content|
|**204**|Successfully received request.  Only supported for event notification.|No Content|
|**default**|Any other status including redirect (3xx) is interpreted as failed notification.<br>Also, when a timeout of 3s is triggered then the notification failed.<br>In either case the event notification is scheduled for retry.<br>Retries are made at time intervals of every 30s during the first 2 hours and then at 3h, 6h, 12h, 24h, 36h, 72h after the first failed notification.<br>After this, the event will be discarded.<br>This retry is tied to the space for the event in question.|No Content|


#### Consumes

* `application/json`


#### Produces

* `application/json`




<a name="definitions"></a>
## Definitions

<a name="inputbody"></a>
### InputBody
One of (ignore that the next line says 'all of')

*Polymorphism* : Composition


|Name|Description|Schema|
|---|---|---|
|**annotationId**  <br>*required*|Id of the annotation that has been removed.|string|
|**annotationPayload**  <br>*required*|Content of the edited annotation.  The format is JSON converted to a string.|string|
|**annotationType**  <br>*required*|Type of the edited annotation.|string|
|**challenge**  <br>*required*|A random string that is used only once.|string|
|**content**  <br>*required*|Message content.|string|
|**contentType**  <br>*required*|Mime type of the message content.|string|
|**memberIds**  <br>*required*|List of ids of the members that where added.|< string > array|
|**messageId**  <br>*required*|Id of the message from which the annotation has been removed.|string|
|**spaceId**  <br>*required*|Id of the space to which the message belongs from which the annotation has been removed.|string|
|**spaceName**  <br>*required*|Name of the space to which the message belongs from which the annotation has been removed.|string|
|**time**  <br>*required*|Time and date of annotation removed, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-annotation-removed`.|string|
|**userId**  <br>*required*|Id of the user who removed the annotation.|string|
|**userName**  <br>*required*|Name of the user who removed the annotation.|string|


<a name="messageannotationaddedbody"></a>
### MessageAnnotationAddedBody
Notifies that an annotation has been added to a message.


|Name|Description|Schema|
|---|---|---|
|**annotationId**  <br>*required*|Id of the new annotation.|string|
|**annotationPayload**  <br>*required*|Content of the annotation.  The format is JSON converted to a string.|string|
|**annotationType**  <br>*required*|Type of the new annotation.|string|
|**messageId**  <br>*required*|Id of the message to which the annotation has been added.|string|
|**spaceId**  <br>*required*|Id of the space to which the message belongs.|string|
|**spaceName**  <br>*required*|Name of the space to which the message belongs.|string|
|**time**  <br>*required*|Time and date of annotation added, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-annotation-added`.|string|
|**userId**  <br>*required*|Id of the user who added the annotation.|string|
|**userName**  <br>*required*|Name of the user who added the annotation.|string|


<a name="messageannotationeditedbody"></a>
### MessageAnnotationEditedBody
Notifies that an annotation that is bound to a message has been edited.


|Name|Description|Schema|
|---|---|---|
|**annotationId**  <br>*required*|Id of the modified annotation|string|
|**annotationPayload**  <br>*required*|Content of the edited annotation.  The format is JSON converted to a string.|string|
|**annotationType**  <br>*required*|Type of the edited annotation.|string|
|**messageId**  <br>*required*|Id of the message to which the modified annotation belongs.|string|
|**spaceId**  <br>*required*|Id of the space to which the message belongs.|string|
|**spaceName**  <br>*required*|Name of the space to which the message belongs.|string|
|**time**  <br>*required*|Time and date of annotation edited, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-annotation-edited`.|string|
|**userId**  <br>*required*|Id of the user who modified the annotation.|string|
|**userName**  <br>*required*|Name of the user who modified the annotation.|string|


<a name="messageannotationremovedbody"></a>
### MessageAnnotationRemovedBody
Notifies that an annotation has been removed from a message.


|Name|Description|Schema|
|---|---|---|
|**annotationId**  <br>*required*|Id of the annotation that has been removed.|string|
|**messageId**  <br>*required*|Id of the message from which the annotation has been removed.|string|
|**spaceId**  <br>*required*|Id of the space to which the message belongs from which the annotation has been removed.|string|
|**spaceName**  <br>*required*|Name of the space to which the message belongs from which the annotation has been removed.|string|
|**time**  <br>*required*|Time and date of annotation removed, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-annotation-removed`.|string|
|**userId**  <br>*required*|Id of the user who removed the annotation.|string|
|**userName**  <br>*required*|Name of the user who removed the annotation.|string|


<a name="messagecreatedbody"></a>
### MessageCreatedBody
Notifies the creation of a new message in a space.

This event is only sent to webhooks that
- have been added for the message-created event
- and belong to an app that is a member of the space.


|Name|Description|Schema|
|---|---|---|
|**content**  <br>*required*|Message content.|string|
|**contentType**  <br>*required*|Mime type of the message content.|string|
|**messageId**  <br>*required*|Unique id of the message.|string|
|**spaceId**  <br>*required*|Id of the space in which the message was created.|string|
|**spaceName**  <br>*required*|Name of the space in which the message was created.|string|
|**time**  <br>*required*|Time and date of message creation, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-created`.|string|
|**userId**  <br>*required*|Id of the user who created the message.|string|
|**userName**  <br>*required*|Name of the user who created the message.|string|


<a name="messagedeletedbody"></a>
### MessageDeletedBody
Notifies the deletion of a message from a space.

This event is only sent to webhooks that
- have been added for the message-deleted event
- and belong to an app that is a member of the space.


|Name|Description|Schema|
|---|---|---|
|**messageId**  <br>*required*|Unique id of the message.|string|
|**spaceId**  <br>*required*|Id of the space in which the message was deleted.|string|
|**time**  <br>*required*|Time and date of message deletion, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `message-deleted`.|string|


<a name="spacemembersaddedbody"></a>
### SpaceMembersAddedBody
Notifies that one or more members (users or apps) have been added to a space.

This event is sent only to webhooks that
- have been added for the space-members-added event
- and belong to an app that is a member of the space.


|Name|Description|Schema|
|---|---|---|
|**memberIds**  <br>*required*|List of ids of the members that where added.|< string > array|
|**spaceId**  <br>*required*|Id of the space to which members where added.|string|
|**spaceName**  <br>*required*|Name of the space to which members where added.|string|
|**time**  <br>*required*|Time and date of member addition, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `space-members-added`.|string|


<a name="spacemembersremovedbody"></a>
### SpaceMembersRemovedBody
Notifies that one or more members (users or apps) have been removed from a space.

This event is sent only to webhooks that
- have been added for the space-members-removed event
- and belong to an app that is a member of the space or which has just been removed from the space, i.e. is one of the items in the memberIds list.


|Name|Description|Schema|
|---|---|---|
|**memberIds**  <br>*required*|List of ids of the members that where added.|< string > array|
|**spaceId**  <br>*required*|Id of the space from which members where removed.|string|
|**spaceName**  <br>*required*|Name of the space from which members where removed.|string|
|**time**  <br>*required*|Time and date of member removal, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**type**  <br>*required*|The event type is `space-members-removed`.|string|

<a name="spaceupdatedbody"></a>
### SpaceUpdatedBody
Notifies that a space has been updated.

This event is sent only to webhooks that
- have been added for the message-updated event
- and belong to an app that is a member of the space.


|Name|Description|Schema|
|---|---|---|
|**spaceId**  <br>*required*|Id of the space which was updated|string|
|**userId**  <br>*required*|Id of the user who updated the space.|string|
|**type**  <br>*required*|The event type is `space-updated`.|string|
|**time**  <br>*required*|Time and date of the space being updated, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|
|**title**  <br>*optional*|The new title of the space.|string|
|**description**  <br>*optional*|The new title of the space.|string|
|**visibility**  <br>*optional*|The new visibility of the space.|string|
|**allowGuests**  <br>*optional*|The new allow guests setting of the space.|string|
|**statusValue**  <br>*optional*|The new status value of the space.|string|
|**spaceProperties**  <br>*optional*|The new space property values of the space.|Map<String, Object>|

<a name="spaceupdatedbody"></a>
### SpaceDeletedBody
Notifies that a space has been deleted.

This event is sent only to webhooks that
- have been added for the message-deleted event
- and belong to an app that was a member of the space at the time of deletion.


|Name|Description|Schema|
|---|---|---|
|**spaceId**  <br>*required*|Id of the space which was deleted.|string|
|**userId**  <br>*required*|Id of the user that deleted the space.|string|
|**type**  <br>*required*|The event type is `space-deleted`.|string|
|**time**  <br>*required*|Time and date of the space being deleted, in milliseconds since January 1st, 00:00, 1970 UTC|integer(int64)|

<a name="verificationinputbody"></a>
### VerificationInputBody
Contains a challenge that the callback has to send back in order to show that it supports this callback API.


|Name|Description|Schema|
|---|---|---|
|**challenge**  <br>*required*|A random string that is used only once.|string|
|**type**  <br>*required*|The event type is `verification`.|string|


<a name="verificationoutputbody"></a>
### VerificationOutputBody
Only used for verification requests.

Send back the verification challenge to show that the webhook supports this callback API.


|Name|Description|Schema|
|---|---|---|
|**response**  <br>*required*|The challenge that was provided in the request body of the verification request.|string|


<a name="addreactionbody"></a>
### AddReactionBody
Notifies the addition of a reaction to a message.  _Since this is an_ `EXPERIMENTAL` _capability, complete information can be found in our github repo, [see Coming Next section](../get-started/coming-next) for more info_.

This event is only sent to webhooks that
- have been added for the reaction-added event
- and belong to an app that is a member of the space.


<a name="removereactionbody"></a>
### RemoveReactionBody
Notifies the removal of a reaction from a message.  _Since this is an_ `EXPERIMENTAL` _capability, complete information can be found in our github repo, [see Coming Next section](../get-started/coming-next) for more info_.

This event is only sent to webhooks that
- have been added for the reaction-removed event
- and belong to an app that is a member of the space.





