---
copyright: 'Copyright IBM Corp. 2017'
link: 'leave-space-mutation'
is: 'experimental'
---

# Leave Space

## Concepts

Currently this API only supports invited space members, for other members it will return an error message. The _leaveSpace_ mutation allows you to leave a workspace. The mutation accepts a Space ID as an argument and makes the request on behalf of the calling user.

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


