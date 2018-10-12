---
copyright: 'Copyright IBM Corp. 2018'
link: 'meeting'
is: 'experimental'
---

# Get meeting details

## Concepts

The _meeting_ query allows the API caller to get details about the meeting.  The query accepts either a Space ID (spaceId) or a meeting ID (id) and will return meeting details if the calling user has access to the meeting.  The calling user will have access to the meeting if the user has access to the space which contains the meeting, or the meeting has been marked to allow public participants.

## Schema

### Meeting Query


```graphql
type QueryRoot {
  ...
  meeting(spaceId: ID, id: ID): Meeting
}

type MeetingRecording {
  url: String!
  startTime: Date
  stopTime: Date
}

type DialInNumber {
  countryCode: String!
  number: String!
}

type JoinInfo {
  allowPublic: Boolean!
  meetingNumber: String
  meetingProviderJoinUrl: String
  password: String
  hostKey: String!
  pstnPasscode: String
  webJoinToken: String!
  dialInNumbers : [DialInNumber]
}

type Meeting {
  id: ID!
  active: Boolean!
  allowPublic: Boolean!
  startTime: Date
  endTime: Date
  description: String
  recordings: [MeetingRecording]
  activeParticipants: PersonCollection
  attendees: PersonCollection
  space: Space!
  startedBy: Person
  message: Message
  joinInfo: JoinInfo
}

```

## Field definitions

# MeetingRecording
|Name|Description|Schema|
|---|---|---|---|
|**url**|The URL pointing to the meeting recording MP4 file.|**String** <br>_required_|
|**startTime** |The start date/time of the meeting recording |**Date**|
|**stopTime** |The stop date/time of the meeting recording |**Date**|


# DialInNumber
|Name|Description|Schema|
|---|---|---|---|
|**countryCode**|Two character country code where the number resides|**String** <br>_required_|
|**number**|E.164 phone number which can be used to dial into the meeting|**String** <br>_required_|

# JoinInfo
|Name|Description|Schema|
|---|---|---|---|
|**allowPublic** |Whether the meeting can be joined by non-members of the space|**Boolean** <br>_required_|
|**meetingNumber**|If a meeting is active, the a string of digits representing the Zoom meeting|**String** <br>_required_|
|**meetingProviderJoinUrl**|A URL which can be used to directly joint he meeting in a browser|**String** <br>_required_|
|**password** |If a meeting is active, the password required to join the Zoom meeting|**String**|
|**hostKey** |If a meeting is active and there is no current host, the host key required to claim host.|**String**|
|**pstnPasscode**|If required, the DTMF digits necessary to join a meeting via a phone dial in|**String**|
|**webJoinToken** |If a meeting is active, the token required to join via the web client.|**String** <br>_required_|
|**dialInNumbers**|An array of DialInNumber objects|** DialInNumber** array|

# Meeting
|Name|Description|Schema|
|---|---|---|---|
|**id**|ID of the meeting|**String** <br>_required_|
|**active**|Whether the meeting is currently active|**Boolean** <br>_required_|
|**allowPublic** |Whether the meeting can be joined by non-members of the space|**Boolean** <br>_required_|
|**startTime** |The start date/time of the meeting |**Date**|
|**endTime** |The date/time the meeting ended |**Date**|
|**description**|A description for the meeting|**String**|
|**recordings**|An array of MeetingRecording objects.  A new MeetingRecording is created each time a cloud recording is started in the meeting.|** MeetingRecording** array|
|**activeParticipants**|If a meeting is active, a PersonCollection representing the current Workspace users.|**PersonCollection**|
|**attendeesParticipants**|A PersonCollection representing the Workspace users who have attended the meeting.|**PersonCollection**|
|**space** |The Space where the meeting was held.|**Space** <br>_required_|
|**message** |A Message representing where in the Space transcript the meeting occurred. |**Message**|
|**joinInfo** |If a meeting is active, the details required to join the meeting |**JoinInfo**|



## Example Request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  query {
    meeting(spaceId: "space-id") {
      active
    	joinInfo {
        meetingNumber
        password
    	  meetingProviderJoinUrl
    	}
    }
  }
}
~~~~
## Example Result

~~~~
{
    "data": {
        "meeting": {
            "active": true,
            "joinInfo": {
                "password": "235253938",
                "password": "53621872",
                "meetingProviderJoinUrl": "https://zoom.us/j/235253938?pwd=vBRBlZBaXAKwIumekTziMw"
            }
        }
    }
}
~~~~

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental&query=query%20getMeetingBySpaceId%20{%20%20meeting(spaceId:%20%22space-id%22)%20{%20%20%20%20startTime%20%20%20%20active%20%20%20%20allowPublic}}" target="_blank">Get a meeting by space-id</a>
