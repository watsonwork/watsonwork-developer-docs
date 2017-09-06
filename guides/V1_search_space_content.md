---
copyright: 'Copyright IBM Corp. 2017'
link: 'search-for-space-content'
is: 'future'
---

## Search for space content

This is a sample GraphQL query to search for messages across spaces to which you have access. Here we are requesting messages
matching the string "interesting fact". The collection returned includes a maximum of 50 messages by default; this may be
changed by passing an additional `size` parameter. If the `total` number of matching messages exceeds the number returned,
successive pages of messages may be obtained using `pageInfo` (i.e., to get the next page, pass the `endCursor` from `pageInfo`
as the `after` parameter on the next request).

Additional optional parameters may be included as follows:
 - `locale`: Locale string, e.g. `en`
 - `searchFields`: Message fields in which to search for the `query` string; defaults are `content`, `annotation.content` and
   `annotation.file_name`
 - `from`: Sender user ID(s)
 - `in`: Space ID(s)
 - `dateFrom`: Earliest timestamp to search
 - `dateTo`: Latest timestamp to search

```
{
  searchMessages(query: "interesting fact") {
    items {
      message {
        content
        contentType
        id
        created
        createdBy {
          displayName
        }
      }
      highlights {
        field
        highlighted
      }
      space {
        id
        title
      }
    }
    pageInfo {
      startCursor
      endCursor
      hasPreviousPage
      hasNextPage
    }
    total
  }
}
```

Try it out with our GraphQL tool - <a href="https://workspace.ibm.com/graphql?query=%7B%0A%20%20searchMessages(query%3A%20%22interesting%20fact%22)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20message%20%7B%0A%20%20%20%20%20%20%20%20content%0A%20%20%20%20%20%20%20%20contentType%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20created%0A%20%20%20%20%20%20%20%20createdBy%20%7B%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20highlights%20%7B%0A%20%20%20%20%20%20%20%20field%0A%20%20%20%20%20%20%20%20highlighted%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20space%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%20%20pageInfo%20%7B%0A%20%20%20%20%20%20startCursor%0A%20%20%20%20%20%20endCursor%0A%20%20%20%20%20%20hasPreviousPage%0A%20%20%20%20%20%20hasNextPage%0A%20%20%20%20%7D%0A%20%20%20%20total%0A%20%20%7D%0A%7D" target="_blank">Search for Messages</a>
