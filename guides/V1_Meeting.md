---
copyright: 'Copyright IBM Corp. 2018'
link: 'meeting'
is: 'experimental'
---

# Get meeting details

## Concepts

The _meeting_ query allows the API caller to get details about the meeting.  The query accepts a Space ID (spaceId) and will return meeting details if the calling user has access to the meeting.  The calling user will have access to the meeting if the user has access to the space which contains the meeting, or the meeting has been marked to allow public participants.

## Schema

### Meeting Query


```graphql
type QueryRoot {
  ...
  meeting(spaceId: ID!): Meeting
}

type Meeting {
  active: Boolean!
  meetingNumber: String
  password: String
  allowPublic: Boolean!
  startTime: Date
  joinInfo: JoinInfo
}

type JoinInfo {
  meetingProviderJoinUrl: String
  pstnPasscode: String
  dialInNumbers : [DialInNumber]
}

type DialInNumber {
  countryCode: String!
  number: String!
}

```

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
    	password
    	joinInfo {
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
            "password": "53621872",
            "joinInfo": {
                "meetingProviderJoinUrl": "https://zoom.us/j/240286814?pwd=vBRBlZBaXAKwIumekTziMw"
            }
        }
    }
}
~~~~

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental&query=query%20getMeetingBySpaceId%20{%20%20meeting(spaceId:%20%22space-id%22)%20{%20%20%20%20startTime%20%20%20%20active%20%20%20%20allowPublic%20%20%20%20meetingNumber%20%20}}" target="_blank">Get a meeting by space-id</a>
