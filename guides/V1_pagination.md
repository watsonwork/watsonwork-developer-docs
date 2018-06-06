---
copyright: 'Copyright IBM Corp. 2017'
link: 'pagination'
is: 'published'
---

## Pagination: Iterate over messages in a conversation one page at a time

The **pageInfo** element is available for any of the collections (people, spaces, members, messages, etc.)
It contains the place where the results start and end, relative to the results and identified by strings in startCursor and endCursor.  Do not assume these strings to be numbers.  Utilize the **hasNextPage** and **hasPreviousPage** boolean values to determine if there is more data.
```
{
  conversation (id: "conversation-id") {
    id
    updated
    created
    messages (first:10, after: "MTUwNDIwNzI3NjQ4OA==") {
      pageInfo {
        startCursor
        endCursor
        hasPreviousPage
        hasNextPage
      }
      items {
        content
      }
    }
  }
}
```
