---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-public-meeting'
is: 'experimental'
---
# Get Public Meeting Details

This REST GET request allows the API caller to get details about a public meeting.

### Version information
- Version: 1.0.0

### URI scheme
_Host_ : **api.watsonwork.ibm.com**
_Scheme_: **HTTPS**

### Path
```
GET v1/publicMeeting/bySpaceId/<spaceId>
```

#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The meeting data returned.|MeetingData(see below)|


#### Produces

* `application/json`


<a name="meetingdata"></a>

#### MeetingData
Entity that represents the requested meeting.

|Name|Description|Schema|
|---|---|---|
|**meetingId**  <br>*required*|Id of the meeting.|string|
|**meetingNumber**  <br>*optional*|The Zoom meeting number if the meeting is currently active or otherwise null.|string|
|**password**  <br>*optional*|The Zoom meeting password if the meeting is currently active or otherwise null.|string|
|**active**  <br>*required*|Boolean representing whether the meeting is currently active.|string|
|**allowPublic**  <br>*required*|Boolean representing whether the meeting open to the public.|string|
|**startTime**  <br>*optional*|Start time of the active meeting or otherwise null.|string|
|**meetingProviderJoinUrl**  <br>*optional*|A URL to join the meeting with the Zoom client or otherwise null.|string|
|**meetingProviderJoinUrl**  <br>*optional*|A URL to join the meeting with the Zoom client or otherwise null.|string|
|**pstnPasscode**  <br>*optional*|The PSTN passcode of the active meeting if present or otherwise null.|string|
|**dialInNumbers**  <br>*optional*|An array of country code identifier plus dial-in number forthe active meeting or otherwise null.|string|
