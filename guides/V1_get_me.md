---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-my-user-information'
is: 'published'
---
## Get my user information

We also have a handy GraphQL query for when you're feeling introspective. This will allow you to get information about the user you are currently logged in as.

```
query getMyself {
  me {
    id
    displayName
    email
  }
}
```

<a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMyself%20%7B%0A%20%20me%20%7B%0A%20%20%20%20id%0A%20%20%20%20displayName%0A%20%20%20%20email%0A%20%20%7D%0A%7D%0A" target="_blank"> Try it now</a>
