---
copyright: 'Copyright IBM Corp. 2017'
link: 'leave-space-mutation'
is: 'experimental'
---

# Leave Space

## Concepts

The leave mutation allows you to leave a workspace by the space ID, where applicable. Currently this only applicable to spaces you are currently invited to.
In this scenario, leaveSpace is used to leave the invite. 

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
    leaveSpace(input: {id: "4aefed18-0dc0-4314-ab73-7cffeef903f1"}) {
      successful
  }
}
~~~~


