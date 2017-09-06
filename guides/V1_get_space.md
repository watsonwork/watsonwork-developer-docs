---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-space-details'
is: 'published'
---
## Get space details

To grab info about a space you can use the _getSpace_ GraphQL query. Be sure to switch "space-id" to the actual id you're curious about.

```
query getSpace {
  space(id: "space-id") {
    title
    description
    membersUpdated
    members {
      items {
        email
        displayName
      }
    }
    conversation{
      messages{
        items {
          content
        }
      }
    }
  }
}
```
