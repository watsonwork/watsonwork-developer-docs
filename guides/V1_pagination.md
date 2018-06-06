---
copyright: 'Copyright IBM Corp. 2017'
link: 'pagination'
is: 'published'
---

## Pagination: Iterate over messages in a conversation one page at a time

The **pageInfo** element is available for any of the collections (people, spaces, members, messages, etc.). It contains 4 elements to help you determine if there is more data and how to specify the start or end boundaries in the next request for more information from that collection.

Utilize the **startCursor** and **endCursor** string values to determine the offset for the next request in the start and end arguments to the collection query.

Utilize the **hasNextPage** and **hasPreviousPage** boolean values to determine if there is more data.


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
