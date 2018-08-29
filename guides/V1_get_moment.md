---
link: 'get-moment-by-id'
is: 'published'
---
## Get a moment by id

This is a sample GraphQL query to get moment by id. Be sure to switch "moment-id" to the actual id you're curious about.

```
query getMomentById {
  moment(id: "moment-id") {
    id
    live
    startTime
    endTime
  }
}

```

Get a moment by ID, see it in action with our GraphQL tool.

<div class="try-it-now">
      <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMomentById%20%7B%0Amoment(id%3A%20%22moment-id%22)%20%7B%0Aid%0Alive%0AstartTime%0AendTime%0A%7D%0A%7D" target="_blank">Try it now</a>
</div>
