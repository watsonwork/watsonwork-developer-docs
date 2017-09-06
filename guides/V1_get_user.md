---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-user-information'
is: 'published'
---
## Get User Information

This is the GraphQL query to get information about a person such as their name (as it would display in your app) and their email address.   

In this example, we are using the user ID to get the information.

```
query getProfile {
  person(id: "user-id") {
    id
    displayName
    email
  }
}
```

You can also get the same information about a person by using their email address.

```
query getProfile {
  person(email: "user@company.com") {
    id
    displayName
    email
  }
}
```
