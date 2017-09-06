---
copyright: 'Copyright IBM Corp. 2017'
link: 'update-space-details'
is: 'published'
---
## Update space details

Is your space in need of a change? Take a look as this simple GraphQL mutation to update the space title:

```
mutation updateSpaceTitle {
  updateSpace(input: { id: "space-id", title: "Space title",  members: ["user3-id", "user4-id"]}){
    space {
      title
    }
  }
}
```

### Add Members

Get the conversation rolling by adding more members. Combine the list of IDs of the new members along with the _memberOperation_ **ADD**;

```
mutation updateSpaceAddMembers {
  updateSpace(input: { id: "space-id", title: "Space title",  members: ["user3-id", "user4-id"], memberOperation: ADD}){
    memberIdsChanged
    space {
      title
      membersUpdated
      members {
        items {
          email
          displayName
        }
      }
    }
  }
}
```

### Remove Members

Space feeling a little crowded? Remove IDs of members using the _memberOperation_ **REMOVE**

```
mutation updateSpaceRemoveMembers {
  updateSpace(input: { id: "space-id", title: "Space title",  members: ["user3-id", "user4-id"], memberOperation: REMOVE}){
    memberIdsChanged
    space {
      title
      membersUpdated
      members {
        items {
          email
          displayName
        }
      }
    }
  }
}
```
