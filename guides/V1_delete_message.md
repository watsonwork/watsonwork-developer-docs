---
copyright: 'Copyright IBM Corp. 2017, 2018'
link: 'delete-a-message'
is: 'published'
---

# Delete a message

## Concepts

The _deleteMessage_ mutation allows the user to delete a message. Currently this is only applicable to messages which have been authored by the user. The mutation accepts a Message ID as an argument and makes the request on behalf of the calling user.

## Schema

### Delete Message Mutation



```graphql
type MutationRoot {
  ...
  deleteMessage(input: DeleteMessageInput!): DeleteOutput
}

type DeleteOutput {
  successful: Boolean!
}

type DeleteMessageInput {
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
    deleteMessage(input: {id: "5a209f74e4b0faa757ac1afd"}) {
      successful
  }
}
~~~~
