---
copyright: 'Copyright IBM Corp. 2018'
link: 'update-meeting'
is: 'experimental'
---

# Update a meeting

## Concepts

The _updateMeeting_ mutation allows the API caller to configure options on the meeting.  The mutation accepts a Space ID (spaceId), and an allowPublic boolean as arguments, and makes the request on behalf of the caller, updating the meeting within the specified space.  The result will reflect the whether the call was accepted for processing by the service.

## Schema

### Update Meeting Mutation



```graphql
type MutationRoot {
  ...
  updateMeeting(input: UpdateMeetingInput!): MeetingMutationOutput
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
    updateMeeting(input: {spaceId : "5ad0fabfe4b078066d690a24", allowPublic: true}) {
      accepted
    }
  }
}
~~~~
## Example Result

~~~~
{
  "data": {
    "updateMeeting": {
      "accepted": "true"
    }
  }
}
~~~~
