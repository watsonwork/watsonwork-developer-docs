---
copyright: 'Copyright IBM Corp. 2018'
link: 'add-a-reaction'
is: 'experimental'
---

# Add a Reaction

## Concepts

The _addReaction_ mutation allows the user to add a reaction to a message.  The mutation accepts a Message ID (targetId) and a reaction as arguments, and makes the request on behalf of the calling user, adding the specified reaction to the message.

## Schema

### Add Reaction Mutation



```graphql
type MutationRoot {
  ...
  addReaction(input: AddReactionInput!): AddReactionMutation
}

type Reaction {
  reaction: String!
  count: Int
  viewerHasReacted: Boolean!
}

type AddReactionMutation {
  reaction: Reaction!
}

type AddReactionInput {
  targetId: String!
  reaction: String!
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
    addReaction(input: {targetId: "5a209f74e4b0faa757ac1afd", reaction: "?"}) {
      reaction {
        reaction
        count
        viewerHasReacted
      }
  }
}
~~~~
