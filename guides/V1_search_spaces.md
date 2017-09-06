---
copyright: 'Copyright IBM Corp. 2017'
link: 'search-for-spaces'
is: 'future'
---

## Search for spaces

This is a sample GraphQL query to search for spaces by title. Here we are looking for spaces whose titles contain "development".
We have added an optional parameter, `sortBy`, to ask that matching results be returned in order of most recent activity in the
space (i.e., most recently active spaces first). (`"activity""` is currently the only sort option supported.) An additional
`size` parameter may optionally be specified to limit the number of matching spaces returned.

```
{
  searchSpaces(title: "development", sortBy: "activity") {
    items {
      title
      id
    }
  }
}
```

Try it out with our GraphQL tool - <a href="https://workspace.ibm.com/graphql?query=%7B%0A%20%20searchSpaces(title%3A%20%22development%22%2C%20sortBy%3A%20%22activity%22)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20title%0A%20%20%20%20%20%20id%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Search for Spaces</a>
