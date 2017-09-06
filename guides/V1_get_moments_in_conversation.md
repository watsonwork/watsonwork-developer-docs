---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-moments-in-conversation'
is: 'beta'
---
## Get a list of moments in conversation

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA


This is a sample GraphQL query to get moments in a space. Be sure to switch "space-id" to the actual id you're curious about.

```
query getMomentsInConversation {
  conversation(id: "space-id") {
    moments {
      items {
        id
        live
        startTime
        endTime
      }
    }
  }
}

```

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMomentsInConversation%20%7B%0A%20%20conversation(id%3A%20%22space-id%22)%20%7B%0A%20%20%20%20moments%20%7B%0A%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20live%0A%20%20%20%20%20%20%20%20startTime%0A%20%20%20%20%20%20%20%20endTime%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&operationName=getMomentsInConversation" target="_blank">Get a list of moments in conversation</a>
