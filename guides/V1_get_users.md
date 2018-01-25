---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-users'
is: 'published'
---
## Get a list of users

Now that you can [get information for one person](https://developer.watsonwork.ibm.com/docs/people/get-user-information), here is the GraphQL query to get information about a list of people.   In this example, we are specifying an array of user IDs to get information for these specific users.

```
query getProfiles {
  people(id: ["user-id1", "user-id2"]) {
    items {
      id
      displayName
      email
    }
  }
}
```

Next, let's just grab the first ten users' information:

```
query getProfiles {
  people(first: 10) {
    items {
      id
      displayName
      email
    }
  }
}
```

<a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getProfiles%20%7B%0A%20%20people(first%3A%2010)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20email%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank"> Try it now</a>

Let's say you just want to get a list of users named 'Kevin'.   This example GraphQL query shows how to return the first five users in a space named Kevin.

```
query getProfiles {
  people(name: "Kevin", first: 5) {
    items {
      id
      displayName
      email
    }
  }
}
```

<a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getProfiles%20%7B%0A%20%20people(name%3A%20%22Kevin%22%2C%20first%3A%205)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20email%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank"> Try it now</a>
