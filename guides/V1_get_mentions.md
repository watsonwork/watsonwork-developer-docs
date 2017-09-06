---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-mentions'
is: 'published'
---
## Get a list of mentions

This is a sample GraphqQL query on how to get information about a list of mentions.

```
query getMentions{
  mentioned(first:50) {
    items{
      space{
        id
      }
      message {
        id
        content
        updated
      }
      person {
        displayName
      }
    }
  }
}
```
