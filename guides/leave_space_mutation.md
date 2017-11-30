---
copyright: 'Copyright IBM Corp. 2017'
link: 'leave-space-mutation'
is: 'experimental'
---

# Leave Space

## Concepts

The leaveSpace mutation allows the user to leave a space. The mutation accepts a Space ID as an argument and makes the request on behalf of the calling user. Currently this API can only be used to reject an invitation to a space. Otherwise it will return an error.

## Schema

### Leave Space Mutation



```graphql
type MutationRoot {
  ...
  leaveSpace(input: SpaceLeaveInput!): SpaceLeaveMutation
}

type SpaceLeaveMutation {
  successful: Boolean!
}

type SpaceLeaveInput {
  id: String!
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
    leaveSpace(input: {id: "4aefed180dc04314ab737cffeef903f1"}) {
      successful
  }
}
~~~~


