---
copyright: 'Copyright IBM Corp. 2017'
link: 'search-for-space-members'
is: 'future'
---

## Search for space members

This is a sample GraphQL query to retrieve all members of a space in paginated fashion. Here we are requesting up to 100 users
(`memberType: "user"`, as opposed to `"app"`) who are members of the specified space, sorted alphabetically. Successive pages of
members may be obtained using `pageInfo` (i.e., to get the next page, pass the `endCursor` from `pageInfo` as the `after`
parameter on the next request). An additional boolean parameter may optionally be added to `includeRequester`, who is otherwise
omitted by default.

```
{
  searchSpaceMembers(spaceId: "5746d50e1e623a84bd003862", memberType: "user", size: 100) {
    items {
      displayName
      extId
      email
    }
    pageInfo {
      startCursor
      endCursor
      hasPreviousPage
      hasNextPage
    }
  }
}
```

Try it out with our GraphQL tool - <a href="https://workspace.ibm.com/graphql?query=%7B%0A%20%20searchSpaceMembers(spaceId%3A%20%225746d50e1e623a84bd003862%22%2C%20memberType%3A%20%22user%22%2C%20size%3A%20100)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20extId%0A%20%20%20%20%20%20email%0A%20%20%20%20%7D%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20startCursor%0A%20%20%20%20%20%20endCursor%0A%20%20%20%20%20%20hasPreviousPage%0A%20%20%20%20%20%20hasNextPage%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Retrieve Members</a>

This is a sample GraphQL query to search for members of a space by name. Here we are asking for all members of the specified
space whose names match the string "john". (An additional parameter `phonetic: true`, can optionally be passed to obtain
matches phonetically similar to the specified `name`.)

```
{
  searchSpaceMembers(spaceId: "5746d50e1e623a84bd003862", name: "john") {
    items {
      displayName
      extId
      email
    }
  }
}
```

Try it out with our GraphQL tool - <a href="https://workspace.ibm.com/graphql?query=%7B%0A%20%20searchSpaceMembers(spaceId%3A%20%225746d50e1e623a84bd003862%22%2C%20name%3A%20%22john%22)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20extId%0A%20%20%20%20%20%20email%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Search for Members</a>
