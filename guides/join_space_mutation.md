---
copyright: 'Copyright IBM Corp. 2017'
link: 'join-space-mutation'
is: 'experimental'
---

# Join Space

## Concepts

The _joinSpace_ mutation allows the user to join a space. Currently this is only applicable to spaces to which the user has already been invited. The mutation accepts a Space ID as an argument and makes the request on behalf of the calling user.

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
    joinSpace(input: {id: "4aefed180dc04314ab737cffeef903f1"}) {
      successful
  }
}
~~~~


