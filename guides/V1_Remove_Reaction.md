---
copyright: 'Copyright IBM Corp. 2018'
link: 'remove-a-reaction'
is: 'published'
---

# Remove a Reaction

## Concepts

The _removeReaction_ mutation allows the API caller to remove a reaction from a message.  The mutation accepts a Message ID (targetId) and a reaction as arguments, and makes the request on behalf of the caller, removing the specified reaction from the message.  The result will reflect the current **count** of users that reacted with the same **reaction** (string/emoji), and **viewerHasReacted** as to whether the caller has reacted (false).

## Schema

### Remove Reaction Mutation



```graphql
type MutationRoot {
  ...
  removeReaction(input: RemoveReactionInput!): RemoveReactionMutation
}

type Reaction {
  reaction: String!
  count: Int
  viewerHasReacted: Boolean!
}

type RemoveReactionMutation {
  reaction: Reaction!
}

type RemoveReactionInput {
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
    removeReaction(input: {targetId: "5a209f74e4b0faa757ac1afd", reaction: ":-)"}) {
      reaction {
        reaction
        count
        viewerHasReacted
      }
  }
}
~~~~
## Example Result

~~~~
{
  "data": {
    "removeReaction": {
      "reaction": {
        "reaction": ":-)",
        "count": 0,
        "viewerHasReacted": false
      }
    }
  }
}
~~~~

