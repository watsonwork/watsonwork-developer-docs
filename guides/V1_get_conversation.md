---
copyright: 'Copyright IBM Corp. 2017'
link: 'view-the-conversation-in-a-space'
is: 'published'
---
## View the conversation in a space

This is a sample GraphQL query on how to get information about a conversation.

```
query getConversation {
  conversation(id: "conversation-id") {
    id
    created
    updated
    messages(first: 50) {
      items {
        content
        contentType
        annotations
      }
    }
  }
}
```
