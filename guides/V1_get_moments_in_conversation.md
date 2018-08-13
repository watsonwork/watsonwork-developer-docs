---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-a-list-of-moments-in-conversation'
is: 'published'
---
## Get a list of moments in conversation

This is a sample GraphQL query to get moments in a conversation. Be sure to switch "conversation-id" to the id of the conversation you're curious about.

```
query getMomentsInConversation {
  conversation(id: "conversation-id") {
    moments {
      items {
        id
        live
        startTime
        endTime
        summaryPhrases(first: 3) {
          label
        }
      }
    }
  }
}
```

Get a list of moments in a conversation, see it in action with our GraphQL tool.

<div class="try-it-now">
      <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMomentsInConversation%20%7B%0Aconversation(id%3A%20%22conversation-id%22)%20%7B%0Amoments%20%7B%0Aitems%20%7B%0Aid%0Alive%0AstartTime%0AendTime%0AsummaryPhrases(first%3A%203)%20%7B%0Alabel%0A%7D%0A%7D%0A%7D%0A%7D%0A%7D" target="_blank">Try it now</a>
</div>
