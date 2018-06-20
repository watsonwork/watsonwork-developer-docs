---
copyright: 'Copyright IBM Corp. 2018'
link: 'update-a-message'
is: 'experimental'
---

# Edit a Message

## Concepts

The _updateMessage_ mutation allows the API caller to change the contents of a message.  The mutation accepts a message id (id) and the new content (content) as arguments, and makes the request on behalf of the caller, adding the specified new content to the message replacing the previous message content.

## Schema

### Update Message Mutation



```graphql
type MutationRoot {
  ...
  updateMessage(input: UpdateMessageInput!): MessageMutation
}

type UpdateMessageInput {
  id: String!
  content: String!
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
    updateMessage(input: {
      id: "message_id",
      content:"message_content"
    }) {
        id
        content
        contentUpdated
        updated
        updatedBy {
          email
        }
    }
  }
}
~~~~
## Example Result

~~~~
{
  "data": {
    "message": {
      "id": "message_id",
      "content": "updated_message",
      "contentUpdated": "2017-11-05T01:23:55.712+0000",
      "updated": "2017-11-05T01:23:55.712+0000",
      "updatedBy": {
        "email": "abc@mail.com"
      }
    }
  }
}
~~~~

