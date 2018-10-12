---
link: 'get-moment-by-id'
is: 'beta'
---
## Get a moment by id

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA


This is a sample GraphQL query to get moment by id. Be sure to switch "moment-id" to the actual id you’re curious about.

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

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMomentById%20{%20%20moment(id:%20%22moment-id%22)%20{%20%20%20%20id%20%20%20%20live%20%20%20%20startTime%20%20%20%20endTime%20%20}}" target="_blank">Get a moment by id</a>
