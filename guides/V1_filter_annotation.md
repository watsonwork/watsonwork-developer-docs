---
copyright: 'Copyright IBM Corp. 2017'
link: 'filter-on-annotations'
is: 'published'
---
### Filter on annotations

Get a specified Space's 10 most recent messages made by 3rd party apps acting as themselves via generic annotation


```
query  {
  space(id: "space-id") {
    conversation {
      messages(first: 10, annotationType:"generic") {
        items {
          content
          id
          createdBy {
             email
             id
             displayName
          }
          annotations
        }
      }
    }
  }
}
```
