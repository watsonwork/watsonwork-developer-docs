---
copyright: 'Copyright IBM Corp. 2017'
link: 'delete-a-space'
is: 'published'
---
## Delete a space

Once a space has served its purpose you can delete it with the _deleteSpace_ GraphQL mutation:

```
mutation deleteSpace {
  deleteSpace(input: { id: "space-id"}){
    successful
  }
}
```
