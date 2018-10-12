---
copyright: 'Copyright IBM Corp. 2018'
link: 'update-a-message'
is: 'experimental'
---

# Edit a Message

## Concepts

The _updateMessage_ mutation allows the API caller to change the contents of a message.  The mutation accepts a message id (id) and the new content (content) as arguments, and makes the request on behalf of the caller, adding the specified new content to the message replacing the previous message content.

Notes:


 - Only the author of a message can update its content.  Updating the content of messages not created by the calling user will receive a **403 Forbidden** response.

 - Existing annotations will be stripped from an updated message.  Apps are expected to regenerate any annotation using the new content.  Mention annotations are automatically regenerated based on the new content.  These annotations will be sent as `message-annotation-added` events.

 - Apps calling the updateMessage mutation using the app’s identity will be rejected with a **403 Forbidden** response, but when the app is running on behalf of a user, it will be allowed to update the user’s messages as that user.

 - An app can not update a message created via generic annotation or by using generic annotations.


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

