---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-a-list-of-moments-in-conversation'
is: 'beta'
---
## Get a list of moments in conversation

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA

or with <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta" target="_blank" >apiType=beta on the graphical GraphQL tool URL</a>.


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

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta&query=query%20getMomentsInConversation%20%7B%0Aconversation(id%3A%20%22conversation-id%22)%20%7B%0Amoments%20%7B%0Aitems%20%7B%0Aid%0Alive%0AstartTime%0AendTime%0AsummaryPhrases(first%3A%203)%20%7B%0Alabel%0A%7D%0A%7D%0A%7D%0A%7D%0A%7D" target="_blank">Get a list of moments in conversation</a>
