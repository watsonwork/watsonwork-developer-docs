---
copyright: 'Copyright IBM Corp. 2017'
link: 'join-space-mutation'
is: 'experimental'
---

# Join Space

## Concepts

The joinSpace mutation allows you to join a workspace by the space ID, where applicable. Currently this only applicable to spaces you are currently invited to.
In this scenario, joinSpace is used to accept the invite.

## Schema

### Join Space Mutation



```graphql
type MutationRoot {
  ...
  joinSpace(input: SpaceJoinInput!): SpaceJoinMutation
}

type SpaceJoinMutation {
  successful: Boolean!
}

type SpaceJoinInput {
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
    joinSpace(input: {id: "4aefed18-0dc0-4314-ab73-7cffeef903f1"}) {
      successful
  }
}
~~~~


