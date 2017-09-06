---
copyright: 'Copyright IBM Corp. 2017'
link: 'search-for-people'
is: 'future'
---
## Search for people

This is a sample GraphQL query to search for people by name. Here we are looking for people whose names contain "john", or
(optionally) a phonetically similar string. The requested property `directMessageSpaceId` will be populated for people with  
whom we have an existing direct message conversation, and null for others within our organization with whom we have yet to
converse directly.

Other (optional) parameters which may be included are:
 - `sources`: Specify whether to search in `DM`s, shared `SPACES`, and/or your `ORGANIZATION` (default if omitted is all sources)
 - `size`: Maximum number of matching results to return
 - `includeRequester`: A boolean indicating whether or not the requesting user should be included in results

```
{
  searchPeople(name: "john", phonetic: true) {
    items {
      displayName
      extId
      email
      directMessageSpaceId
  }
}
```

Try it out with our GraphQL tool - <a href="https://workspace.ibm.com/graphql?query=%7B%0A%20%20searchPeople(name%3A%20%22john%22%2C%20phonetic%3A%20true)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20extId%0A%20%20%20%20%20%20email%0A%20%20%20%20%20%20directMessageSpaceId%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Search for People</a>
