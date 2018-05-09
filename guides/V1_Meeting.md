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
    meeting(spaceId: "5a9ee86ee4b0cb1ca3dfef33") {
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
