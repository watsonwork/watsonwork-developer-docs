---
copyright: 'Copyright IBM Corp. 2018'
link: 'start-meeting'
is: 'experimental'
---

# Start a meeting within a space

## Concepts

The _startMeeting_ mutation allows the API caller to start a meeting with a **space**.  The mutation accepts a Space ID (spaceId) as an argument, and makes the request on behalf of the caller, starting a meeting within the specified space.  The result will reflect the whether the call was accepted for processing by the service.

## Schema

### Start Meeting Mutation



```graphql
type MutationRoot {
  ...
  startMeeting(input: StartMeetingInput!): MeetingMutationOutput
}

type MeetingMutationOutput {
  accepted: Boolean!
}
```

## Example Request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  mutation {
    startMeeting(input: {spaceId : "5ad0fabfe4b078066d690a24"}) {
      accepted
    }
  }
}
~~~~
## Example Result

~~~~
{
  "data": {
    "startMeeting": {
      "accepted": "true"
    }
  }
}
~~~~

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental&query=mutation%20startMeeting%20{%20%20startMeeting(input: {spaceId:%20%22space-id%22})%20{%20%20%20%20accepted%20%20}}" target="_blank">Start a meeting</a>
