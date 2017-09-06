---
copyright: 'Copyright IBM Corp. 2017'
link: 'view-a-message-from-a-conversation'
is: 'published'
---
## View a message from a conversation

This is a sample GraphQL query on how to get information about a message.

```
query getMessage {
  message(id: "message-id") {
    id
    content
    contentType
    annotations
  }
}
```
